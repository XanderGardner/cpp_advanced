# GO Basics

- GO Playground: https://go.dev/play/
- Go standard library: https://pkg.go.dev/std

## Outline
- designed for large distributed systems
```go
package main

import "fmt" // format package

func main() {
	fmt.Println("Hello")
}
```

## Variables
- assignments (go will only compile if all variables are used)
- types are `int`, `bool`, `float32`
```go
var a int = 3
var b = 2
c := 1
var d int // default is 0
var e, f int = -1, -2 // assign multiple
```

## Loops
- supports `break` and `continue`
```go
// for loop
for i := 1; i <= 3; i++ {
  fmt.Println(i)
}

// while loop
i := 1
for i <= 10 {
  fmt.Println(i)
  i++
}

// break outerloop
Outerloop:
for i:=0; i<3 ; i++ {
  break Outerloop
}
```

## Functions
-
```go
func f(a int, b int) int {
  return a + b
}

func f(a, b int) (int,int) { // both a and b are int types
  return a, b
}
```
