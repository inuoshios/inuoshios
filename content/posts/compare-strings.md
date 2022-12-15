+++
title = "String Comparison in Go"
date = "2022-10-20"
author = "Inu John"
cover = "img/gopher.jpg"
tags = ["golang", "strings", "go"]
description = "How to compare strings using the Go programming language."
+++

To check if two strings are equal in golang, you could simply do something like this:

```go
email := "email"
password := "password"

if strings.ToLower(email) == strings.ToLower(password) {
    // do something
}
```

What if there's an easier method?

Using the `strings.EqualFold()` makes it a lot easier to compare strings in Golang.

```go
email := "email"
password := "password"

if strings.EqualFold(email, password) {
    // do something
}
```
