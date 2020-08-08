# Variable Shadowing

> **Shadowing** - redeclairing variable that was declaired in upper scope

or 

> **Shadowing** - having variables with the same name but in different scopes


Example:

```js
const someVal = "some value";

function log() {
  const someVal = "another value";
  console.log(someVal); // prints "another value"
}

log();
```

Another Example:

```js
// global scope
var user = "max";

//greetings(); // Welcome

// global scope
function greetings() {
  // local (function) scope
  var user = "john"; // variable shadowing
  console.log("Welcome " + user);
}

// global scope
function doSmth() {
  // local (function) scope
  var action = "Running";
  console.log(action);
}

greetings(); // Welcome john
doSmth(); // Running

```
