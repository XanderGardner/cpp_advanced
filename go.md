# GO Basics

basics
- [outline](#outline)
- [variables](#variables)
- [control](#control)
- [functions](#functions)
- [io](#io)

ds
- [struct](#struct)
- [string](#string)
- [array](#array)
- [slice](#slice)
- [map](#map)

algos
- [sort](#sort)

systems
- [OOP](#oop)
- [go routines](#go-routines)

experiment
- GO Playground: https://go.dev/play/
- Go standard library: https://pkg.go.dev/std

## outline
- designed for large distributed systems
- run with `go run filename.go`
```go
package main

// import packages
import (
  "fmt"
)

func main() {
  fmt.Println("Hello")
}
```

## variables
- assignments (go will only compile if all variables are used)
- types are `int`, `bool`, `float32`, `string`, `error`
```go
var a int = 3
var b = 2
c := 1
var d int // default is 0
var e, f int = -1, -2 // assign multiple
```

## control
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

for i, c := range s { } // loop over items in string
for i, item := range a { } // loop over items in array
for key, value := range myMap { } // loop over map items
```

## functions
```go
func f(a int, b int) int {
  return a + b
}

// both a and b are int types
func f(a, b int) (int,int) { 
  return a, b
}

// function that returns a (function that returns an int)
func example() func() int {
  var x int
  return func() int {
    x++
    return x*x
  }
}
```

## io

- files `import "os"`
``` go
// create file
file, err := os.Open("file.go") // read access
if err != nil {
  log.Fatal(err)
}

// read file all at once
data := make([]byte, 0)
count, err := file.Read(data)
if err != nil {
  log.Fatal(err)
}

// close file
file.Close()

```

- reading files `import bufio`
```go

// line by line
scanner := bufio.NewScanner(file)
for scanner.Scan() { // scans to "\n"
    scanner.Text() // retrieves current line
}
if scanner.Err() != nil {
    fmt.Println(scanner.Err())
}

// word by word
scanner := bufio.NewScanner(file)
scanner.Split(bufio.ScanWords) // use to scan to spaces
for scanner.Scan() {
  scanner.Text() // retrieves current word
}
if scanner.Err() != nil {
  fmt.Println(scanner.Err())
}

```

## struct

```go
// define
type Person struct {
  Name string
  Age int
}

// create instance
a := Person{
  Name: "John",
  Age: 30,
}

// access
a.Name
```


## string
```go
// import "strings"

// create string
s := "hiTHERE"
s := string(byte_slice) // create string from []byte type
s := strconv.Itoa(123) // string from integer "123"

// access
len(s)
s[3]
s[3:5]

// modify
a := strings.ToLower(s) // lower case
a := strings.Split(s, ",") // split into array of strings
a := strings.Fields(s) // splits by white space
s := strings.Join(a, ", ") // joins array of strings
```

## array
- fixed space
```go
// create array of size 8
a := []int{1,2,3,4,5,6,7,8}

// 
```

## slice

```go
// create slice of size 3
a := make([]string, 3)


// append O(1)
a = append(a,"tom")


```

## map
```go
// create map: string->int
a := make(map[string]int)

// access
value, exists := m[key] // check
a["strkey"] = 1 // assign

// remove
delete(a,"strkey")

```


## sort
- `import "sort"`
```go

sort.Ints(numbers) # sorts array of ints
sort.Strings(words) # sorts array of strings
sort.Float64s(numbers) # sorts array of float64s

// custom sort
sort.Slice(names, func(i, j int) bool {
  return names[i] < names[j]
})
```


## OOP
```go
// define a struct (acts as a contructor)
type Person struct {
    FirstName string
    LastName  string
    Age       int
}


// create a method for Person
func (p *Person) FullName() string {
    return p.FirstName + " " + p.LastName
}

// note that without the pointer, p is a coppy
func (p Person) FullName() string {
    return p.FirstName + " " + p.LastName
}


// create instance
func main() {
  
  person := Person{
      FirstName: "John",
      LastName:  "Doe",
      Age:       30,
  }
  fullName := person.FullName()

}
```


# go routines
```go
// use go keyword
func goroutines() {
  for i:= 0; i< 10; i++ {
    go fmt.Printf("go rountine")
  }
  fmt.Println("launched")
}

```

- channels (unbuffered)
```go
// makes an int channel which can hold one int
ch := make(chan int)

// send value to channel (which blocks until someone consumes from the channel)
ch <- i*i

// receive value from a channel (which blocks until someone sends to the channel)
value := <-ch
value, ok := <-ch // ok indicates if the channel is still open

// close channel
close(ch)

// function that takes channel (can send or receive)
func sumWorker(ch chan int) { }

// function that takes channel which can only send ints
func sendData(ch chan<- int, data int) {
    ch <- data
}
sendData(ch,42)

// function that takes channel that can only be read from
func receiveData(ch <-chan int) int {
    return <-ch
}
receiveData(ch)

// loop over channel, which continues until the channel is empty and closed
for item := range ch { }
```

- channels (buffered)
- only blocks sending when channel is full
- only blocks receiving when channel is empty
```go
// makes an int channel that can hold 3 elements
ch2 := make(chan int, 3)

// can send multiple ints
ch <- 1
ch <- 2
ch <- 3
```
