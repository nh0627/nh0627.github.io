---
title: JavaScript Execution Context
layout: single
categories:
- JavaScript
tags:
- javascript
last_modified_at: '2021-04-28 14:00:00 +08000'
---

> Summarize what I learned on `Execution Context` of JS

## Execution Context
Execution Context is simply the environment where JavaScript codes run. It has two types, Global and Function, which work as below:
	1. When code is executed, a new execution context with a stack (LIFO) structure is created. 
	2. When control is on the global code, *Global Execution Context* is created and stacked on the execution context. The global execution context exists until the application is finished (either leaving the web page or closing the browser).
	3. When a function is called, its *Function Execution Context* is created and stacked on top of the execution context of the code block executed before. When it is done, the function execution context is discarded and its control is returned to the previous execution context.

## Stage of Execution Context
Each context also has two stages also: Creation and Execution.

### Global Execution Context

#### Creation phase
	1. Create a `global` object
	2. Init all `var` variables to `undefined` and store the initialized variables and declared function into a memory heap (a.k.a. [`hoisting`](Hoisting)
	3. Bind `this` to the global object

#### Execution phase
	1. Assign a value to variables
	2. Execute each function
> When a function in the global code starts executing, a new function execution context is created for every function. 

### Function Execution Context

#### Creation phase
	1. Create a `argument` object, which references all parameters passed into the function
	2. Init arguments, and store arguments and inner functions into a memory heap
	3. Determine `this` value
> A value assigned to `this` will be determined by the function call.

#### Execution phase
	1. Assign a value to variables
	2. Execute inner functions and create each function execution context

### Hoisting
	Hoisting is the process of putting all variable and function declarations into memory during the compile phase. In JavaScript, functions are fully hoisted, var variables are hoisted and initialized to undefined, and `let` and `const` variables are hoisted but not initialized a value. We should avoid `hoisting` by using `let` and `const` as much as possible because it can cause memory leaks and make debugging hard.

### Sources
[Udemy course - JavaScript: The Advanced Concepts](https://www.udemy.com/course/advanced-javascript-concepts/learn/lecture/13772862#overview)
[Poiemaweb](https://poiemaweb.com/js-execution-context)
[JavaScript Tutorial](https://www.javascripttutorial.net/javascript-execution-context/)
[Parameter vs. Arguments](https://stackoverflow.com/questions/1788923/parameter-vs-argument)