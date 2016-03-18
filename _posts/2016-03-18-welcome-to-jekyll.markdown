---
layout: post
title:  "Switching rootViewController"
date:   2016-03-18 15:24:18 +0800
categories: ios
---
When developing iOS app, there are often case that you want to display an onboarding or login page before even displaying the main app flow. The most common way to achieve this result is by setting your `window.rootViewController` on `AppDelegate` based on parameters you set.
