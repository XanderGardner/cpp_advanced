
Basics
- [throw errors](#throw-errors)
- [primitive data types](#primitive-data-types)
- [object](#object)
- [array](#array)


# throw errors

```javascript
// throw an error
throw new Error("Cannot divide by zero");


// catch an error
try {
  const result = divide(10, 0);
} catch (error) {
  console.error("An error occurred:", error.message);
}
```

# primitive data types

```javascript
//////////// number //////
let a = 25;
// basic operations: +, -, *, /, %, ++, --, +=, <
Math.round(4.6); // 5
Math.floor(4.6); // 4
Math.ceil(4.2); // 5
Math.random(); // [0,1)
Math.pow(2,3); // 2^3


////// string ////// (immutable)
let s = "word";
let s = "word" + " " + "2"; // concat
s.length;
s.charAt(1); // get char at index
s.substring(0,5); // 0 to 4 inclusive


////// boolean //////
let b = true;

////// null //////
let s = null

////// undefined (uninitialized) //////
let x;

```

# object
```javascript
// constructor
let a = {
  b: "word",
  c: 25,
  d: true
};

// constructor from nothing
let a = new Object();

// dot notation
a.name = "word"; // add key
delete a.name; // delete key name

// bracket notation
a["name"] = "word"
delete a["name"]

if ("name" in a) { } // check if a.name key exists

// iterate
for (let key in a) {// over keys as strings
  a[key]
}

// get keys
let arraykeys = Object.keys(a)
Object.keys(a).length // number of keys
```


# array
```javascript
let a = ["a", "b", "c"];

a[0] = "a"; // set
let v = a[1]; // get

// as a stack
a.push("b");
let last = a.pop();

// check if exists
if (a.includes("b")) { }

// slice
let b = a.slice(1,3); // [a[1], a[2]]

// iterate
for (let val of a) { }
a.forEach(function (val) {

});
```



```javascript

```
