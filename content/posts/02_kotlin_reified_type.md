---
title: "Kotlin reified type"
date: 2023-05-16T22:53:10+05:30
draft: false
tags: ["kotlin","generics"]
---

# 1. Introduction

Generics in the JVM provide a powerful way to write reusable code that can operate on different types. However, due to type erasure, the actual type information is lost at runtime, limiting the capabilities of generic code. 

In this blog post, we'll know more about Kotlin's approach to tackling type erasure through the use of reified types. We'll explore how Kotlin's inline functions and reified types work together to preserve type information, leading to more flexible code.


# 2. Generics

Generics allows us to reuse code by defining and enforce type constraints in compile time. This removes the need for explicit type casting. 

Generics are represented by angle brackets (<>) and are used typically in collections and generic classes.

The type parameter inside angle brackets represents a placeholder for a specific type, which is determined when instance of class is created.


```java
// A generic class using generic type T
class Box<T>(var item: T) {
    fun getItem(): T {
        return item
    }
}

fun main() {
    // Creating an instance of Box with type Int
    // Kotlin has type inference, so we can omit the type parameter when creating instances 
    val integerBox = Box(10)

    // Creating an instance of Box with type String
    val stringBox = Box("Hello")

    // Retrieving the items from the boxes
    val intValue: Int = integerBox.getItem()
    val stringValue: String = stringBox.getItem()

    println("Integer value: $intValue")
    println("String value: $stringValue")
}
```

# 3. Type erasure

In Java, type erasure refers to the process by which generic type information is removed or erased during compilation. 

This means that the specific type arguments used for a generic class or method are not retained at runtime.
The type erasure mechanism was introduced to ensure backward compatibility with pre-generic versions of Java.

Let's create an instance of Box class defined above:

```java
Box<Integer> intBox = new Box<>(42);

Class<?> clazz = intBox.getItem().getClass(); // Won't return Integer.class
boolean isInteger = intBox.getItem() instanceof Integer; // Won't evaluate to true
```

At compile time, the Java compiler performs type erasure, removing the generic type information. So, at runtime, the variable intBox is treated as if it were just an instance of Box, without any information about the specific type T (in this case, Integer).

Both getClass() and instanceof will provide information about the erased type, which is Object in this case.


# 4. What if we want to implement some functionality using the class of generic parameter? 

To work around the limitations of type erasure, we can pass the class type explicitly or use reflection to access the generic type information indirectly. For example, we can modify the Box class to accept a Class<T> parameter:

```java
public class Box<T> {
    private T item;
    private Class<T> itemType;

    public Box(T item, Class<T> itemType) {
        this.item = item;
        this.itemType = itemType;
    }

    public T getItem() {
        return item;
    }

    public Class<T> getItemType() {
        return itemType;
    }
}
```


