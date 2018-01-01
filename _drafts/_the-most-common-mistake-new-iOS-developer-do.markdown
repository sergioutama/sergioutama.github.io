---
layout: post
title:  "The Most Common Mistake New iOS Dev Do"
author: Sergio Utama
date:   2017-06-27 21:20:18 +0800
categories: ios
---

Have you ever did this in your code?


``` swift

// ViewControllerA.swift

...

func displayNextViewController() {
  let nextController = NextViewController()
  present(nextController, animated:true, completion:nil)
}

...

// NextViewController.swift
...
func goBack(){
  dismissViewController(animated: true, completion:nil)
}
...

```
