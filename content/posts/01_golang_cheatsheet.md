---
title: "Golang cheatsheet"
date: 2023-04-01T21:52:15+05:30
draft: false
tags: ["go","golang","cheatsheet"]
categories: ["cheatsheet"]
---

## Hello world

- main method needs to go in 'main' package 
- We have to import package we need to use 
- fmt is standard library

#### **`main.go`**
```go
package main

import (
	"fmt"
)

func main() {
  fmt.Println("hello world")
}
```

### To run this we can do 
- It compiles and runs the application

```bash
go run .
```


## Command line arguments

- Use os package to get command line args

```go
package main

import (
	"fmt"
    "os"
)

func main() {
  if len(os.Args) > 1 {
    fmt.Println("hello,",os.Args[1])
  } else {
    fmt.Println("hello, world!")
  }
}
```

## Basic types

int - size is equal to word size of machine
e.g. on my laptop 64 bit

In golang int is the default type for integers

For non integers -> float32 float64 complex64 complex128

For money, go has package like 'Go money'


## Special types

- bool -> false, true (can't convert to/from integers)
- error -> type with one function Error(), error maybe nil or non-nil
- Pointers -> Physical addresses, no pointer manipulation except package `unsafe`


## Initial values

Go initializes all vars to "zero"

- Numbers gets 0 (float 0.0, complex 0i)
- bool gets `false`
- string gets `""`
- everything gets `nil`

## Simple declarations

variable name first, then its type

```go
var a int // a will be assigned 0
```

Multiple declaration in same statement, go infers types.

```go
var (
  b = 2
  f = 2.01
)
```

Within a function, we can do a short declaration

```go
c := 2
```


## Print with formatting

go has verbs for formatting
- %s for strings
- %T for types
- %v for value of variable

```go
package main

import (
	"fmt"
)

func main() {
  a:=2

  // %T is verb for type
  // %v is verb for value
  fmt.Printf("a: %T %v\n",a,a) //a: int 2


  b:=3.1

  // with %8T, we can fix col length for this to format
  // with %[1]v, we can tell it to use paramter 1, which is 1
  // so we don't have to send it two times
  fmt.Printf("b: %8T %[1]v\n",b)

  // a = b 
  //assignment will fail, types are different

   //But we can do value conversion
  a = int(b)
}
```

## Strings

Types related to strings
- byte a synonym for uint8
- rune a synonym for int32
- string: immutable seq of characters
    * physically seq of bytes (uses UTF-8 encoding)
    * logically a sequence of (unicode) runes

Raw strings
```go
var a:=`string with "quotes"`
```

If a string has non ascii characters,  `len(s)` will return the number of bytes required to stored that string and not the number of characters in string


Strings are immutable

```go
s := "hello world"
hello := s[:5]
world :=[6:]
``` 

The variable s is kind of like pointers,it points to the memory location of string but it also keeps metadata like len of string.

`s`, `hello` and `world` variables are pointing to the same string (hello and world point to substring of s)

## Composite types

- string
- [4]int array
- []int slice (variable length array)
- map[string]int 