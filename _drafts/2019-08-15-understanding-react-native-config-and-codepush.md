---
layout: post
title: Understanding react-native-config and codepush
date: 2019-08-15 13:14 +0800
---

One of the advantages of using ReactNative is the ability to share code between platform. The way ReactNative works is by bundling shared js code and load it natively during runtime. This opens up possibility to ship additional code after the app released to the store. Since what's needed is actually a bundled js code, the code itself can later be fetched or hosted at different location. Codepush is one of the tools that allow switching bundled js code required for ReactNative to operate.

Using Codepush is easy and for those who need a faster way to release app and skip Apple app review, you definitely want this. However, Codepush only limited to the changes on the javascript side. When there is a new native code being added, you will still need to submit your changes to AppStore / PlayStore. Further, it's a good practice to still release the app updates after using Codepush. Managing app versions solely based on Codepush can easily goes out of hand, especially when there are multiple builds, and you work on large scale application. Keep Codepush to release a quick fix.

Talking about large scale application on enterprise or even startup, we as developer often need to build different version of the app with slight different configuration. React-native-config is the exact tools that we can leverage to solve this problem. It allows defining `.env` file which bring http://12factor.net/config love to your mobile apps.