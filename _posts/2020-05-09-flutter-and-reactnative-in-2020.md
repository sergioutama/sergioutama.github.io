---
layout: post
title: Flutter and ReactNative in 2020
author: Sergio Utama
date: 2020-05-09 17:23 +0800
categories: blog
tags: ['ios','android','flutter','reactnative']
---

My first encounter with Flutter was in 2018 when I started doing ReactNative more extensively (I learnt a bit ReactNative in 2016 and hate it, lol). I have a basic as native mobile developer therefor ReactNative makes more sense for me that time because if anything goes wrong, I can always make do with building it natively using Swift, Objective-C, Java, or Kotlin.

ReactNative also make sense that time because it’s based on popular React framework and it’s using JavasScript. It allow me to switch back and forth between mobile dev and web dev as I gain proficiency.

These few days I pick up Flutter again and here some of my thoughts about it. PS: I still haven’t dig extensively to Flutter (need to find a new flutter project, anyone want to pass me some?) so my knowledge is limited to what I experienced. It might be skewed and bias.

---

### 1. Flutter is way better than RN in UI, Animation, and Gesture

Performance wise on its basic form both Flutter and RN is good enough. However, once it goes into UI, animation, and gesture, RN start to slow down. Flutter on the other hand perform very good. Flutter has widgets that taking care of gesture for you, it also has better API design, it makes it easy to implement gesture based animation on Flutter.

RN will need to install few 3rd party libraries to deal with animation and gesture. react-native-reanimated and react-native-gesture-handler are some of the library I am using to achieve what plain Flutter can do.

### 2. Flutter is easier to setup compared with RN

Flutter is relatively easier to setup. It’s straight forward and there is no need to worry about other tools and dependency, what you need is just Dart and Flutter SDK. I still recall the first time I encounter RN there is Expo, there is Yarn there is NPM. It’s a little bit too much information and configuration just for a basic setup.
RN of course already improved so much however the flexibility of JS development and the confusion around it carries over. Babel, Metro, EsLint, Flow, etc.

### 3. Flutter now can be integrated to existing native app

This is one of the reason why 2 years ago I hesitate to go with Flutter because RN has better integration with native so I can mix and match and replace the component easier if I decide to ditch RN and go full native or vice versa.

Right now Flutter can support integration with native app on Activity/ViewController level.

This is important personally for me because I can’t risk to be chained with these tools either Flutter or RN. Apple and Google keep adding new features and improvement to existing native SDK which can only be accessed if you have direct native integration. I don’t want to be on mercy of Flutter or RN to wait until they integrate the feature that I want.

### 4. RN has more tools and larger community

RN has advantage of reusing tools from JS and React. Become the earlier player in the market there are many tools available that can be used with RN ecosystem. There are many tools to debug your code and inspect your application.

Being RN developer you can learn from the React community on how to do certain things. Your knowledge on React can be carried over to RN and vice versa. Flutter can do something similar with Flutter Web but the adoption rate of Flutter web is less than React. It’s easy to see that RN has advantage because it comes from web to mobile, while Flutter comes from mobile to web.

---

Now beside those points, what I haven’t try is optimization.

When you do Flutter, well, you only do Flutter. There are less chances you encounter bugs and fix the undelying native module, that is just how Flutter works.
This is where I suffer the most on RN. Not only I need to fix the JS code but also the native code. Integrating 1 RN library means maintaining 3–5 code base and that is a painful experience especially when deadline is approaching.

I hope to dig a bit more to get a better sense of Flutter development.

In terms of career when you learn Flutter, you stuck with Dart and Flutter. In this case learning RN give advantage of portability and flexibility of JavaScript and React. You can carry your JS knowledge to almost any part of development, wether it’s web or backend, or even microcontrollers.

Therefor, if you want to be versatile and perhaps want to be a more fullstack dev, RN is a better choice because of React and JS, however if you want to be a dev with expertise on mobile, Flutter is the better option.

Cheers