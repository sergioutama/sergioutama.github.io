---
layout: post
title:  "T&T: Improve react debug process"
author: Sergio Utama
date:   2018-05-24 15:24:18 +0800
categories: ios
comments: true
---

When I started using react/react-native i approach it from functional perspective, trying to make everything a function. This include when i try to render custom component. I will try to use  `functional stateless component (fsc)`.

```
const LoadingOverlay = (props)=>{

    return (
        <View>... and any other custom component here</View>
    )
}
```

Recently I change this to use `PureComponent`. The main reason for me doing this is not performance but readability and debug. Whenever I try to debug the component using `fsc` i will have difficulties looking for that component within DOM. However by using `React.createClass` or extending `React.Component / React.PureComponent` you can easily find or filter the component based on its class name. This will help you to traverse DOM and debug your custom component.


```
class LoadingOverlay extends React.Component {
    render(){
        return(
            <View>.... your content here</View>
        )
    }
}
```



