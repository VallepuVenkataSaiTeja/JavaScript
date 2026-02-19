# JavaScript Functions – Complete Topics Guide

---

## 1️⃣ Function Basics
- Function declaration  
- Function expression  
- Named vs anonymous functions  
- Parameters vs arguments  
- Return statement  
- Default parameters  
- Rest parameters (`...args`)  
- Spread operator with functions  

---

## 2️⃣ Arrow Functions (ES6)
- Basic syntax  
- Single parameter (no parentheses)  
- Implicit return  
- Returning objects  
- Arrow vs regular functions  
- `this` behavior difference  

---

## 3️⃣ Scope & Execution Context
- Global scope  
- Function scope  
- Block scope (`let`, `const`)  
- Lexical scope  
- Scope chain  
- Execution context  
- Call stack  

---

## 4️⃣ Hoisting
- Function hoisting  
- Variable hoisting  
- Temporal Dead Zone (TDZ)  
- Declaration vs expression behavior  

---

## 5️⃣ Closures ⭐
- What is a closure  
- Lexical environment  
- Data encapsulation  
- Private variables  
- Real-world examples  
- Common interview problems  

---

## 6️⃣ Callback Functions
- What is a callback  
- Synchronous callbacks  
- Asynchronous callbacks  
- Callback hell  
- Error-first callbacks  

---

## 7️⃣ Higher-Order Functions
- Functions as arguments  
- Functions returning functions  
- Array methods:
  - `map()`  
  - `filter()`  
  - `reduce()`  
  - `forEach()`  
  - `some()`  
  - `every()`  

---

## 8️⃣ `this` Keyword
- `this` in global scope  
- `this` in regular functions  
- `this` in object methods  
- `this` in arrow functions  
- Explicit binding:
  - `call()`  
  - `apply()`  
  - `bind()`  
- Hard vs soft binding  

---

## 9️⃣ Immediately Invoked Function Expressions (IIFE)
- Syntax  
- Why use IIFE  
- Module pattern  
- Avoiding global pollution  

---

## 🔟 Recursion
- Base case  
- Recursive case  
- Stack overflow  
- Tail recursion  
- Practical problems (factorial, Fibonacci, tree traversal)  

---

## 1️⃣1️⃣ Function Methods
- `call()`  
- `apply()`  
- `bind()`  
- `toString()`  

---

## 1️⃣2️⃣ Pure vs Impure Functions
- Side effects  
- Deterministic output  
- Referential transparency  
- Benefits in functional programming  

---

## 1️⃣3️⃣ Currying
- What is currying  
- Manual currying  
- Partial application  
- Practical examples  

---

## 1️⃣4️⃣ Function Composition
- Combining functions  
- Pipe vs compose  
- Functional programming patterns  

---

## 1️⃣5️⃣ Generators
- `function*` syntax  
- `yield` keyword  
- Iterators  
- Generator control flow  
- Practical use cases  

---

## 1️⃣6️⃣ Async Functions
- Promises  
- `async` / `await`  
- Error handling with `try/catch`  
- Sequential vs parallel execution  
- `Promise.all()`  
- `Promise.race()`  

---

## 1️⃣7️⃣ Debouncing & Throttling
- Concept  
- Differences  
- Use cases (search input, scroll events)  
- Implementation logic  

---

## 1️⃣8️⃣ Memoization
- Concept  
- Caching results  
- Performance optimization  
- Implementation  

---

## 1️⃣9️⃣ Functional Programming Concepts
- First-class functions  
- Immutability  
- Declarative vs imperative style  
- Side effects management  
- Higher-order utilities  

---

# 🎯 Interview Focus Areas
- Closures  
- `this` keyword  
- Hoisting  
- Async/await  
- Callbacks  
- Currying  
- Recursion  
- Higher-order functions  
- Debouncing & Throttling  

---








# 1️⃣ Function Basics

A **function** in JavaScript is a reusable block of code designed to perform a specific task.

Think of it as:

* Input → Process → Output

```js
function greet() {
  console.log("Hello!");
}
```

You run (call) it like this:

```js
greet(); // Output: Hello!
```

---

# 2️⃣ Function Declaration

A **function declaration** defines a function using the `function` keyword.

### Syntax:

```js
function functionName(parameters) {
  // code
}
```

### Example:

```js
function add(a, b) {
  return a + b;
}
```

### Key Features:

* Hoisted (can be called before it's defined)
* Has a name

```js
console.log(add(2, 3)); // 5

function add(a, b) {
  return a + b;
}
```

---

# 3️⃣ Function Expression

A **function expression** is when a function is assigned to a variable.

### Syntax:

```js
const variableName = function(parameters) {
  // code
};
```

### Example:

```js
const multiply = function(a, b) {
  return a * b;
};

console.log(multiply(3, 4)); // 12
```

### Key Features:

* Not hoisted like declarations
* Treated as a value
* Can be anonymous or named

❌ This won’t work:

```js
console.log(multiply(2, 3)); // Error

const multiply = function(a, b) {
  return a * b;
};
```

---

# 4️⃣ Named vs Anonymous Functions

## ✅ Named Function

A function with a name.

```js
function sayHello() {
  console.log("Hello");
}
```

Also possible in expressions:

```js
const greet = function sayHi() {
  console.log("Hi");
};
```

### Why use named?

* Better debugging (shows name in stack traces)
* Can refer to itself (recursion)

---

## ✅ Anonymous Function

A function without a name.

```js
const greet = function() {
  console.log("Hello");
};
```

Commonly used:

* In callbacks
* In event handlers

Example:

```js
setTimeout(function() {
  console.log("Done!");
}, 1000);
```

---

# 5️⃣ Parameters vs Arguments

## 📌 Parameters

Variables listed in the function definition.

```js
function greet(name) {  // name is a parameter
  console.log("Hello " + name);
}
```

## 📌 Arguments

Actual values passed when calling the function.

```js
greet("John");  // "John" is an argument
```

### Example:

```js
function add(a, b) {
  return a + b;
}

add(5, 3); // 5 and 3 are arguments
```

---

# 6️⃣ Return Statement

The `return` statement:

* Sends a value back
* Stops function execution immediately

```js
function square(num) {
  return num * num;
}

let result = square(4);
console.log(result); // 16
```

### Important:

Without `return`, the function returns `undefined`.

```js
function test() {
  console.log("Hello");
}

console.log(test()); // undefined
```

### Early return example:

```js
function checkAge(age) {
  if (age < 18) {
    return "Too young";
  }
  return "Allowed";
}
```

---

# 7️⃣ Default Parameters

Default parameters allow you to set default values.

### Syntax:

```js
function greet(name = "Guest") {
  console.log("Hello " + name);
}
```

### Example:

```js
greet();        // Hello Guest
greet("Sam");   // Hello Sam
```

### Important:

Default values work if:

* No argument is passed
* `undefined` is passed

```js
greet(undefined); // Hello Guest
```

But:

```js
greet(null); // Hello null
```

---

# 8️⃣ Rest Parameters (...args)

Rest parameters allow a function to accept unlimited arguments.

### Syntax:

```js
function functionName(...args) {
  // args is an array
}
```

### Example:

```js
function sum(...numbers) {
  let total = 0;
  for (let num of numbers) {
    total += num;
  }
  return total;
}

console.log(sum(1, 2, 3, 4)); // 10
```

### Important:

* Must be the last parameter
* Collects remaining arguments into an array

```js
function example(a, b, ...rest) {
  console.log(a);     // first argument
  console.log(b);     // second argument
  console.log(rest);  // remaining arguments
}

example(1, 2, 3, 4, 5);
// a = 1
// b = 2
// rest = [3, 4, 5]
```

---

# 9️⃣ Spread Operator with Functions

The spread operator `...` expands an array into individual values.

## 🔹 Without spread:

```js
function add(a, b, c) {
  return a + b + c;
}

const numbers = [1, 2, 3];

add(numbers); // ❌ Not correct
```

## 🔹 With spread:

```js
add(...numbers); // 6
```

### How it works:

```js
add(...[1, 2, 3]);
```

Becomes:

```js
add(1, 2, 3);
```

---

## 🔹 Spread with Rest Together

```js
function sum(...nums) {
  return nums.reduce((total, n) => total + n, 0);
}

const values = [10, 20, 30];

console.log(sum(...values)); // 60
```

Here:

* Spread expands array
* Rest collects values

---

# 🔥 Deep Comparison: Rest vs Spread

| Feature | Rest                  | Spread                  |
| ------- | --------------------- | ----------------------- |
| Purpose | Collect values        | Expand values           |
| Used in | Function parameters   | Function calls / arrays |
| Result  | Array                 | Individual elements     |
| Syntax  | `function f(...args)` | `f(...array)`           |

---

# 💡 Complete Practical Example

```js
function calculate(operation = "add", ...numbers) {
  if (operation === "add") {
    return numbers.reduce((a, b) => a + b, 0);
  }
  
  if (operation === "multiply") {
    return numbers.reduce((a, b) => a * b, 1);
  }
}

console.log(calculate("add", 1, 2, 3));       // 6
console.log(calculate("multiply", 2, 3, 4));  // 24
console.log(calculate());                     // 0 (default + no numbers)
```

This example uses:

* Default parameter
* Rest parameter
* Return
* Parameters & arguments

---

# 2️⃣ Arrow Functions (ES6)

Arrow functions were introduced in **ES6 (ECMAScript 2015)**.
They provide a shorter syntax and behave differently from regular functions — especially with `this`.

---

# 🔹 1. Basic Syntax

### Regular Function

```js
function add(a, b) {
  return a + b;
}
```

### Arrow Function

```js
const add = (a, b) => {
  return a + b;
};
```

### Shorter Version

```js
const add = (a, b) => a + b;
```

---

# 🔹 2. Single Parameter (No Parentheses)

If there is **only one parameter**, parentheses are optional.

```js
const square = x => x * x;

console.log(square(5)); // 25
```

But if there are:

* **Zero parameters** → use `()`
* **Two or more parameters** → use `(a, b)`

```js
const greet = () => "Hello";
const add = (a, b) => a + b;
```

---

# 🔹 3. Implicit Return

If the function body has **one expression**, arrow functions automatically return it.

### Regular:

```js
function double(n) {
  return n * 2;
}
```

### Arrow (Implicit Return):

```js
const double = n => n * 2;
```

⚠ If you use `{}`, you must write `return` explicitly:

```js
const double = n => {
  return n * 2;
};
```

---

# 🔹 4. Returning Objects

This is where many beginners get confused.

### ❌ Wrong:

```js
const getUser = () => { name: "John" };
```

JavaScript thinks `{}` is a function body.

### ✅ Correct:

Wrap the object in parentheses:

```js
const getUser = () => ({ name: "John" });

console.log(getUser()); // { name: "John" }
```

---

# 🔹 5. Arrow vs Regular Functions

| Feature                    | Regular Function | Arrow Function |
| -------------------------- | ---------------- | -------------- |
| Has its own `this`         | ✅ Yes            | ❌ No           |
| Can be used as constructor | ✅ Yes            | ❌ No           |
| Has `arguments` object     | ✅ Yes            | ❌ No           |
| Syntax                     | Longer           | Shorter        |
| Good for methods           | ✅ Yes            | ⚠ Usually No   |

---

# 🔹 6. `this` Behavior Difference (Very Important 🔥)

This is the **most important difference**.

---

## 🧠 Regular Function → `this` depends on how it's called

```js
const person = {
  name: "Alice",
  greet: function() {
    console.log(this.name);
  }
};

person.greet(); // Alice
```

Here, `this` refers to `person`.

---

## 🧠 Arrow Function → `this` is inherited (lexical `this`)

Arrow functions **do not have their own `this`**.
They take `this` from the surrounding scope.

### Example:

```js
const person = {
  name: "Alice",
  greet: () => {
    console.log(this.name);
  }
};

person.greet(); // undefined
```

Why?

Because arrow function's `this` refers to the global scope, not `person`.

---

# 🔥 Real-World Example (Where Arrow Functions Shine)

## Problem with Regular Function inside setTimeout

```js
const person = {
  name: "Bob",
  greet: function() {
    setTimeout(function() {
      console.log(this.name);
    }, 1000);
  }
};

person.greet(); // undefined
```

Why?
Because inside `setTimeout`, `this` is not `person`.

---

## ✅ Solution with Arrow Function

```js
const person = {
  name: "Bob",
  greet: function() {
    setTimeout(() => {
      console.log(this.name);
    }, 1000);
  }
};

person.greet(); // Bob
```

Arrow function inherits `this` from `greet`.

This is called **lexical `this`**.

---

# 🔹 Arrow Functions Do NOT Have:

## ❌ 1. Their own `arguments`

Regular function:

```js
function test() {
  console.log(arguments);
}

test(1, 2, 3);
```

Arrow function:

```js
const test = () => {
  console.log(arguments); // Error
};
```

Use rest parameters instead:

```js
const test = (...args) => {
  console.log(args);
};
```

---

## ❌ 2. Cannot Be Used as Constructor

```js
const Person = (name) => {
  this.name = name;
};

const p = new Person("John"); // Error
```

Arrow functions cannot be used with `new`.

---

# 🔥 When to Use Arrow Functions

✅ Best for:

* Short functions
* Array methods (`map`, `filter`, `reduce`)
* Callbacks
* When you want lexical `this`

Example:

```js
const numbers = [1, 2, 3];

const doubled = numbers.map(n => n * 2);

console.log(doubled); // [2, 4, 6]
```

---

# 🔥 When NOT to Use Arrow Functions

❌ As object methods (usually)
❌ As constructors
❌ When you need dynamic `this`
❌ When you need `arguments`

---

# 🔥 Deep Concept Summary

### Regular Function:

* Dynamic `this`
* Can be constructor
* Has `arguments`
* More flexible

### Arrow Function:

* Lexical `this`
* Short syntax
* No constructor
* No `arguments`

---

# 🧠 Final Comparison Example

```js
function regular() {
  console.log(this);
}

const arrow = () => {
  console.log(this);
};

regular(); // depends how called
arrow();   // always from outer scope
```

---

Excellent 🔥 — this is one of the **most important core concepts in JavaScript**.
If you deeply understand **Scope & Execution Context**, you’ll understand how JS really works behind the scenes.

We’ll go step by step and connect everything together clearly.

---

# 3️⃣ Scope & Execution Context (Deep Explanation)

---

# 1️⃣ Global Scope

## 📌 What is Global Scope?

Global scope is the outermost scope in your JavaScript program.

* Variables declared outside any function or block
* Accessible everywhere in the program

```js
let globalVar = "I am global";

function show() {
  console.log(globalVar);
}

show(); // I am global
```

### 🌍 In Browser

Global scope is attached to:

```js
window
```

```js
var x = 10;
console.log(window.x); // 10
```

⚠ But:

```js
let y = 20;
console.log(window.y); // undefined
```

Why?
Because `var` attaches to `window`, but `let` and `const` do NOT.

---

# 2️⃣ Function Scope

## 📌 What is Function Scope?

Variables declared inside a function:

* Are accessible only inside that function
* Cannot be accessed outside

```js
function test() {
  let message = "Hello";
  console.log(message);
}

test(); // Hello
console.log(message); // ❌ Error
```

Each function creates its own **local scope**.

---

## 🔥 Important: `var` is function-scoped

```js
function example() {
  if (true) {
    var x = 5;
  }
  console.log(x); // 5
}
```

Even though `x` is inside `if`, it is accessible because `var` ignores block scope.

---

# 3️⃣ Block Scope (let, const)

Block scope means variables exist only inside `{ }`.

Applies to:

* `let`
* `const`

```js
if (true) {
  let a = 10;
  const b = 20;
}

console.log(a); // ❌ Error
console.log(b); // ❌ Error
```

---

## 🔥 var vs let (Important Difference)

```js
if (true) {
  var x = 1;
  let y = 2;
}

console.log(x); // 1
console.log(y); // ❌ Error
```

✔ `var` → function-scoped
✔ `let/const` → block-scoped

---

# 4️⃣ Lexical Scope

This is extremely important.

## 📌 Lexical = Based on where code is written

JavaScript determines scope **at writing time**, not at runtime.

---

### Example:

```js
function outer() {
  let outerVar = "I am outer";

  function inner() {
    console.log(outerVar);
  }

  inner();
}

outer();
```

Why does `inner()` access `outerVar`?

Because of **lexical scope** — inner function was defined inside outer function.

---

## 🔥 Key Rule:

> Inner functions can access variables of outer functions.

But outer functions cannot access inner variables.

```js
function outer() {
  function inner() {
    let secret = "Hidden";
  }
  console.log(secret); // ❌ Error
}
```

---

# 5️⃣ Scope Chain

When JS tries to find a variable, it looks in a specific order.

## 📌 What is Scope Chain?

If a variable is not found in the current scope, JavaScript looks in:

1. Current scope
2. Parent scope
3. Parent’s parent scope
4. Global scope
5. If not found → ReferenceError

---

### Example:

```js
let a = 1;

function first() {
  let b = 2;

  function second() {
    let c = 3;
    console.log(a, b, c);
  }

  second();
}

first();
```

### How JS finds variables inside `second()`:

* Looks for `a` → not inside `second`
* Goes to `first`
* Not there
* Goes to global
* Found ✅

That searching process is the **scope chain**.

---

# 6️⃣ Execution Context (Very Important 🔥🔥)

Now we go deeper into how JavaScript actually runs code.

---

## 📌 What is Execution Context?

Execution Context is the environment in which JavaScript code runs.

There are 3 types:

1. Global Execution Context (GEC)
2. Function Execution Context (FEC)
3. Eval Execution Context (rarely used)

---

# 🔹 Global Execution Context (GEC)

When JS starts running:

* It creates Global Execution Context
* `this` is set
* Memory is allocated for variables & functions

Example:

```js
let x = 10;

function test() {
  console.log("Hello");
}

test();
```

When this runs:

1. JS creates Global Execution Context
2. Allocates memory
3. Executes line by line

---

# 🔥 Execution Context Has Two Phases

Every execution context has:

## 1️⃣ Memory Creation Phase (Hoisting Phase)

* Variables declared with `var` → set to `undefined`
* Functions → stored completely
* let/const → in "temporal dead zone"

Example:

```js
console.log(x);
var x = 5;
```

Behind the scenes:

Memory phase:

```js
var x = undefined;
```

Execution phase:

```js
x = 5;
```

That’s why output is:

```
undefined
```

---

## 2️⃣ Execution Phase

Now JS runs code line by line and assigns values.

---

# 7️⃣ Call Stack (How Functions Run)

JavaScript is **single-threaded**.

It uses a structure called:

# 📦 Call Stack

Think of it like a stack of plates.

Last in → First out (LIFO)

---

### Example:

```js
function one() {
  two();
}

function two() {
  three();
}

function three() {
  console.log("Done");
}

one();
```

---

### What happens in Call Stack:

1. Global Execution Context pushed
2. `one()` pushed
3. `two()` pushed
4. `three()` pushed
5. `three()` finishes → removed
6. `two()` finishes → removed
7. `one()` finishes → removed
8. Back to global

---

### Visual:

```
| three() |
| two()   |
| one()   |
| Global  |
```

Then it unwinds.

---

# 🔥 Call Stack Overflow

If functions call themselves infinitely:

```js
function test() {
  test();
}

test();
```

You get:

```
Uncaught RangeError: Maximum call stack size exceeded
```

Because stack memory fills up.

---

# 🧠 How Everything Connects

When you run JS:

1. Global Execution Context created
2. Variables & functions stored in memory
3. Code executed line by line
4. Each function call creates new Execution Context
5. Execution contexts are pushed into Call Stack
6. Removed when finished
7. Scope chain determines variable access

---

# 🔥 Real Mental Model

Think of it like:

* Scope = Where variables live
* Lexical Scope = Who can see whom
* Scope Chain = How JS searches variables
* Execution Context = Container where code runs
* Call Stack = Order of function execution

---

# 🚀 Super Important Interview Summary

✔ JS is lexically scoped
✔ `var` = function scoped
✔ `let/const` = block scoped
✔ Execution context has memory & execution phases
✔ JS uses call stack (LIFO)
✔ Each function call creates new execution context

---


