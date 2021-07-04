---
layout: post
title: Spec First Development
date: 2021-07-04 22:57 +0800
author: Sergio Utama
categories: blog
tags: ['backend']

---
Lately I've been doing more backend than before and implementing Spec First Development.

Instead of jumping from user story / requirement directly into implementation, spec first development focus on developing a API specification. Developer focus on translating requirements into API specification the request and response of the API. This specification will be used a source of truth when developing the system regardless whether it's for frontend that will consume the API or backend that serve the API. 

Having API spec as contract help developer to focus on implementation that adhere to the spec rather than back and forth fine tuning the request/response during the development.

### The good

Personally there are 4 main benefits when I implement spec first development in my workflow

1. Single source of truth

API spec can be single source of truth for both frontend and backend developer. Since we treat the spec as a contract, developer (especially frontend) can rest assure that the response they get from the API will be following the spec. It's also relatively easy to generate a Postman collection to simulate the response from the API. Additionally it also make it easy to see a gap between data to be displayed in the UI and the API response. 

The spec can also be used by QA to generate smoke test or integration test. Thus reducing friction during integration or when backend ready to serve the API.


2. Frontend and backend development can run concurrently

This will be biggest benefit having spec first development. When both frontend and backend can be developed in parallel, it means reduced overall development speed. It also reduce the time needed to integrate both frontend and backend. This is because both frontend and backend follow the spec.

3. Freedom of implementation

Having API Spec defined early allow backend and frontend to have a freedom of implementation. Developer can write abstraction or having multiple services, it doesn't matter because by the end of the day as long as adhering to API spec, the API will works as intended.

4. Request and response can be validated

Another benefit of using spec first development is security. Security comes in form of request and response validation. There are many tools out there that can generate a request/response validation based on API spec. Thus, bugs or incorrect implementation can be detected early. Sensitive data leaked? As long as API spec does not define the response, you can also prevent this scenario.


### The hiccup

Implementing spec first development is not without it's drawbacks

1. Initial time to start development can be slow

It takes time to match requirements to a spec. The spec only work as good as how well defined it is based on the requirement. Ideally both backend, frontend, and other stakeholder should give input to the spec so it can be used as source of truth. This initial investment to refine spec might discourage people to implement it, however there are other way to speed up the process afterwards, by using generator for example. We can use tool to generate route, model, or even client request from the spec that we defined earlier. 

  
2. Changes to spec might still happen

Change is inevitable and spec first development won't be spare. Having spec first development doesn't mean there will be no changes after the api is specified. When changer happen, spec need to change, therefor there is a need to have API versioning ready. It is another investment, where backend need to implement API versioning, because API versioning usually comes quite late once API is solid and properly released. Mitigating a need to create API versioning, some kind of API gateway can be implemented, therefore removing responsibility to handle versioning from backend.

---

Regardless, the drawback it has, I believe spec first has more benefits and that's the reason why I defaulted to spec first development.

I've been on both side, as frontend developer that need to consume the API and backend dev that need to serve the API. Especially from frontend perspective, API changes is quite expensive, because it change data structure, changes in API might affect the how UI to be displayed, therefore it might also affect UX of the web or app.

Spec first development is not a holy grail, having a solid technical specification and well defined requirements often give more benefit. A full blown technical specification and requirements takes more time, and when it change (which inevitably will happen) it takes more time to update and redefine based on the changes. Thus I believe spec first development for my current workflow, give the best balance in terms of time to take to define the spec, the implementation, and adopting to changes in requirements 


ref: 
- [Atlassian blog in 2019](https://www.atlassian.com/blog/technology/spec-first-api-development).
