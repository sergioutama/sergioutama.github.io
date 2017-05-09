---
layout: post
title:  "Rescued By Protocol"
author: Sergio Utama
date:   2016-05-04 15:24:18 +0800
categories: ios
---
When Apple introduced swift couple of years back, they introduced it as **Protocol Oriented Language** and never I thought I will one day feeling grateful to protocol.

I recently had a project where I need to combine 2 different arrays which containts different objects as data source for my UICollectionView. Unfortunately for me, Swift does not allow two different array which contain two different objects to be combined (god bless Objective-C). 

Ex: 
``` swift
    var array1 = [1,2,3]
    var array2 = ["some","random","string"]
```

I knew I can work around by casting the array into `[AnyObject]`, however this might cause the issue during runtime and I need to do multiple checking just to ensure the object is the correct one. This is where **Protocol** come into play. Since the objects within the array has no similarity at all, I create a protocol that save common variables that I need to display UICollectionViewCell correctly.

Now I make my model object conform to the protocol, and whoilaa, it works. I can swap and add or replace my model object, as long as it conform to the protocol.

I still have some issue on how to make it more reusable, perhaps using **Generic**, but that is topic for another post.

Ciaosz!