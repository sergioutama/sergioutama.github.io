---
layout: post
title:  "A bug at DahMakan iOS App"
author: Sergio Utama
date:   2018-05-24 16:24:18 +0800
categories: ios
comments: true
---

DahMakan is a startup that provide and deliver exclusively made food to your doorstep. You can order from their app and i've been using it couple of times. Today on their recent release for iOS (v 30.0) I found a bug.

Here is how to reproduce:

1. Order few food
2. Open cart
3. Remove item in cart one by one
4. Upon finish the app will display that you don't have item in cart
5. It crash


Let's assume and try to figure out why this bug exist.

The app only show cart screen if you already add an item into cart. There is no other action which will triger cart screen to display. Upon displaying the cart, there is a loading screen. Based on this, I assume the app is fetching data from server. This is common on e-commerce app to ensure the data as valid and consistent. Everytime i remove the item from cart, the cart screen is loading and reset its state and content.

aparently i cannot replicate for the scond time