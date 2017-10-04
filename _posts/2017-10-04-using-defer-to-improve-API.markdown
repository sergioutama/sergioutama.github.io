---
layout: post
title: "Using defer to redoce your API code"
author: Sergio Utama
date:   2017-10-04 21:20:18 +0800
categories: ios
---

Making a network request is a common operation that you'll do as iOS developer. You will notice that there are a lot of stuff that happening there, from preparing your request, handling the response, checking status code, check for error, check for avaialable data, etc.

Here some common network request

```
func requestProducts(completion:@escaping ([String:Any], Error?)->Void){

    let session = URLSession(configuration: .default)
    let baseURL = URL(string: "https://api.yourservice.com/v1/getsomething")!
    var request = URLRequest(url: baseURL)

    request.setValue("application/json", forHTTPHeaderField: "Accept")
    request.setValue("application/json", forHTTPHeaderField: "Content-Type")
    request.httpMethod = "GET"

    session.dataTask(with: request) { (data, response, error) in
        if let error = error {
            completion([:],error)
            return
        }

        if let httpResponse = response as? HTTPURLResponse {
            let statusCode = httpResponse.statusCode
            if statusCode > 400  {
                let clientError = NSError(domain: "mydomain", code: statusCode, userInfo:[NSLocalizedDescriptionKey:"Request Error"])
                completion([:],clientError)
                return
            }
        }

        guard let data = data else {
            completion([:],nil)
            return
        }

        do {
            guard let responseObject = try JSONSerialization.jsonObject(with: data, options: .allowFragments) as? [String:Any] else {
                completion([:],nil)
                return
            }

            completion(responseObject,nil)

        } catch let serializationError {
            completion([:],serializationError)
        }



    }.resume()

}
```

Notice that you will need to handle multiple possible response and there are a lot of redundant code which is smelly. One of the easiest way to remove the smelly code is by using `defer`



