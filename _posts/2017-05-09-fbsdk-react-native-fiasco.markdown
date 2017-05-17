---
layout: post
title:  "FBSDK React-Native Fiasco"
date:   2017-05-09 17:24:18 +0800
categories: ios
---

Recently I've been playing around with **react-native** and wanted to implement facebook login.
It should be easy, isn't it. React-native is a framework developed by facebook and facebook has a nice guide how to implement facebook login within react-native.

However, I found some issues during installation.

- `react-native run-ios` will always produce compilation error in some part of its dependency
- the app will start to mentioning that the view doesn't have certain `propTypes`

I was trying to debug the issue, finding my way over stackoverflow, documentations, github, etc to no avail
I ended recreate a new plain react-native app, and add the dependency one by one and try. Spending half of my day gone, I finally found the real culprit.

While following instruction on integrating react-native and facebook sdk. It relly heavily on `ios_setup.js`. This script should download the SDKs, extract it, configure the search path, and other configuration in **plist**, and you will expect it to **just works**. The script works, however there is one particular issue. the SDKs file that the script should download actually corrupted (I am not sure how, but it's corrupt). This could've been avoided if the script check the file MD5 or simple check wether the file successfully unzipped is great as well.

So the next time you tried integrating facebookSDK in your raect-native app don't forget to check the downoaded frameworks by the script, maybe, that's the cause of your headache.
