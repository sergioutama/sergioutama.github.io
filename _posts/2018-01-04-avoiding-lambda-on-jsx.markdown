---
layout: post
title:  "Avoiding Lambda on JSX"
author: Sergio Utama
date:   2018-01-04 15:40:18 +0800
categories: general
comments: true
---

When you write your React/ReactNative code for the first time, there are quite a number of tutorial that use lambda or arrow function within JSX.
It's convenience, it is easy, and you don't need to worry about `this`.

However, this practice can be considered bad and affect performance.
The reason behind it is due to how `render` function get called in React and the nature of lambda itself.

React component by default will re-render whenever its `state` changed.
Therefore, recreating the lambda every single time it render and put previous function into garbage collection.

There are 2 general solution for this problem.

### 1. Bind the method in constructor

```
class AwesomeComponent extends Component {
    constructor(){
        super()
        this.doSomething = this.doSomething.bind(this)
    }

    doSomething(){
        // whatever you want to do here
    }

    render(){
        return(
            <TouchableOpacity onPress={this.doSomething}>
                <Text>Press Me</Text>
            </TouchableOpacity>
        )
    }

}
```

### 2. Define your arrow function as a class property

```
class AwesomeComponent extends Component {
    constructor(){
        super()
    }

    doSomething = ()=>{
        // fill me in
    }

    render(){
        return(
           <TouchableOpacity onPress={this.doSomething}>
            <Text>Press Me Again</Text>
           </TouchableOpacity>
        )
    }
}

```

Quite easy solution that can improve your React/ReactNative performance.
