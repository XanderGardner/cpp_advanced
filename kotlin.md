# Kotlin for Competitive Programming

Basics
- [read input](#read-input)
- [exceptions](#exceptions)
- [random](#random)
- [math](#math)
- [casting](#casting)

Basic Data Types
- [Boolean](#boolean)
- [Int](#int)
- [Double](#double)
- [Char](#char)
- [String](#string)

Collections
- [Array](#array)
- [ArrayList](#arraylist)
- [Pair](#pair)
- [Triple](#triple)
- [ArrayDeque](#arraydeque)

More Collections
- [PriorityQueue](#priorityqueue)
- [Set](#set)
- [Map](#map)

Functional
- [conditional expressions](#conditional-expressions)
- [functions and lambdas](#functions-and-lambdas)
- [iterating over](#iterating-over)

Advanced Uses
- [lambdas with receivers](#lambdas-with-receivers)
- [scope functions](#scope-functions)

# read input

```kotlin
// read one line
val name: String? = readLine()

// read one line as int
val age: Int? = readLine()?.toIntOrNull()

// read single line of ints
val numbers: List<Int>? = readLine()
        ?.split(" ")
        ?.mapNotNull { it.toIntOrNull() }
```

# exceptions

```kotlin
throw IllegalArgumentException("Number must be non-negative")
// IllegalArgumentException
// IllegalStateException
// NullPointerException
// NumberFormatException
// ArrayIndexOutOfBoundsException
// ArithmeticException
// ClassCastException
// IOException
// FileNotFoundException
// ConcurrentModificationException

// custom exception
class CustomException(message: String) : Exception(message)
fun main() {
  throw CustomException("Value cannot be greater than 5")
}

// handling exceptions
try {
  val number = susFunction()
} catch (e: IllegalArgumentException) {
  println("Caught an exception: ${e.message}")
} finally {
  println("Execution completed.")
}
```

# random

```kotlin
import kotlin.random.Random

// random int in range [x,y)
val a = Random.nextInt(1, 11) 

// random double in range  [x,y)
val a = Random.nextDouble(1.0, 10.0)

// random item from list
val a = list.random()
```

# math
```kotlin
maxOf(a,b)
minOf(a,b)
```

# casting

- smart casting will change the type to not be nullable
```kotlin
val s: String? = null
if (s != null) {
    println(s.toUpperCase()) // s is of type String here
}
```

# Boolean

```kotlin
// assign
var a: Boolean = true // false

// operations
a && b
b || c
!d

// equality
a == b // common structureal equality
a != b
a === b // reference equality
```

# Int

```kotlin
// assign
var a: Int = 43

// min and max values
val a = Int.MAX_VALUE
val b = Int.MIN_VALUE
```

# Double

```kotlin
// assign
val a: Double = 3.14159

// might also take on special values
val a = Double.POSITIVE_INFINITY
val a = Double.NEGATIVE_INFINITY
val a = Double.NaN

// round down to int
val b = value.toInt()

// round to int
val b = value.roundToInt()

// round for printing
val s = String.format("%.2f", a)
```

# Char

```kotlin
// assign
val a: Char = 'a'

// check type of char
a.isLetter()
a.isDigit()
a.isWhitespace() // true for \n

// convert to upper
val b = a.toUpperCase()
val b = a.toLowerCase()

// get ascii code of character
val c: Int = a.code

// cast
val num = a.toInt()
```

# String

- immutable array of unicode characters
- any modification creates a new string
```kotlin
// basics
val a: String = "asbds"
a[2]
a += "sdfss" // O(n)
"s" in a
"df" in a
a.length

// split based on char
val a = c.split(",")

// replace occurances
val s = c.replace(" ","")

// cast
val num = str.toInt()
val num = str.toIntOrNull()
```
- O(1) append required stringbuilder
```kotlin
// create
val a = StringBuilder("hi")

// append
a.append("dude")

// pop/remove
sb.delete(sb.length - 1, sb.length) // pop
sb.delete(sb.length - 3, sb.length)

// output to string
val s = a.toString()
```

# Array
- mutable
- fixed size
- concrete class
```kotlin
// create
val a: Array<Int> = arrayOf(1, 2, 3, 4, 5) // explicit

// access
a[2]
a[2] = 5

// length
val l = a.size

// sorting
a.sort() // inplace
a.sortDescending()
// custom sorting for Pairs
array.sortWith { a, b -> 
  val result = a.second.compareTo(b.second)
  if (result == 0) {
      a.first.compareTo(b.first)
  } else {
      result
  }
}
```
- avoid overhead of boxing primitives
```kotlin
// create
val a: IntArray = intArrayOf(5, 10, 15, 20)
val a: DoubleArray = doubleArrayOf(5.0, 10.0, 15.0, 20.0)

val a = IntArray(2) // size 2, 0's

```

# ArrayList
- `MutableList` implements the `List` and provides mutability
- variable size
- interface which extends List
- implementations of this interface inlude:
  - `ArrayList`
  - `LinkedList`
```kotlin
// create
val a = ArrayList<Int>()
val a: ArrayList<Int> = arrayListOf(1, 2, 3, 4, 5)

// access
a[2]
a[2] = 5

// append
a += 4 // .add(4)
a += c // .addAll(c)

// length
val l = a.size

// cast
a.toIntArray() // to IntArray

// sorting
a.sort() // inplace
a.sortDescending()
// custom sorting for Pairs
array.sortWith { a, b -> 
  val result = a.second.compareTo(b.second)
  if (result == 0) {
      a.first.compareTo(b.first)
  } else {
      result
  }
}
```
- 2d arrays
```kotlin
val a = Array(numrows) { IntArray(numcols) }
```

# Pair
- immutable
```kotlin
// create
val a: Pair<Int, String> = Pair(1, "one")

// get
val first = a.first
val second = a.second
```

# Triple
- immutable
```kotlin
// create
val a: Triple<Int, String, Double> = Triple(1, "one", 1.0)

// get
val first = a.first
val second = a.second
val third = a.third
```

# ArrayDeque
- stack and queue
- (first/left end) [0,1,2,3,4] (last/right end)
```kotlin
// create
val a: ArrayDeque<Int> = ArrayDeque()

// right end (as stack)
a.addLast(1)
a.removeLast()
a.last() // peek
a.lastOrNull()

// left end
a.addFirst(0)
a.removeFirst()
a.first() // peek
a.firstOrNull()

// size
a.size
a.isEmpty()
a.isNotEmpty()

// (as queue)
a.addLast(1)
a.removeFirst()
```

# PriorityQueue
- from java standard library
```kotlin
// import
import java.util.PriorityQueue

// create (min heap by default)
val a = PriorityQueue<Int>()

// add
a.add(5)

// pop
val b: Int = a.poll()

// size
a.size
a.isEmpty()
a.isNotEmpty()

// custom priority
// (since comparator is a functional interface, we use a lambda)
val pairComparator: Comparator<Pair<Int, String>> = Comparator<Pair<Int, String>> { pair1, pair2 ->
        ...
    }
val a = PriorityQueue<Pair<Int, String>>(pairComparator)
```

# Set
- `MutableSet` extends `Set` by making it mutable
- implementations are `HashSet`, `LinkedHashSet`, and `TreeSet`
```kotlin
import java.util.HashSet
import java.util.LinkedHashSet
import java.util.TreeSet

// create
val a = HashSet<Int>() // hashmap
val a = LinkedHashSet<Int>()  // maintains insertion order
val a = TreeSet<Int>() // red black tree

val a = hashSetOf(1,2,3)
val a = linkedHashSetOf(1,2,3)
val a = treeSetOf(1,2,3)

// add O(logn)
a.add(3)

// remove O(logn)
a.remove(3)

// contains O(logn)
a.contains(3)

// traversal O(n)
for (item in a) { ... } // ordered

// add first/last O(1)
a.first()
a.last()

// size
a.size
```

# Map
- `MutableMap` extends `Map` by making it mutable
- implementations are `HashMap`, `LinkedHashMap`, and `TreeMap`
```kotlin
import java.util.HashMap
import java.util.LinkedHashMap
import java.util.TreeMap

// create
val a = HashMap<String, Int>() // hashmap
val a = LinkedHashMap<String, Int>() // maintains insertion order
val a = TreeMap<String, Int>() // red black tree

// set
a["one"] = 1

// access
a["two"]
```



# conditional expressions

- one line
```kotlin
val answerString = if (count == 42) {
    "I have the answer."
} else if (count > 35) {
    "The answer is close."
} else {
    "The answer eludes me."
}
```

- when statement
```kotlin
val answerString = when {
    count == 42 -> "I have the answer."
    count > 35 -> "The answer is close."
    else -> "The answer eludes me."
}
```

# functions and lambdas

- lambdas: functions
```kotlin
// lambda
val add: (Int, Int) -> Int = { x, y -> x + y }
val add: (Int) -> Int = { it + it } // it when one param

// anonymous function without return
val add = fun(x: Int, y: Int): Int = x + y

// anonymous function with return
val add = fun(a: Int, b: Int): Int { return a + b }

// functions as input
stringMapper("Android", { input ->
    input.length
})
// if a function is the last parameter it is equivalent to:
stringMapper("Android") { input ->
    input.length
}
```

- lambdas: functional interfaces
- provides a way to (1) implement an interface (2) override the single abstrct function (3) get an instance of the implementation
```kotlin
// while you could do something like this ...
class CustomComparator : Comparator<String> {
    override fun compare(s1: String, s2: String): Int {
        ... return ...
    }
}
val cc: Comparator<String> = CustomComparator()

// ... since  Comparator is a functional interface (has one abstract method) ...
@FunctionalInterface
public interface Comparator<T> {
    int compare(T o1, T o2);
}

// ... you can simplify to implementing the interface
// and overriding the single abstract function
// and getting an instance of that
// in a lambda ...
val cc: Comparator<String> = Comparator<String> { s1, s2 -> ... }


```

# iterating over
- general iteration
```kotlin
for (i in 1 until 10) { ... }
for (i in 1 until 10 step 2) { ... }
for (i in 10 downTo 1) { ... }
for (i in 10 downTo 1 step 2) { ... }
```
- for Array, List, and MutableList
```kotlin
for (item in a) { ... }
for (i in a.indices) { ... }
a.forEach( item -> ... )
a.forEachIndexed { index, item -> ... }
```

# lambdas with receivers

- An extension function is a function defined outside of a class that extends the class’s functionality
```kotlin
// create extension function on String
fun String.a(): String {
    return this + "!"
}

// use extension function
"Hello".a() // Hello!
```

- A receiver is the object on which an extension function operates, in this case "Hello"
- Note every class implicitly has a receiver type of ClassName.()
- A "lambda with receiver" defines operations to perform on an object type. This is a special kind of lambda and the lambda does not take an input "it" but rather has reference to "this" with no input parameter
```kotlin
// create lambda with receiver for StringBuilder
val a: StringBuilder.() -> Unit = {
    append("!") // implicit use of this.append()
}

// use lambda with receiver
StringBuilder("hi").apply(a).toString()
```

- Combining extension functions and lambdas with receivers
```kotlin
// create extension function with lambda with receiver
fun StringBuilder.extFunc(lambRec: StringBuilder.() -> Unit): String {
    this.lambRec()
    return this.toString()
}

// use
val out = StringBuilder().extFunc {
    append("!")
    append("World!")
}
```
- A common use of this is for DSL (domain specific languages)
```kotlin
data class Person(var name: String = "", var age: Int = 0)

fun person(block: Person.() -> Unit): Person {
    val person = Person()
    person.block() // Apply the lambda with receiver
    return person
}

val newPerson = person {
    name = "John Doe"
    age = 30
}
```

# scope functions
- used to perform operations on objects within a specific scope
- note the special input type of lambda with receiver which has no explicit input for the lambda
```kotlin
// -------- LAMBDA WITH RECEIVER --------

// APPLY
// used to configure an object
// input: lambda with receiver: T.() -> Unit
// output: receiver object: T
// object reference: this
val sb = StringBuilder().apply {
    append("Hello, ") // implicit this.append()
    append("World!")
}.toString()

// RUN
// perform operations on an object and return a result
// input: lambda with receiver: T.() -> R
// output: result of lambda: R
// object reference: this
val result = "Hello".run {
    this + " World!" // this refers to the receiver String
}

// WITH
// perform multiple operations on an object within a block and return a result
// input: 
    // receiver object: T
    // lambda with receiver: T.() -> R
// output: result of lambda: R
// object reference: this
val result = with(StringBuilder()) {
    append("Hello, ") // implicit this.append()
    append("World!")
    toString() // returns the final String
} 

// -------- OBJECT SCOPED --------

// ALSO
// perform additional actions on an object, typically for side-effects
// input: lambda that acts on receiver object: (T) -> Unit
// output: receiver object: T
val sb = StringBuilder().also {
    it.append("Hello, ")
    it.append("World!")
    println("Current content: ${it.toString()}")
}

// LET
// perform operations on the result of an expression and return a result
// input: lambda that acts on receiver object: (T) -> R
// output: result of lambda: R
val length = s?.let {
    it.length // executed if s is non-null
} ?: 0
```
