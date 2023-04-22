---
title: "Golang cheatsheet"
date: 2023-04-01T21:52:15+05:30
draft: false
tags: ["go","golang","cheatsheet"]
categories: ["cheetsheet"]
---

# Golang cheetsheet

## Hello world

- main method needs to go in 'main' package \
- We have to import package we need to use \
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


