---
title: JavaScript Scope
layout: single
categories:
- JavaScript
tags:
- javascript
last_modified_at: '2021-04-29 14:00:00 +08000'
---

> A summarized note about what I learned on `Scope` of JS.

Scope is a rule for finding a referenced identifier (a unique name that can distinguish one object from another object). JavaScript looks up identifiers according to the scope rule. An identifiers has its scope where it can be valid (where other code can refer to them) by where it is declared. If there is no directory, we can only create one file with the same name. Scope also avoids collision of duplicated identifier names in this way. 

## Function-level scope
Unlike other C-family languages (which has block-level scope), JavaScript has function-level scope. Function level scope means that a variable declared within a function code block is valid only within the function code block and not (cannot be referenced) outside the function. All variables declared outside a function will have global scope, even if they are declared inside a block of code. However, block-level scope can be used by using `const` or `let` keyword.
```js
if (true) {
  var x = 5;
}
console.log(x); // global scope
```

## Global & Local scope

### Global Scope
Global variables with global scope can be referenced globally (from anywhere in your code). A global variable declared with the `var` keyword is a property of a global object `window`. 
 
### Local Scope 
Local variables declared in a region (inside a function) can only be referenced in that local region.
```js
var x = 'global';

function foo() {
  var x = 'local';
  console.log(x);
}

foo();          // local
console.log(x); // global
```

## Scope chain
Each scope created has a link outside of its lexical environment called the scope chain. The scope chain gives us access to variables in the parent scope (only upwards). When a variable is used, JavaScript will look up the variable in the current context (function execution context). If it cannot find any, then it will find the variable in the in the outer execution context which is its parent function's execution context or global execution context.

```js
var y = 20;

function bar() {
    var y = 200;

    function baz() {  
        console.log(y);
    }

    baz();
}

bar();
```

## Global variable leaks
After the JavaScript looks up the `counter` variable from the local to global scope, if it cannot find any, it creates the variable in the global scope. By adding `use strict` at the top, we can prevent this weird behavior.
```js
function getCounter() {
    counter = 10;
    return counter;
}

console.log(getCounter()); // 10
```