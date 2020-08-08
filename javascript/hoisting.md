# Hoisting

> **Hoisting** - order of execution. which lines executes firstly.

or

> **Hoisting** is when variable declarations and function declarations pop up to the top

```js

log(); // 'smth'

function log() {
  console.log('smth');
}
```

```js
const someVal = 'some value';

log();

function log() {
  console.log(someVal);
}
```

JS Execution splits into two phases:

Phases:

1. Compile phase
2. Execution phase

**Compile phase** - Code is analysing

- Variables and functions "store" in memory

**Execution phase**

- code executes from top to bottom


**Hoisting global scope example**

```js
// hoisting works in global scope and local (function) scope

// FUNCTIONS
// hoisting pop up this function 'log' to the top

// VARIABLES
// hoisting pop up DECLARATION of variable someVal to the top
// !!! it means that variable is not initalized (doesnt have value)

//log();

console.log(someVal); // undefined but not error

var someVal = "some value";

//function log() {
//console.log("loggin...");
//}

// 'cause here function is a variable
// hoisting pop up only DECLARATION of variable
// so smth like just "var log;"
// when you will try to call log() above - you will get error "log is not a function"
// BASICALLY: hoisting works the same as with variable for function expressions
var log = function () {
  console.log("loggin...");
};

// here variable 'log' is already initialized with function as a value
// so you can call it as a function
log();
```

**Hoisting local scope example**

```js
logInfo();

// hoisting works the same as in global scope inside function
function logInfo() {
  console.log(numbers); // undefined because hoisting pop up just declaration of variable

  var numbers = [1, 2, 3];
}
```

**Hoisting block scope example (const, let)**

```js
console.log(someVal);

//var someVal = "some value"; // console.log => undefined
const someVal = "some value"; // console.log => error: cannot access ... before initialization
//let someVal = "some value"; // same as for const
```


