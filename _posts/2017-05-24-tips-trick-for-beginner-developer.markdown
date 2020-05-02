---
layout: post
title:  "6 Tips & Tricks for Beginner Developer"
author: Sergio Utama
date:   2017-05-24 11:33:18 +0800
categories: ios
---

I've been spending the last couple of months as mentor for iOS Developer bootcamp program at [NEXTAcademy](https://www.nextacademy.com/). Here are 6 advices, tips, tricks I told my students to improve their code.

## 1. Name things properly.

You are not only write code for the machine, but also for other developer to read. Especially if you are working in a team. The rule of thumb is, the name of your class, variable, or function, **should be self explanatory**. People who read, should understand what it does directly.

```swift
// Example
var name = "John"; // good variable name
var x = "Max" // what is x??

// Other example

var students : [Student] // using plural form
var student : [Student] // so 'student' is many students or ???
```

## 2. One function should only do one thing.

This is the basic of **Single Responsibility Principle**. One function should only do one thing and one thing only. It should self explanatory, function name should reflect what it does.

```swift
func displayAlert() {
  // write code that will only display alert here
}
```

## 3. Avoid side effect when using function.

When writing a function, quite often you will change the state or the value of an object which declared outside function declaration, perhaps a variable you declare in your class. This often called **side effect**. Ideally you want to avoid side effect as much as possible. You can write a function that accept parameter and return a new value.

```swift
// Example

func viewDidLoad(){
  super.viewDidLoad()

  students = studentsFromJSONArray(jsonArray);
}

// ...somewhere down in your code

func studentsFromJSONArray(_ JSONArray: [[String:Any]]) -> [Student] {
  // create your student objects here
}
```

## 4. Use extension to separate the logic or protocol implementation.

Extension in swift, is meant to add functionality to the code that you don't own. However, I also like to use it to separate my code logic, especially protocol implementation. The good thing about it, once you get used to separate your logic, you might starting to see a pattern in your code and you can refactor it easily if you want to.

```swift

class ViewController : UIViewController {
  // write logic specific of your ViewController here
}

extension ViewController: UITableViewDataSource {
  // write all protocol implementation of UITableViewDataSource or function related to it in extension
}

```

## 5. Separate business logic from your ViewController

**Modal View Controller (MVC)** pattern is the first architecture pattern you'll learn when building iOS application. It's great, however Apple tied the View and Controller together in UIViewController and its subclass. This without proper check can go out of control causing **Massive-View-Controller** instead. To solve this, I often take out my business logic to different class which is a plain object. I will end up with at least 2 classes : **ViewController** and **Controller**. ViewController only role is to accept input, pass it to Controller and displaying output. Therefor, your ViewController doesn't have any business logic at all. Your Controller is the one which has business logic, however, it doesn't have UIKit component at all, this will make your code more reusable.

```swift

// AuthViewController.swift
class AuthViewController: UIViewController {
  // UIViewController lifecycle, accepting input from view and displaying output
  // No business logic
}

// AuthController.swift
class AuthController {
  // only do business logic, no UI element
  func login(username: String, password: String, completion: (Bool, Error?) -> Swift.Void){
    //... implementation
  }
}
```

## 6. As vanilla as possible

I often encourage my students to be as vanilla as possible. It simply mean, do not include library if it's not required. Example, if you want to do simple network request, it's better to create a class by your own instead of using library such as `Alamofire`.

## Conclusion

Those are my personal favorites. It's easy to implement and will lead to a better code almost instantly. It doesn't change the structure too much so you can directly refactor your code.

I personally believe a better code is something readable. You'll need that readability if you work again on the codebase after couple of months. It helps on context switching.

Cheers
