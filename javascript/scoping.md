# Scoping

> **Scoping** - accessing variables to different areas of the code

## Scopes

> Scope is about visibility of variables

1. Local Scope (Function Scope)
2. Global Scope
3. Block Scope


- **Local Scope** -- variables defined inside some function
- **Global Scope** -- variables defined outside of any functions (variables defined globally)
- **Block Scope** - variabled defined inside --> {}

**var** can be declared in scopes:

- Local Scope
- Global Scope

**let**, **const** can be declared only in:

- Block Scope

## Local and Global Scopes

```js
// declairing and initializing (defining)

// var smth - declaration of the variable
// = "something" - initialization (definition) of the variable
var smth = "something"; // <---- global scope ('cause variable isnt declairing inside some function)

function log() {
  function logMore() {
    var someMoreName = "just some name";
    console.log(someName); // print "some name" 'cause there is the same scope - local scope
    console.log(smth);
  }

  var someName = "some name"; // <--- local scope (function scope)
  console.log("logging..." + someName);
  console.log("and also..." + smth); // local scope has access to variables from global scope

  //console.log("someMoreName", someMoreName); // error: is not defined

  logMore();
}

// console.log(someName); // error! is not defined

log();
```

## Global Scope in several files

Variables that defined in global scope are available in all .js files in one page (html)

**index.html**

```html
  <script src="moduleA.js"></script>
  <script src="moduleB.js"></script>
```

**moduleA.js**

```js
var someName = "some name";
```

**moduleB.js**

```js
console.log(someName); // "someName"
console.log(this.someName); // "someName"
console.log(self.someName); // "someName"
```

if we use **let** or **const** for someName:

**moduleA.js**

```js
const someName = "some name";
```

**moduleB.js**

```js
console.log(someName); // "someName"
console.log(this.someName); // undefined
console.log(self.someName); // undefined
```

## Block Scope

```js
const isSmth = true; // block scope (but seems like global scope)

if (isSmth) {
  // block scope
  var globalVar = 123; // <--- but this is a global scope because of "var". var can't be in block scope

  const smth = "something";

  console.log(smth); // 'something'
}

console.log(globalVar); // '123'

//console.log(smth); // error, is not defined

function log() {
  const someVal = "some value";
  console.log("globalVar 1", globalVar); // prints '123', available everywhere (global scope)

  function logMore() {
    const someMoreVal = "some more val";
    console.log("someVal", someVal); // 'some value'
    console.log("globalVar 2", globalVar); // the same as line 18
  }

  //console.log("someMoreVal", someMoreVal); // error: is not defined

  logMore();
}

log();
```

**Another Example**

global scope:

- user
- greetings
- doSmth

local scope (greetings):

- user
- local scope (doSmth):
- action


```js
/*
//console.log(y); // error
console.log(x);

y = 42;

// by using 'var' js stores declaration of variable (without value) in memory
// thats why will see 'undefined' in line 2
var x = 10;

console.log(y);
console.log(x);
*/

// global scope
var user = "max";

//greetings(); // Welcome

// global scope
function greetings() {
  // local (function) scope
  var user = "john"; // variable shadowing
  console.log("Welcome");
}

// global scope
function doSmth() {
  // local (function) scope
  var action = "Running";
  console.log(action);
}

greetings(); // Welcome
doSmth(); // Running

// Scope Manager controls variables and declaration and put them into needed scopes
```

**One more example**

```js
/* case with 'name' variable/parameter
 *
function log(name) {
  console.log("this is " + name);
}

log("john");

// in browser: prints empty string (name is already in global scope as window.name)
// in node: exception
console.log(name);
*/

// var in loop

for (var i = 0; i < 10; i++) {
  //console.log("in loop " + i);
}

// prints '10' 'cause it will be incremented but won't print in loop because of 10 is not lower than 10
// and also 'i' is in global scope
//console.log("globally " + i);

for (let j = 0; j < 10; j++) {
  console.log("in loop " + j);
}

// 'j' is in block scope of for loop
// it doesn't exist in global scope
//console.log("globally " + j); // error: is not defined

try {
  throw new Error();
} catch (error) {
  // special scope that is seems like block scope
  console.log(error);
}
```
