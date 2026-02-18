# 1.8 Functions (Basics) — JavaScript

Functions are one of the **most fundamental building blocks** in JavaScript.

👉 A function is simply a **reusable block of code** designed to perform a specific task.

Instead of writing the same code multiple times, you define it once and call it whenever needed.

Think of a function like a **machine**:

- Input → Parameters  
- Process → Function body  
- Output → Return value  

---

# ✅ Why Functions Matter

Functions help you write:

✅ Cleaner code  
✅ Reusable logic  
✅ Modular programs  
✅ Easier debugging  
✅ Scalable applications  

Without functions, large programs would become chaotic and repetitive.

---

# ✅ 1. Function Declaration

The most traditional way to create a function.

## Syntax

```javascript
function name(parameters) {
  return value;
}
```

## Example

```javascript
function greet(name) {
  return "Hello " + name;
}

console.log(greet("Sam"));
```

Output:
```
Hello Sam
```

---

## ⭐ Hoisting (VERY IMPORTANT)

Function declarations are **hoisted**, meaning JavaScript moves them to the top of their scope during compilation.

You can call them **before they appear in the code.**

```javascript
sayHi(); // Works!

function sayHi() {
  console.log("Hi!");
}
```

### Why?
Behind the scenes, JavaScript registers the function before execution begins.

---

## ✅ Creates a Named Function

Named functions:

- Improve readability  
- Help debugging (stack traces show the name)  
- Allow recursion  

---

# ✅ 2. Function Expression

A function stored inside a variable.

## Syntax

```javascript
const fn = function(parameters) {

};
```

## Example

```javascript
const add = function(a, b) {
  return a + b;
};

console.log(add(2, 3));
```

Output:
```
5
```

---

## ⚠️ NOT Hoisted

Function expressions behave like variables.

Calling them early causes an error.

```javascript
add(2,3); // ❌ Error

const add = function(a,b){
  return a+b;
};
```

Why?

Because `const` and `let` are not initialized until execution reaches that line.

---

## Anonymous vs Named Expressions

### Anonymous:
```javascript
const square = function(x) {
  return x * x;
};
```

### Named:
```javascript
const square = function sq(x) {
  return x * x;
};
```

Named expressions help debugging but are less common.

---

# ✅ 3. Parameters vs Arguments

## Parameters
Variables listed in the function definition.

```javascript
function greet(name) {
}
```

`name` is a parameter.

---

## Arguments
Actual values passed into the function.

```javascript
greet("Alex");
```

"Alex" is the argument.

---

## Missing Arguments → undefined

```javascript
function greet(name) {
  console.log(name);
}

greet(); // undefined
```

---

## Extra Arguments → Ignored (Mostly)

```javascript
function add(a, b) {
  return a + b;
}

add(2,3,4); // 4 is ignored
```

However, they can still be accessed using the **arguments object**.

---

## The `arguments` Object

Available inside **non-arrow functions**.

```javascript
function showArgs() {
  console.log(arguments);
}

showArgs(1,2,3);
```

Output:
```
{0:1, 1:2, 2:3}
```

Useful when you don’t know how many inputs will come.

---

## ⭐ Arity (Interview Concept)

Arity = Number of declared parameters.

```javascript
function test(a,b,c){}

console.log(test.length); // 3
```

👉 Does NOT count arguments — only parameters.

---

# ✅ 4. Return Statement

The `return` keyword:

- Sends a value back to the caller  
- Immediately stops function execution  

---

## Example

```javascript
function multiply(a,b){
  return a*b;
}

let result = multiply(2,4);
console.log(result);
```

Output:
```
8
```

---

## ⚠️ No Return → undefined

```javascript
function test(){
}

console.log(test());
```

Output:
```
undefined
```

Even this returns undefined:

```javascript
return;
```

---

## Returning Multiple Values

JavaScript returns **only ONE value**.

Use objects or arrays.

### Object Example
```javascript
function getUser(){
  return {
    name: "Sam",
    age: 25
  };
}
```

### Array Example
```javascript
function getCoords(){
  return [10,20];
}
```

---

## ⭐ Early Return (Best Practice)

Reduces nesting and improves readability.

```javascript
function checkAge(age){

  if(age < 18){
    return "Minor";
  }

  return "Adult";
}
```

Cleaner than deep `if/else`.

---

# ✅ 5. Scope

Scope determines **where variables are accessible**.

---

## 🔹 Global Scope

Declared outside functions.

```javascript
let globalVar = "I am global";

function test(){
  console.log(globalVar);
}
```

Accessible everywhere (avoid overusing).

---

## 🔹 Function Scope

Variables declared inside a function stay inside it.

```javascript
function demo(){
  let secret = 123;
}

console.log(secret); // ❌ Error
```

---

## 🔹 Block Scope

Created with `{}` when using `let` or `const`.

```javascript
if(true){
  let x = 10;
}

console.log(x); // ❌ Error
```

⚠ `var` ignores block scope — avoid it in modern JS.

---

# ⭐ Lexical Scope (VERY IMPORTANT)

Functions access variables based on **where they are defined**,  
NOT where they are called.

```javascript
let x = 10;

function outer(){

  let x = 20;

  function inner(){
    console.log(x);
  }

  inner();
}

outer();
```

Output:
```
20
```

Inner function uses the nearest variable in its lexical environment.

---

# ⭐ Nested Functions & Closure Intro

Functions inside other functions can access outer variables.

```javascript
function outer(){

  let counter = 0;

  function inner(){
    counter++;
    console.log(counter);
  }

  return inner;
}

const fn = outer();
fn();
fn();
```

Output:
```
1
2
```

Even after `outer()` finishes, `inner()` remembers `counter`.

👉 This behavior is called a **closure**.

(You’ll study this deeply later — it’s a major JavaScript concept.)

---

# ✅ 6. Shadowing

When an inner variable has the **same name** as an outer variable.

```javascript
let value = 10;

function test(){

  let value = 20;

  console.log(value);
}

test();
```

Output:
```
20
```

The inner variable **shadows** the outer one.

The outer variable remains unchanged.

---

## ⚠️ Illegal Shadowing

```javascript
let x = 10;

{
  var x = 20; // ❌ Error
}
```

Mixing `let` and `var` this way causes issues.

---

# ⭐ Function Best Practices

✅ Keep functions small  
✅ Do one task only  
✅ Use descriptive names  
✅ Prefer early returns  
✅ Avoid global variables  
✅ Use `const`/`let`, avoid `var`  

---

# 🔥 Common Beginner Mistakes

## ❌ Forgetting return
```javascript
function add(a,b){
  a+b;
}
```

Returns undefined.

---

## ❌ Confusing parameters and arguments

Parameters → definition  
Arguments → actual values  

---

## ❌ Overusing global variables
Leads to bugs and side effects.

---

## ❌ Writing giant functions
Break them into smaller ones.

---

# 🧠 Interview-Level Insight

👉 In JavaScript, functions are **first-class citizens**.

This means they can be:

- Stored in variables  
- Passed as arguments  
- Returned from other functions  

(This is the foundation of callbacks, promises, and async programming.)

---

# ✅ One-Line Summary

**Functions are reusable blocks of code that accept inputs, process logic, and return outputs while maintaining their own scope.**
