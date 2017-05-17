---
layout: post
title:  "Curious Case Of CoreData"
date:   2016-06-21 15:24:18 +0800
categories: ios
---
Recently I found an interesting bug on my app. Whenever I pass an object which containt `NSManagedObject` subclass, at one point of time it will disappear from the memory. I was frustrated and naively change my implementation by passing the unique parameter of NSManagedObject subclass and fetch it from CoreData whenever it disappear. I was happy, things are working well, there was an increase of memory usage but everything run smoothly.

Yesterday I found the same issue again and finally able to uncover amusing mistery.

Aparrantely since `NSManagedObject` depend on `NSManagedObjectContext`, without the context you can't do any, and since the context and threading doesn't run well together, whenever the thread of context creation is killed by **CoreData**, the context disappear and your NSManagedObject will fault.

I believe it's my implementation default on multi threading on **CoreData** but at least now I know why and how to solve the issue. By ensuring your thread is still active and long live, you should have no issue with `NSManagedObjectContext`. Now I make sure I only use 2 different context, read and update, which is good enough for my apps.

Would love to explore more about multi threading on **CoreData**, perhaps there are more intersting stuff I can dig along. It's an interesting time to live as mobile dev.

Till then,
Ciaosz
