# Recursion and Execution Context

> Execution Context - data structure in JS that hold information about script/function execution;

There are several contextes:

1. Global context
2. Function context
3. eval

Example with factorial method:

```js
console.log(fct(4)); // 4 * 3 * 2 * 1 = 24
//console.log(fct(5)); // 5 * 4 * 3 * 2 * 1

/*
function fct(n) {
  let res = 1;
  for (let i = 0; i < n; i++) {
    res *= n - i;
  }
  return res;
}
*/

function fct(n) {
  //return n === 0 ? 1 : n * fct(n - 1);
  if (n === 0) {
    return 1;
  }
  return n * fct(n - 1); // recursive step
}
```

Steps:

1. s1. created new execution local context: fct(2)
2. s2. created new execution local context: fct(1)
3. s3. created new execution local context: fct(0)


**LCONTEXT** = Local Context

```

|            SCRIPT            |                    JS Engine                                        |
|------------------------------|---------------------------------------------------------------------|
|                              | st1         | st2        | st3         | Execution Context Stack    |
|                              | LCONTEXT    | LCONTEXT   | LCONTEXT    | (Call Stack)               |
| function fct(n) {            | fct(2)      | fct(1)     | fct(0)      |----------------------------|
|   if (n === 0) { return 1;}  | ------------|------------|-------------|                            |
|   return n * fct(n - 1);     | n = 2       | n = 1      | n = 0       |                            |
| }                            | if -> false | if -> false| if -> true  |  fct(0) ----               |
|                              | 2 * fct(1)  | 1 * fct(0) |             |            |1              | 
| fct(2);  (st1)               | ^-------->  |            |             |  fct(1) <---1*fct(0)=> 1*1 |
|                              |             |            |             |            |1              |
|                              |             |            |             |  fct(2) <---2*fct(1)=> 2*1 |
|                              |             |            |             |                            |
|                              |             |            |             |                            |

```

