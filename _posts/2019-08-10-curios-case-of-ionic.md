---
layout: post
title: Curios Case of Ionic
author: Sergio Utama
date: 2019-08-10 22:41 +0800
categories: blog
---

Couple of weeks ago I was asked by my friends to help setting up **CI/CD** for an **Ionic** project. The project has no documentation and cannot be build natively. Initially I didn't notice that it was build with older version of **Ionic** (*v2*) and since there is no `platform` folder in the project, the build always failed. Only after painstaking debugging, it is clear the issue was due to older **Ionic/Cordova**, few older dependencies, and **AndroidX** support.

Here are some learning points I took after the exhausting project.


## 1. Commit your `platform` folder.

When you use **Ionic** often than not, there is a tendency to not committing the `platform` folder. This is great, until there is major update on **Ionic** or **Cordova** version. Committing `platform` folder will ensure the information preserved and even if the **Ionic/Cordova** changed, the code can still be built natively either using **Xcode** or **Android Studio**.


## 2. Install Ionic and Cordova as local dependency.

When I received the code, I couldn't build the app at all with the recent version of **Ionic** and **Cordova**. Apparently it was caused due to **AndroidX** support and some older dependencies that was not maintained (which can be solved by committing `platform` folder to repository). 

The other issue is due to **Cordova** (*v9*) which is not compatible with older dependencies. To solve it, either upgrade dependency or downgrade **Cordova**. We settle with downgrading **Cordova**. Installing **Ionic** and **Cordova** locally as dependency can solve this issue.

Run
```sh
npm install -D ionic cordova
```

This will add **Ionic/Cordova** to your `devDependencies`
```js
// package.json

"devDependencies": {
    "cordova": "^8.1.1",
    "ionic": "^5.2.3",
},

```

To call it, I utilise **npm script**
```js
// package.json

"scripts": {
    ...
    "ionic": "ionic", // add ionic
    "cordova": "cordova" // add cordova
},
```

## 3. Specify build.json

**Cordova** build can be configured by specifying the build config. This is also related with the **Ionic/Cordova** version, mainly on iOS to make **Xcode** run on legacy build system as well as specifying the profisioning profile that was set and configured using `fastlane match`.

Sample build config
```js
{
    "ios": {
        "debug": {
            "codeSignIdentity": "iPhone Developer",
            "developmentTeam": "Team_ID",
            "provisioningProfile":"Profisioning_Profile_ID",
            "packageType": "development",
            "automaticProvisioning": false,
            "buildFlag": [
                "-UseModernBuildSystem=0"
            ]
        },
        "release": {
            "codeSignIdentity": "iPhone Developer",
            "developmentTeam": "Team_ID",
            "provisioningProfile":"Profisioning_Profile_ID",
            "packageType": "app-store",
            "automaticProvisioning": false,
            "buildFlag": [
                "-UseModernBuildSystem=0"
            ]
        }
    }
}
```

## 4. Use npm script to split build process

To utilise locally installed **Ionic/Cordova** I wrote a script to ensure that it use the right **Ionic/Cordova** version. The script also split into several steps. Basically when running **Ionic** to build it run 2 steps. 
1. Running `ionic-app-script`
2. Running `cordova build`
`cordova build` itself are actually a command that run `cordova prepare` followed by `cordova compile`

Using script I can choose which steps I want to perform and link it as I need.

```js
// package.json
"script":{
    "ionic:build:ios": "MY_ENV=prod ionic-app-scripts build --target cordova --platform ios",
    "cordova:prepare:ios": "npm run cordova prepare ios",
    "fastlane:build:ios": "bundle exec fastlane ios build_store",
    "build:ios":"npm run ionic:build:ios && npm run cordova:prepare:ios -- --prod && npm run fastlane:build:ios",
}
```

> **ps**: you can definitely configure this using `npm-run-all` package or `npx`

Using **npm script** also give me flexibility to split the build process. This helps me use native build instead of **Cordova** build as well as using tools such as `fastlane`. This also beneficial when using **CI/CD** tools.


## 5. CI/CD

Integrating **CI/CD** tools on this project proven a hassle. It's not straightforward due to specific **Cordova** version. The **CI/CD** workflow was changed to run the script instead of default build, then it chained the process to use `fastlane`. Utilising CI/CD tools such as **Bitrise** also help, especially to debug workflow by using their CLI tools and specifying `bitrise.yml` file. It makes debugging faster because the workflow run on the local machine, further this file can also be shared with other people in the team. Since the `platform` folder are committed, my `bitrise.yml` also become simpler.

Sample `bitrise.yml`
```yaml
format_version: "8"
default_step_lib_source: https://github.com/bitrise-io/bitrise-steplib.git
project_type: ionic
app:
  envs:
  - FASTLANE_XCODE_LIST_TIMEOUT: "120"
  - FASTLANE_WORK_DIR: .
  - FASTLANE_LANE: ios upload_testflight
trigger_map:
- push_branch: '*'
  workflow: primary
- pull_request_source_branch: '*'
  workflow: primary
workflows:
  primary:
    steps:
    - activate-ssh-key@4.0.3:
        run_if: '{{getenv "SSH_RSA_PRIVATE_KEY" | ne ""}}'
    - git-clone@4.0.14: {}
    - script@1.1.5:
        title: Do anything with Script step
    - fastlane@2.4.0:
        inputs:
        - lane: $FASTLANE_LANE
        - work_dir: $FASTLANE_WORK_DIR

```

---

By the end of the day, I am not satisfied with the project, really. It's a hassle, and required a lot of workaround. The good things, now I am more comfortable mixing different tools to automate app build and using **CI/CD**.


Will I ever want to do this again? Definitely no, I still think **Ionic** sucks, and any cross platform solution should be avoided if possible. It's not fun to maintain such system in the long run.
