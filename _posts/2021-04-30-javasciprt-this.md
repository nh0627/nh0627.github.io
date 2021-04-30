---
title: JavaScript the `this` Keyword
layout: single
categories:
- JavaScript
tags:
- javascript
last_modified_at: '2021-04-30 14:00:00 +08000'
---

> A summarized note about what I learned on the `this` keyword of JS.

The `this` keyword in JavaScript works differently from other programming language. The `this` references *the object that is currently calling the function*. In other words, the object to be bound to `this` is determined *dynamically*  (not *statically* or *lexically*) depending on how the function is called when the function is called.

## Global Context
Global Object means the only top-level object of all objects, which is `window` in a browser-side and `global` in a server-side (Node.js). Basically, `this` is bound to the global object. In the case of global functions, even inner functions and callback functions, `this` is bound to the global object, not to the outer function.

```js
var value = 1;

var obj = {
  value: 100,
  foo: function() {
    console.log("foo's this: ",  this);  // obj
    console.log("foo's this.value: ",  this.value); // 100
    function bar() {
      console.log("bar's this: ",  this); // window
      console.log("bar's this.value: ", this.value); // 1
    }
    bar();
  },
  cb: function() {
    setTimeout(function() {
      console.log("callback's this: ",  this);  // window
      console.log("callback's this.value: ",  this.value); // 1
    }, 100);
  }
};

obj.foo();
obj.cb();
```

### In the strict mode
When we prevent this situation that is `this` references the global object when a functions is called. With `use strict`, we can make `this` points `undefined, rather the global object.

```js
function foo() {
    "use strict";
    console.log(this === undefined); // true

    function bar() {
        console.log(this === undefined); // true
    }
    bar();
}

foo();

```

## Method invocation
When we call an object's method, `this` will mean the object that has the method.

```js
var obj1 = {
  name: 'Lee',
  sayName: function() {
    console.log(this.name);
  }
}

var obj2 = {
  name: 'Kim'
}

obj2.sayName = obj1.sayName;

obj1.sayName();
obj2.sayName();
```

However, if we call the method without specifying its object, `this` is set to the global object in non-strict mode and `undefined` in the strict mode.

```js
// still continued with the above code

var sayName = obj1.sayName;
sayName(); // undefined
```

To fix this, we can use `bind()`, `apply()`, `call()` to specify an owner of the method, or to clear an object `this` has to be bount to.

```js
// still continued with the above code

var sayName = obj1.sayName.bind(obj1);
sayName(); // Lee
```

## Constructor Invocation
In JavaScript, if a normal function is called with `new` operator, it behaves as a constructor function. JavaScript creates a new object and sets `this` to the newly created object. To avoid a confusion, a constructor function is named by capitalizing the first character.

```js
// contructor function
function Person(name) {
  this.name = name;
}

var me = new Person('Lee');
console.log(me); // Person&nbsp;{name: "Lee"}

// It does not behave as a contructor function without a 'new' operator
var you = Person('Kim');
console.log(you); // undefined
```

## Arrow Function
In arrow functions, `this` is set *lexically*. In other words, it takes the `this` from the outer function of the arrow function, without its own execution context. This is the reason why the arrow functions are useful for callback functions. Moreover, the arrow functions are not recommended to use them as a method of an object, because `this` will be lexically scoped.

```js
let getThis = () => this;
console.log(getThis() === window); // true

```

## Sources
[Udemy course - JavaScript: The Advanced Concepts](https://www.udemy.com/course/advanced-javascript-concepts/)
[Poiemaweb](https://poiemaweb.com/js-this)
[JavaScript Tutorial](https://www.javascripttutorial.net/javascript-this/)
