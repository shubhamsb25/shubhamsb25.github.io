---
title: "Effective java"
date: 2023-07-24T08:34:01+05:30
draft: false
tags: ["java","book review"]
---

# Review notes: Effective Java


## Item 1: Static factory methods

### Advantages

- We can't name constructors, but we use static factory methods have an advantage of them having names
- We can use these to cache, or give back pre constructed instances
- The can return any sub type of their return type adhering to program by interfaces. 
- We could change class of returned object based on some parameters, which decouples client from internal implementation.
- Class of returned object need not exist when method is written. This forms the basis for SERVICE PROVIDER FRAMEWORKS in which providers implement a service and system makes the implementations available to clients. Service provider framework has three components:
    - Service interface, represents implementation
    - Provider registration api
    - Service access api, used to get instance of service
    - (optional) service provider inteface, describes a factory object that produce instance of service interface.

### Limitations

- If we skip constructors altogether, we won't be able to create sub classes. In a way this is good as it promotes "Composition over inheritance"
- Static factory methods do no stand out in documentation, as opposed to constructors.