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


# 1.9 Arrow Functions — JavaScript

Arrow functions are a **modern and shorter way** to write functions in JavaScript.  
Introduced in ES6, they provide cleaner syntax and more predictable behavior — especially with `this`.

👉 Think of them as **compact functions with lexical behavior**.

---

# ✅ Why Arrow Functions Exist

Traditional functions sometimes behave unexpectedly with `this`, especially inside callbacks.

Arrow functions solve this by:

✅ Providing shorter syntax  
✅ Removing `this` confusion  
✅ Encouraging functional programming style  
✅ Making callbacks cleaner  

---

# ✅ Basic Syntax

## Traditional Function
```javascript
function add(a, b){
  return a + b;
}
```

## Arrow Function Equivalent
```javascript
const add = (a, b) => {
  return a + b;
};
```

---

# ⭐ Shorter Return (Implicit Return)

If the function has **one expression**, you can skip `{}` and `return`.

```javascript
const add = (a, b) => a + b;
```

Automatically returns the result.

---

# ✅ Parameter Variations

## No Parameters
```javascript
const greet = () => "Hello!";
```

⚠ Parentheses are required.

---

## One Parameter
```javascript
const square = x => x * x;
```

Parentheses are optional (but often recommended for readability).

---

## Multiple Parameters
```javascript
const multiply = (a, b) => a * b;
```

Parentheses are required.

---

# ✅ Returning Objects (Common Trap)

This does NOT work:

```javascript
const user = () => {name: "Sam"};
```

JavaScript thinks `{}` is a function body.

## ✅ Correct Way:
Wrap object in parentheses.

```javascript
const user = () => ({name: "Sam"});
```

---

# 🔥 Arrow Functions vs Regular Functions

Understanding the differences is critical.

---

# ⭐ 1. `this` Behavior (MOST IMPORTANT)

### Regular Function:
`this` depends on **how the function is called**.

### Arrow Function:
`this` is inherited from the surrounding scope (lexical).

---

## Example — Regular Function Problem

```javascript
const person = {
  name: "Alex",
  greet: function(){
    setTimeout(function(){
      console.log(this.name);
    }, 1000);
  }
};

person.greet();
```

Output:
```
undefined
```

Why?  
Because `this` inside `setTimeout` refers to the global object.

---

## ✅ Arrow Function Fix

```javascript
const person = {
  name: "Alex",
  greet: function(){
    setTimeout(() => {
      console.log(this.name);
    }, 1000);
  }
};

person.greet();
```

Output:
```
Alex
```

Arrow functions **capture `this` from their parent scope.**

👉 This is one of the biggest reasons developers love arrow functions.

---

# ⭐ 2. Arrow Functions Are NOT Hoisted

```javascript
sayHi(); // ❌ Error

const sayHi = () => {
  console.log("Hi");
};
```

Behave like variables declared with `const` or `let`.

---

# ⭐ 3. No `arguments` Object

Regular functions have access to `arguments`.

Arrow functions do NOT.

```javascript
const test = () => {
  console.log(arguments); // ❌ Error
};
```

## ✅ Use Rest Parameters Instead

```javascript
const test = (...nums) => {
  console.log(nums);
};

test(1,2,3);
```

Output:
```
[1,2,3]
```

---

# ⭐ 4. Cannot Be Used as Constructors

Arrow functions cannot be called with `new`.

```javascript
const Person = (name) => {
  this.name = name;
};

new Person("Sam"); // ❌ Error
```

Why?  
They do not have their own `this`.

Use regular functions or classes instead.

---

# ⭐ 5. No `prototype`

Because they cannot act as constructors, arrow functions also lack a prototype.

---

# ⭐ 6. Cannot Use `yield`

Arrow functions cannot be generator functions.

---

# ✅ When SHOULD You Use Arrow Functions?

Perfect for:

✔ Callbacks  
✔ Array methods  
✔ Short utility functions  
✔ Functional programming  
✔ Situations needing lexical `this`  

---

## Example — Array Mapping

```javascript
const numbers = [1,2,3];

const doubled = numbers.map(n => n * 2);

console.log(doubled);
```

Output:
```
[2,4,6]
```

Clean and readable.

---

# ⚠️ When NOT to Use Arrow Functions

## ❌ Object Methods

Avoid this:

```javascript
const user = {
  name: "Sam",
  greet: () => {
    console.log(this.name);
  }
};

user.greet();
```

Output:
```
undefined
```

Because arrow functions don't bind their own `this`.

---

## ✅ Use Regular Function Instead

```javascript
const user = {
  name: "Sam",
  greet(){
    console.log(this.name);
  }
};
```

---

## ❌ Event Handlers (Sometimes)

If you need `this` to refer to the element, avoid arrow functions.

---

# ⭐ Implicit vs Explicit Return

## Explicit
```javascript
const add = (a,b) => {
  return a+b;
};
```

## Implicit
```javascript
const add = (a,b) => a+b;
```

Use implicit for short logic.  
Use explicit for complex code.

---

# ⭐ Readability Rule

👉 Short → Arrow  
👉 Complex → Regular function  

Never sacrifice clarity for brevity.

---

# 🔥 Common Beginner Mistakes

## ❌ Forgetting parentheses around object return
## ❌ Using arrows as object methods
## ❌ Expecting `arguments`
## ❌ Trying to use with `new`
## ❌ Assuming they are hoisted

---

# 🧠 Interview-Level Insight

Arrow functions are **lexically bound**.

This means they permanently capture:

- `this`
- `super`
- `arguments` (from parent)
- `new.target`

From the surrounding scope.

👉 This makes behavior more predictable.

---

# ⭐ Traditional vs Arrow (Quick Table)

| Feature | Regular Function | Arrow Function |
|--------|-----------------|----------------|
| Syntax | Longer | Short |
| this | Dynamic | Lexical |
| Hoisted | Yes (declaration) | No |
| arguments | Yes | No |
| Constructor | Yes | No |
| Prototype | Yes | No |

---

# ✅ Best Practices

✔ Use arrow functions for short logic  
✔ Prefer them in array callbacks  
✔ Avoid for object methods  
✔ Avoid when dynamic `this` is needed  
✔ Keep them readable  

---

# ✅ One-Line Summary

**Arrow functions are concise, lexically bound functions that simplify syntax and eliminate `this` confusion, making them ideal for modern JavaScript development.**
