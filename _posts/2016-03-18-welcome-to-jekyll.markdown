---
layout: post
title:  "Switching rootViewController"
date:   2016-03-18 15:24:18 +0800
categories: ios
---
When developing iOS app, there are often case that you want to display an onboarding or login page before even displaying the main app flow. The most common way to achieve this result is by setting your `window.rootViewController` on `AppDelegate` based on parameters you set. However, it's not the only way.

##1. Switching rootViewController
Switch view controller
Caveat :
- Dirty flow

##2. Presenting ViewController
Present view controller normally
Caveat : 
- glitch when displaying the first view controller 
- might cause error warning the view controller displayed without visible view

##3. ViewController containment
Swtich using viewcontroller containment
ex: CLHoppingViewController
Caveat : 
- slow

ref :
- http://stackoverflow.com/questions/15287678/warning-attempt-to-present-viewcontroller-whose-view-is-not-in-the-window-hiera
- http://stackoverflow.com/questions/28379327/ios-warning-attempt-to-present-viewcontroller-whose-view-is-not-in-the-window
- http://stackoverflow.com/questions/19962276/best-practices-for-storyboard-login-screen-handling-clearing-of-data-upon-logou
