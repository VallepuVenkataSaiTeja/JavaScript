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

## 4️⃣ Hoisting in JavaScript (Deep Dive)

**Hoisting** is JavaScript’s default behavior of moving *declarations* to the top of their scope **before code execution**.

Important:
JavaScript does **NOT** move your code physically. During the **creation phase** of execution, the engine scans the code and registers declarations in memory before running it.

---

# 🔹 1. Function Hoisting

## ✅ Function Declarations — Fully Hoisted

Function declarations are hoisted **with their entire definition**.

### Example:

```js
sayHello(); 

function sayHello() {
  console.log("Hello!");
}
```

### What actually happens behind the scenes:

During memory creation:

```js
function sayHello() {
  console.log("Hello!");
}
```

So when `sayHello()` runs, the function already exists.

---

### Why This Works

Function declarations are stored in memory before execution, so you can:

* Call them before definition
* Use them anywhere in their scope

---

## ❌ Function Expressions — Not Fully Hoisted

Function expressions behave differently.

### Example:

```js
sayHi(); // ❌ TypeError

var sayHi = function() {
  console.log("Hi!");
};
```

### What happens:

During creation phase:

```js
var sayHi = undefined;
```

So when `sayHi()` runs:

```js
undefined(); // ❌ TypeError
```

The variable is hoisted — but the function assignment is NOT.

---

### With `let`:

```js
sayHi(); // ❌ ReferenceError

let sayHi = function() {
  console.log("Hi!");
};
```

Now it fails differently (TDZ — explained below).

---

# 🔹 2. Variable Hoisting

## `var` Hoisting

Variables declared with `var` are:

* Hoisted
* Initialized with `undefined`

### Example:

```js
console.log(a); // undefined
var a = 10;
```

Behind the scenes:

```js
var a;        // hoisted
console.log(a); // undefined
a = 10;
```

So no error — just `undefined`.

---

## `let` and `const` Hoisting

`let` and `const` are also hoisted…

But they are NOT initialized.

This creates something called the:

---

# 🔹 3. Temporal Dead Zone (TDZ)

The **Temporal Dead Zone (TDZ)** is:

> The time between entering scope and the actual declaration being executed — where the variable exists but cannot be accessed.

---

### Example:

```js
console.log(x); // ❌ ReferenceError
let x = 5;
```

Behind the scenes:

```js
// x exists in memory
// but is uninitialized
```

Accessing it before initialization causes:

```
ReferenceError: Cannot access 'x' before initialization
```

---

## TDZ Timeline

```js
{
  // TDZ starts
  let x; // TDZ ends here
}
```

From block start → until `let x` executes = TDZ.

---

## Why TDZ Exists

It prevents accidental usage before initialization.

Compare:

```js
var count = 5;
```

vs

```js
let count = 5;
```

With `var`, mistakes silently become `undefined`.

With `let`, JavaScript throws an error — safer and more predictable.

---

# 🔹 4. Declaration vs Expression Behavior

This is where many developers get confused.

---

## Function Declaration

```js
function greet() {
  return "Hello";
}
```

* Fully hoisted
* Can call before definition

---

## Function Expression

```js
var greet = function() {
  return "Hello";
};
```

* Variable hoisted
* Function NOT hoisted
* Cannot call before assignment

---

## Arrow Function

```js
const greet = () => "Hello";
```

* `const` hoisted
* But in TDZ
* Cannot call before definition

---

# 🔥 Side-by-Side Comparison

| Type                         | Hoisted?  | Initialized?    | Can Call Before Definition? |
| ---------------------------- | --------- | --------------- | --------------------------- |
| `function declaration`       | ✅ Yes     | ✅ Yes           | ✅ Yes                       |
| `var` variable               | ✅ Yes     | ✅ undefined     | ❌ (undefined)               |
| `let` variable               | ✅ Yes     | ❌ No (TDZ)      | ❌ ReferenceError            |
| `const` variable             | ✅ Yes     | ❌ No (TDZ)      | ❌ ReferenceError            |
| Function expression (`var`)  | Partially | undefined       | ❌ TypeError                 |
| Arrow function (`let/const`) | In TDZ    | Not initialized | ❌ ReferenceError            |

---

# 🔎 Advanced Example — Tricky Interview Question

```js
var x = 1;

function test() {
  console.log(x);
  var x = 2;
}

test();
```

### Output:

```
undefined
```

### Why?

Inside `test`, this happens:

```js
function test() {
  var x;            // hoisted
  console.log(x);   // undefined
  x = 2;
}
```

The inner `x` shadows the outer `x`.

---

# 🔎 Another Tricky One (TDZ)

```js
let x = 1;

function test() {
  console.log(x);
  let x = 2;
}

test();
```

### Output:

```
ReferenceError
```

Because:

* `let x` inside `test` creates TDZ
* Accessing before initialization is illegal

---

# 🔬 Execution Phases (Very Important)

JavaScript runs in two phases:

### 1️⃣ Creation Phase

* Memory is allocated
* Declarations are registered
* `var` → undefined
* `let/const` → uninitialized (TDZ)
* Functions → fully stored

### 2️⃣ Execution Phase

* Code runs line by line
* Variables get assigned
* Functions execute

---

# 🎯 Key Mental Model

Instead of thinking:

> "JavaScript moves code up"

Think:

> "JavaScript registers declarations before running the code"

---

# 🧠 Real-World Best Practices

✔ Prefer `let` and `const`
✔ Avoid `var`
✔ Define functions before using them (even though hoisting allows it)
✔ Avoid relying on hoisting — write predictable code

---

# 🚀 Final Concept Summary

* **Function declarations** are fully hoisted.
* **`var` variables** are hoisted and initialized to `undefined`.
* **`let` and `const`** are hoisted but live in the **Temporal Dead Zone**.
* **Function expressions and arrow functions** follow variable hoisting rules.
* Hoisting happens during the **creation phase** of execution.

---

# 🔥 Closures in JavaScript — Complete & Deep Explanation

# 1️⃣ What Is a Closure?

### 📌 Precise Definition

A **closure** is:

> A function that remembers and can access variables from its **lexical (outer) scope**, even after that outer function has finished executing.

---

### Simple Example

```js
function outer() {
  let count = 0;

  function inner() {
    count++;
    console.log(count);
  }

  return inner;
}

const counter = outer();
counter(); // 1
counter(); // 2
```

### Why does this work?

* `outer()` creates `count`
* `inner()` references `count`
* `outer()` finishes
* Normally, `count` should disappear
* But it does not

Because:

👉 `inner` closes over the variable `count`

That preserved relationship is a **closure**.

---

# 2️⃣ Closures Are Created When Functions Are Defined

Important concept:

Closures are created at **function creation time**, not when the function runs.

Example:

```js
function outer() {
  let x = 10;

  return function inner() {
    console.log(x);
  };
}
```

When `inner` is defined:

* JavaScript stores:

  * Function code
  * Reference to outer lexical environment

That stored reference = closure.

---

# 3️⃣ How Closures Actually Work Internally

When a function is created, JavaScript attaches a hidden property:

```
[[Environment]]
```

It points to the outer lexical environment.

So internally:

```
inner = {
  code: function() { console.log(x); },
  [[Environment]]: reference to outer scope
}
```

When `inner()` runs:

1. It looks for `x`
2. Not found inside itself
3. Goes to outer environment
4. Finds `x`
5. Uses it

That lookup chain is called the **scope chain**.

---

# 4️⃣ Closures Do NOT Copy Values

Common misconception:

Closures **do not copy variable values**.

They store references to variables.

Example:

```js
function outer() {
  let x = 10;

  return function() {
    console.log(x);
  };
}

const fn = outer();
```

If `x` changes before calling `fn`, the updated value is used.

Closures reference the live variable.

---

# 5️⃣ Closures Preserve State

Closures allow variables to persist between function calls.

Example:

```js
function createCounter() {
  let count = 0;

  return function() {
    count++;
    return count;
  };
}

const counter = createCounter();

console.log(counter()); // 1
console.log(counter()); // 2
console.log(counter()); // 3
```

Why?

Because `count` remains in memory as long as `counter` exists.

---

# 6️⃣ Each Closure Has Its Own Memory

Example:

```js
function createCounter() {
  let count = 0;

  return function() {
    return ++count;
  };
}

const c1 = createCounter();
const c2 = createCounter();

console.log(c1()); // 1
console.log(c1()); // 2
console.log(c2()); // 1
```

Each call to `createCounter()` creates:

* A new lexical environment
* A new `count`
* A new closure

They do not share state.

---

# 7️⃣ Closures in Loops (Very Important)

### Problem with `var`

```js
for (var i = 1; i <= 3; i++) {
  setTimeout(function() {
    console.log(i);
  }, 1000);
}
```

Output:

```
4
4
4
```

Why?

* `var` creates one shared `i`
* All callbacks close over the same variable
* After loop ends, `i = 4`
* All print 4

---

### Fix with `let`

```js
for (let i = 1; i <= 3; i++) {
  setTimeout(function() {
    console.log(i);
  }, 1000);
}
```

Output:

```
1
2
3
```

Why?

* `let` creates new binding per iteration
* Each closure gets its own `i`

---

# 8️⃣ Closures in Asynchronous Code

Closures are heavily used in async programming.

Example:

```js
function delayedMessage(msg) {
  setTimeout(function() {
    console.log(msg);
  }, 1000);
}

delayedMessage("Hello");
```

Even after `delayedMessage` finishes:

* `msg` remains accessible
* Because the callback closes over it

Without closures, async JavaScript wouldn't work.

---

# 9️⃣ Closures Enable Data Privacy

Closures allow variables to be hidden from outside.

Example:

```js
function createAccount(balance) {
  return {
    deposit(amount) {
      balance += amount;
    },
    getBalance() {
      return balance;
    }
  };
}

const account = createAccount(100);
account.deposit(50);
console.log(account.getBalance()); // 150
```

You cannot access `balance` directly.

This is true private state.

---

# 🔟 Closures and Memory

Normally:

* When a function finishes → variables are removed from memory.

But if:

* An inner function still references them → they remain.

Example:

```js
function outer() {
  let largeData = new Array(1000000);

  return function() {
    console.log("Using closure");
  };
}
```

`largeData` stays in memory because of closure.

If closures hold large unused data → memory leaks can occur.

---

# 1️⃣1️⃣ Closures Inside Closures

Closures can stack.

```js
function a() {
  let x = 1;

  return function b() {
    let y = 2;

    return function c() {
      console.log(x, y);
    };
  };
}

a()()();
```

Output:

```
1 2
```

`c` closes over:

* `y` from `b`
* `x` from `a`

Multiple layers are preserved.

---

# 1️⃣2️⃣ Closures vs `this`

Closures capture variables from lexical scope.

They do NOT capture `this`.

`this` depends on how the function is called.

Closures = lexical scope
`this` = dynamic binding

They are separate concepts.

---

# 1️⃣3️⃣ Common Interview Traps

---

## Trap 1

```js
function test() {
  let x = 5;

  return function() {
    console.log(x);
  };
}

let x = 100;
const fn = test();
fn();
```

Output:

```
5
```

Because closures use lexical scope, not global lookup at call time.

---

## Trap 2

```js
function outer() {
  let x = 10;

  return function() {
    x++;
    console.log(x);
  };
}

const fn = outer();
fn();
fn();
```

Output:

```
11
12
```

Because closure keeps same reference.

---

# 1️⃣4️⃣ Why Closures Are Important

Closures are fundamental for:

* State management
* Async programming
* Event handlers
* Callbacks
* Functional programming
* Memoization
* Currying
* Module patterns
* Data privacy

Without closures, JavaScript would not work the way it does.

---

# 🔥 Final Mental Model

A closure is:

```
Function
+ Reference to outer lexical environment
+ That environment persists as long as the function exists
```

---

# 🎯 Ultimate One-Line Definition

> A closure is formed when a function retains access to variables from its lexical scope, even after the outer function has finished execution.

---

# 🔥 Callback Functions in JavaScript — Clear, In-Depth, Complete Guide

This explanation will build callbacks from the ground up and explain **how they really work internally**, not just what they are.

---

# 1️⃣ What Is a Callback Function?

### 📌 Simple Definition

A **callback function** is:

> A function that is passed as an argument to another function and is executed later.

That’s it at the core.

---

### Basic Example

```js
function greet(name) {
  console.log("Hello " + name);
}

function processUser(callback) {
  const name = "Alice";
  callback(name);
}

processUser(greet);
```

### What happens step by step:

1. `greet` is passed into `processUser`
2. Inside `processUser`, we call `callback(name)`
3. That executes `greet("Alice")`

So:

* `greet` is the callback
* `processUser` is a higher-order function

---

# 2️⃣ Why Do Callbacks Exist?

Callbacks exist because:

JavaScript functions are **first-class citizens**.

That means:

* Functions can be stored in variables
* Passed as arguments
* Returned from other functions

So instead of writing:

```js
function doSomething() {
  console.log("Task finished");
}
```

We allow flexibility:

```js
function doSomething(callback) {
  callback();
}
```

Now behavior becomes dynamic.

---

# 3️⃣ How JavaScript Treats Functions

When you pass:

```js
processUser(greet);
```

You are NOT calling `greet`.

You are passing a **reference** to it.

It’s like giving another function the ability to execute it later.

---

# 4️⃣ Synchronous Callbacks

These run immediately.

Example:

```js
[1, 2, 3].forEach(function(num) {
  console.log(num);
});
```

What happens:

1. `forEach` loops
2. For each item, it calls the callback immediately
3. Execution stays in the same call stack

No delay.

---

### Another Example

```js
function calculate(a, b, operation) {
  return operation(a, b);
}

calculate(5, 3, function(x, y) {
  return x + y;
});
```

The callback runs instantly.

---

# 5️⃣ Asynchronous Callbacks (Important)

These run later.

Example:

```js
setTimeout(function() {
  console.log("Hello");
}, 1000);
```

The callback executes after 1 second.

But how?

This requires understanding the **event loop**.

---

# 6️⃣ Event Loop + Callback Queue (Deep Explanation)

JavaScript is:

* Single-threaded
* Synchronous by default

So how does async work?

Through:

1. Call Stack
2. Web APIs
3. Callback Queue
4. Event Loop

---

### Example

```js
console.log("Start");

setTimeout(function() {
  console.log("Timeout");
}, 0);

console.log("End");
```

### Step-by-step execution

#### 1️⃣ Call Stack:

* `console.log("Start")`
* Output → Start

#### 2️⃣ `setTimeout`

* Sent to Web API
* Timer starts
* Callback stored

#### 3️⃣ `console.log("End")`

* Output → End

#### 4️⃣ Timer completes

* Callback moves to Callback Queue

#### 5️⃣ Event Loop checks:

* Is Call Stack empty?
* Yes → Push callback to stack

#### 6️⃣ Execute callback

* Output → Timeout

Final Output:

```
Start
End
Timeout
```

Even with `0ms`, it waits until stack clears.

---

# 7️⃣ Error-First Callbacks (Node.js Pattern)

Node.js uses this format:

```js
function callback(error, result)
```

Example:

```js
function fetchData(callback) {
  const success = true;

  if (success) {
    callback(null, "Data loaded");
  } else {
    callback("Something went wrong", null);
  }
}

fetchData(function(err, data) {
  if (err) {
    console.error(err);
  } else {
    console.log(data);
  }
});
```

Pattern rule:

* First argument → error
* Second argument → success data

This ensures consistent error handling.

---

# 8️⃣ Callback Hell

When async callbacks are nested deeply:

```js
getUser(function(user) {
  getOrders(user, function(orders) {
    getItems(orders, function(items) {
      processItems(items, function(result) {
        console.log(result);
      });
    });
  });
});
```

Problems:

* Hard to read
* Hard to maintain
* Hard to debug
* Pyramid shape

This is called:

### ⚠️ Callback Hell

Solution:

* Promises
* Async/Await

---

# 9️⃣ Inversion of Control (Very Important Concept)

When you pass a callback:

You are giving control of your function to another function.

Example:

```js
setTimeout(myFunction, 1000);
```

You trust:

* It will call it once
* At the correct time
* With correct arguments

This is called:

### Inversion of Control

Problems:

* Callback might be called twice
* Might not be called
* Might be called with wrong data

This led to Promises being created.

---

# 🔟 Callbacks + Closures

Callbacks often use closures.

Example:

```js
function outer() {
  let count = 0;

  setTimeout(function() {
    count++;
    console.log(count);
  }, 1000);
}

outer();
```

The callback:

* Remembers `count`
* Even after `outer` finished

Because of closure.

---

# 1️⃣1️⃣ Common Mistakes

---

## ❌ Mistake 1: Calling Instead of Passing

Wrong:

```js
setTimeout(myFunction(), 1000);
```

This calls immediately.

Correct:

```js
setTimeout(myFunction, 1000);
```

---

## ❌ Mistake 2: Loop + var

```js
for (var i = 0; i < 3; i++) {
  setTimeout(function() {
    console.log(i);
  }, 1000);
}
```

Output:

```
3
3
3
```

Because all callbacks share same `i`.

---

# 1️⃣2️⃣ When Should You Use Callbacks?

Use callbacks when:

* You need to run code after something finishes
* You need dynamic behavior
* Handling async operations
* Event-driven programming

Examples:

* `addEventListener`
* `setTimeout`
* `setInterval`
* `fs.readFile`
* `fetch` (before promises)

---

# 🔥 Final Mental Model

A callback is:

```
A function passed into another function
so that it can be executed later,
either immediately (sync) or after an operation completes (async).
```

For async:

```
Call Stack → Web API → Callback Queue → Event Loop → Execution
```

---

# 🎯 Interview-Ready Definition

> A callback function is a function passed as an argument to another function, which is invoked after a task completes, enabling asynchronous and dynamic behavior in JavaScript.

---

# 🔥 Higher-Order Functions in JavaScript — Complete In-Depth Guide

# 1️⃣ What Is a Higher-Order Function?

### 📌 Definition

A **Higher-Order Function (HOF)** is:

> A function that either:
>
> * Takes one or more functions as arguments
> * Returns a function
> * Or both

---

### Why “Higher-Order”?

Because it operates on functions.

Functions become data.

---

# 2️⃣ Foundation: Functions Are First-Class Citizens

In JavaScript, functions can:

* Be stored in variables
* Be passed as arguments
* Be returned from other functions
* Be assigned to properties
* Be created dynamically

Example:

```js
const sayHello = function() {
  console.log("Hello");
};
```

Since functions behave like values, we can pass them around.

That’s what makes HOFs possible.

---

# 3️⃣ Type 1: Function Taking Another Function (Callback)

Example:

```js
function greet(name) {
  return "Hello " + name;
}

function processUser(name, callback) {
  return callback(name);
}

processUser("Alice", greet);
```

Here:

* `processUser` is a Higher-Order Function
* `greet` is the callback

---

# 4️⃣ Type 2: Function Returning Another Function

Example:

```js
function multiplyBy(x) {
  return function(y) {
    return x * y;
  };
}

const double = multiplyBy(2);
console.log(double(5)); // 10
```

Here:

* `multiplyBy` is a Higher-Order Function
* It returns a new function
* Closure preserves `x`

---

# 5️⃣ How Higher-Order Functions Work Internally

When you pass a function:

```js
someFunction(callback);
```

You are passing:

* A reference to executable code

The receiving function decides:

* When to execute it
* How many times
* With what arguments

When returning a function:

```js
return function() {};
```

JavaScript creates a new function object and returns it.

If it references outer variables → closure is formed.

---

# 6️⃣ Built-In Higher-Order Functions (Very Important)

JavaScript provides many HOFs.

---

## 🔹 forEach()

```js
[1, 2, 3].forEach(function(num) {
  console.log(num);
});
```

Executes callback for each item.

---

## 🔹 map()

Transforms array.

```js
const numbers = [1, 2, 3];

const doubled = numbers.map(function(num) {
  return num * 2;
});

console.log(doubled); // [2, 4, 6]
```

Returns a new array.

---

## 🔹 filter()

Filters elements.

```js
const nums = [1, 2, 3, 4];

const evens = nums.filter(function(num) {
  return num % 2 === 0;
});

console.log(evens); // [2, 4]
```

---

## 🔹 reduce()

Reduces array to single value.

```js
const nums = [1, 2, 3, 4];

const sum = nums.reduce(function(acc, curr) {
  return acc + curr;
}, 0);

console.log(sum); // 10
```

---

# 7️⃣ Creating Your Own Higher-Order Function

Example:

```js
function repeat(n, action) {
  for (let i = 0; i < n; i++) {
    action(i);
  }
}

repeat(3, function(i) {
  console.log("Iteration:", i);
});
```

`repeat` is a Higher-Order Function.

---

# 8️⃣ Closures + Higher-Order Functions

Returning functions creates closures.

Example:

```js
function counter() {
  let count = 0;

  return function() {
    count++;
    return count;
  };
}

const c = counter();
console.log(c()); // 1
console.log(c()); // 2
```

The returned function:

* Is created by a HOF
* Uses closure to preserve state

---

# 9️⃣ Functional Programming Patterns

Higher-Order Functions enable functional programming.

---

## 🔹 Currying

Transform function into sequence of unary functions.

```js
function add(a) {
  return function(b) {
    return a + b;
  };
}

add(5)(3); // 8
```

---

## 🔹 Partial Application

```js
function greet(greeting) {
  return function(name) {
    return greeting + " " + name;
  };
}

const sayHello = greet("Hello");
console.log(sayHello("John"));
```

---

## 🔹 Function Composition

```js
function compose(f, g) {
  return function(x) {
    return f(g(x));
  };
}

const double = x => x * 2;
const square = x => x * x;

const doubleThenSquare = compose(square, double);

console.log(doubleThenSquare(3)); // 36
```

---

# 🔟 Real-World Use Cases

Higher-Order Functions are used in:

* Array transformations
* Event handling
* Middleware (Express.js)
* React hooks
* Async programming
* Data pipelines
* Validation systems

Example (event handling):

```js
button.addEventListener("click", function() {
  console.log("Clicked");
});
```

`addEventListener` is a Higher-Order Function.

---

# 1️⃣1️⃣ Performance Considerations

HOFs:

* Create new functions
* Can increase memory usage if overused
* May reduce readability if nested deeply

But:

They improve code clarity and reusability.

Modern engines optimize them efficiently.

---

# 1️⃣2️⃣ Common Interview Questions

---

## Question 1

What makes a function “higher-order”?

Answer:

It either accepts a function as an argument or returns a function.

---

## Question 2

Is `map()` a Higher-Order Function?

Yes.

Because it takes a function as argument.

---

## Question 3

What is the difference between callback and HOF?

* Callback → function passed into another function
* HOF → function that takes or returns another function

---

## Question 4

Explain HOF with example returning function.

```js
function multiplier(factor) {
  return function(number) {
    return number * factor;
  };
}
```

---

# 🔥 Mental Model

Higher-Order Function =

```
Function that operates on other functions
```

There are two patterns:

1️⃣ Takes function
2️⃣ Returns function

---

# 🎯 Final Interview Definition

> A Higher-Order Function is a function that either takes one or more functions as arguments or returns a function, enabling abstraction, reusability, and functional programming patterns in JavaScript.

---

In JavaScript, the **`this`** keyword is one of the most powerful—and misunderstood—features of the language.

At its core:

> **`this` refers to the object that is currently executing the function.**

But what `this` actually points to depends entirely on *how a function is called*, not where it is written.

Let’s break it down in depth.

---

# 1️⃣ The Global Context

In the global scope (outside any function):

* In browsers → `this` refers to `window`
* In Node.js → `this` refers to `module.exports` (not `global`)

### Browser Example:

```js
console.log(this); 
// window object (in browser)
```

If you declare:

```js
var name = "John";
console.log(this.name); // "John"
```

Because `var` attaches to `window` in browsers.

---

# 2️⃣ `this` Inside a Regular Function

## Case A: Non-Strict Mode

```js
function show() {
  console.log(this);
}

show();
```

In browsers:

```
window
```

Because when a regular function is called standalone, `this` defaults to the global object (in non-strict mode).

---

## Case B: Strict Mode

```js
"use strict";

function show() {
  console.log(this);
}

show();
```

Output:

```
undefined
```

In strict mode, `this` is `undefined` in standalone functions.

---

# 3️⃣ `this` Inside an Object Method

When a function is called as a method of an object:

```js
const user = {
  name: "Alice",
  greet: function() {
    console.log(this.name);
  }
};

user.greet(); // "Alice"
```

### Why?

Because the object before the dot (`user`) becomes `this`.

Rule:

> Whoever calls the function becomes `this`.

---

# 4️⃣ `this` and Function Borrowing

```js
const person1 = {
  name: "John",
  greet() {
    console.log(this.name);
  }
};

const person2 = {
  name: "Sarah"
};

person2.greet = person1.greet;
person2.greet(); // "Sarah"
```

Even though `greet` was written in `person1`, `this` depends on who calls it.

---

# 5️⃣ `this` in Arrow Functions ⚠️ (Very Important)

Arrow functions **DO NOT have their own `this`**.

They inherit `this` from their surrounding lexical scope.

### Example:

```js
const user = {
  name: "Mike",
  greet: () => {
    console.log(this.name);
  }
};

user.greet(); // undefined (or window.name in browser)
```

Why?

Because arrow functions capture `this` from where they are defined — not from who calls them.

---

### Correct Use Inside Object:

```js
const user = {
  name: "Mike",
  greet() {
    const inner = () => {
      console.log(this.name);
    };
    inner();
  }
};

user.greet(); // "Mike"
```

Here, the arrow function inherits `this` from `greet()`.

---

# 6️⃣ `this` Inside Constructor Functions

When using `new`, `this` refers to the newly created object.

```js
function Person(name) {
  this.name = name;
}

const p1 = new Person("Alice");
console.log(p1.name); // "Alice"
```

Rule:

> When a function is called with `new`, `this` becomes the new instance.

---

## Without `new` (Danger ⚠️)

```js
function Person(name) {
  this.name = name;
}

Person("Bob");
console.log(window.name); // "Bob" (in browser)
```

Because without `new`, it behaves like a regular function call.

---

# 7️⃣ `this` in Classes

Classes in JavaScript (introduced in ECMAScript 2015) are syntactic sugar over constructor functions.

```js
class Person {
  constructor(name) {
    this.name = name;
  }

  greet() {
    console.log(this.name);
  }
}

const p1 = new Person("Emma");
p1.greet(); // "Emma"
```

Same rule: `this` refers to the instance.

---

# 8️⃣ Controlling `this` Manually

JavaScript gives 3 powerful methods:

* `call()`
* `apply()`
* `bind()`

---

## `call()`

```js
function greet() {
  console.log(this.name);
}

const user = { name: "David" };

greet.call(user); // "David"
```

Immediately invokes function with specified `this`.

---

## `apply()`

Same as `call()` but arguments passed as array.

```js
function greet(age) {
  console.log(this.name, age);
}

greet.apply({ name: "Lisa" }, [25]);
```

---

## `bind()`

Returns a new function with fixed `this`.

```js
function greet() {
  console.log(this.name);
}

const user = { name: "Sam" };

const boundGreet = greet.bind(user);
boundGreet(); // "Sam"
```

---

# 9️⃣ `this` in Event Listeners (Browser)

```js
button.addEventListener("click", function() {
  console.log(this);
});
```

`this` refers to the element that received the event.

But:

```js
button.addEventListener("click", () => {
  console.log(this);
});
```

Arrow function → `this` is inherited (likely `window`).

---

# 🔟 `this` in setTimeout

```js
const user = {
  name: "Anna",
  greet() {
    setTimeout(function() {
      console.log(this.name);
    }, 1000);
  }
};

user.greet(); // undefined
```

Because `setTimeout` callback is a regular function → standalone call.

Fix with arrow function:

```js
setTimeout(() => {
  console.log(this.name);
}, 1000);
```

---

# 🔥 The 5 Golden Rules of `this`

1. **Global scope →** global object (or undefined in strict mode)
2. **Regular function call →** global object (or undefined in strict mode)
3. **Object method →** object before the dot
4. **Constructor (`new`) →** new instance
5. **Arrow function →** inherits `this` from outer scope

---

# 🧠 Advanced Concept: Execution Context

Every function call creates an execution context containing:

* Variable environment
* Scope chain
* `this` binding

`this` is determined at **call time**, not definition time (except arrow functions).

---

# 🆚 `this` vs `self` vs closures

Developers used to write:

```js
const self = this;
```

Before arrow functions existed.

Now arrow functions replace that pattern.

---

# ⚠️ Common Interview Trick

```js
const obj = {
  name: "Alex",
  greet() {
    return function() {
      console.log(this.name);
    };
  }
};

obj.greet()(); // ?
```

Answer:

```
undefined
```

Because returned function is standalone.

Fix:

```js
greet() {
  return () => {
    console.log(this.name);
  };
}
```

---

# 🚀 Summary

`this` is determined by:

* How a function is called
* Whether it’s strict mode
* Whether it’s an arrow function
* Whether it’s called with `new`
* Whether `call/apply/bind` is used

---

# 9️⃣ Immediately Invoked Function Expressions (IIFE)

An **IIFE** (Immediately Invoked Function Expression) is:

> A function that is **defined and executed immediately after it is created**.

It’s one of the most important historical patterns in JavaScript, especially before modules existed.

---

# 1️⃣ Basic Syntax

### Standard IIFE

```js
(function () {
  console.log("I run immediately!");
})();
```

Breakdown:

1. `function() {}` → Function definition
2. Wrapped in `()` → Turns it into an **expression**
3. Final `()` → Immediately invokes it

---

# 2️⃣ Why Do We Need the Parentheses?

JavaScript distinguishes between:

* **Function Declaration**
* **Function Expression**

This is invalid:

```js
function () {
  console.log("Hello");
}();
```

Because JS expects a function declaration to have a name.

So we wrap it:

```js
(function () {
  console.log("Hello");
})();
```

Now JavaScript treats it as a **function expression**, and expressions can be invoked immediately.

---

# 3️⃣ Alternative IIFE Syntax Variations

All of these work:

```js
(function () {})();

(function () {}());

!function () {}();

+function () {}();

void function () {}();
```

Why?

Because operators like `!`, `+`, `void` force the function into an expression.

However, the **first version is the standard and recommended style.**

---

# 4️⃣ IIFE with Parameters

You can pass arguments immediately:

```js
(function (name) {
  console.log("Hello " + name);
})("Alice");
```

Output:

```
Hello Alice
```

---

# 5️⃣ Why IIFEs Were So Important (Before ES6)

Before `let`, `const`, and ES6 modules (introduced in
ECMAScript 2015), JavaScript only had **function scope** and `var`.

There was **no block scope**.

This caused global variable pollution.

---

## 🔥 Problem Without IIFE

```js
var count = 10;

for (var i = 0; i < count; i++) {
  console.log(i);
}

console.log(i); // 10 😬
```

`i` leaks outside the loop.

---

## ✅ Fix Using IIFE

```js
(function () {
  var count = 10;

  for (var i = 0; i < count; i++) {
    console.log(i);
  }
})();

console.log(typeof count); // undefined
console.log(typeof i);     // undefined
```

Now variables are private.

---

# 6️⃣ IIFE Creates Private Scope

This is one of the biggest uses.

```js
const counter = (function () {
  let count = 0;

  return {
    increment() {
      count++;
      console.log(count);
    },
    decrement() {
      count--;
      console.log(count);
    }
  };
})();

counter.increment(); // 1
counter.increment(); // 2
```

### Why does this work?

Because of **closures**.

* The IIFE runs once.
* It returns an object.
* The returned methods still reference `count`.
* `count` is private — inaccessible from outside.

This pattern was heavily used in libraries like:

* jQuery
* Underscore.js

---

# 7️⃣ IIFE and Module Pattern

Before ES Modules, this was the main module pattern.

```js
const UserModule = (function () {
  let username = "Admin";

  function getUsername() {
    return username;
  }

  function setUsername(name) {
    username = name;
  }

  return {
    getUsername,
    setUsername
  };
})();
```

This is called:

> The Revealing Module Pattern

It allows:

* Private data
* Public API
* Encapsulation

---

# 8️⃣ IIFE and `this`

Inside an IIFE:

```js
(function () {
  console.log(this);
})();
```

* In non-strict mode → global object
* In strict mode → `undefined`

Safer version:

```js
(function () {
  "use strict";
})();
```

Many libraries wrapped everything in:

```js
(function (global) {
  // library code
})(this);
```

This safely passed the global object.

---

# 9️⃣ Arrow Function IIFE (Modern Style)

You can write:

```js
(() => {
  console.log("Arrow IIFE");
})();
```

Or with parameters:

```js
((name) => {
  console.log(name);
})("Alice");
```

However:

⚠️ Arrow IIFEs don’t have their own `this`.

---

# 🔟 Async IIFE (Very Powerful)

With `async/await`, IIFEs became useful again.

```js
(async function () {
  const data = await fetch("https://api.example.com");
  console.log("Fetched!");
})();
```

Why useful?

Because before top-level `await` was supported, this allowed async code at top level.

Even today, in some environments, async IIFEs are still used.

---

# 1️⃣1️⃣ IIFE vs Block Scope

Today, with `let` and `const`, we often don’t need IIFEs:

Instead of:

```js
(function () {
  var x = 10;
})();
```

We can write:

```js
{
  let x = 10;
}
```

Block scope replaces many IIFE use cases.

---

# 1️⃣2️⃣ When Should You Use IIFE Today?

### Still Useful For:

* Immediately executed setup code
* Creating one-time initialization logic
* Async wrapper
* Creating isolated scope in legacy code
* Avoiding global pollution in older environments

### Not Needed For:

* Module systems (ES Modules handle this)
* Block scoping (`let`, `const`)

---

# 🔥 Deep Understanding: Why It Works

JavaScript treats:

```
function foo() {}
```

as a declaration.

But:

```
(function foo() {})
```

as an expression.

And expressions can be:

* Assigned
* Passed
* Invoked immediately

---

# 🎯 Interview Trick

```js
var x = 10;

(function () {
  console.log(x);
  var x = 20;
})();
```

Output:

```
undefined
```

Why?

Because of **hoisting**:

Inside IIFE becomes:

```js
(function () {
  var x;
  console.log(x); // undefined
  x = 20;
})();
```

---

# 🧠 Mental Model

An IIFE is:

1. A function expression
2. Wrapped in parentheses
3. Immediately called
4. Creates a new scope
5. Can return values
6. Enables private state

---

# 🚀 Summary

An IIFE is:

* A design pattern
* Used for encapsulation
* Used for scope isolation
* Used heavily before ES6
* Still useful for async wrappers and initialization logic

---

# 🔟 Recursion (In-Depth Guide in JavaScript)

## 📌 What Is Recursion?

> **Recursion** is when a function calls itself to solve a smaller version of the same problem.

Instead of using loops, recursion breaks a problem into subproblems until it reaches a stopping condition.

---

# 1️⃣ The Two Essential Parts

Every recursive function MUST have:

### 1. Base Case

The condition that stops recursion.

### 2. Recursive Case

The part where the function calls itself with a smaller input.

---

## 🔹 Basic Example: Countdown

```js
function countdown(n) {
  if (n === 0) {        // ✅ Base case
    console.log("Done!");
    return;
  }

  console.log(n);
  countdown(n - 1);     // 🔁 Recursive call
}

countdown(5);
```

Output:

```
5
4
3
2
1
Done!
```

---

# 2️⃣ How Recursion Actually Works (Call Stack)

JavaScript uses a **call stack**.

Each function call:

* Gets pushed onto the stack
* Executes
* Gets popped off when finished

Let’s trace:

```js
function sum(n) {
  if (n === 1) return 1;
  return n + sum(n - 1);
}

sum(4);
```

### What happens internally:

```
sum(4)
→ 4 + sum(3)
    → 3 + sum(2)
        → 2 + sum(1)
            → 1 (base case)
```

Then it resolves backward:

```
2 + 1 = 3
3 + 3 = 6
4 + 6 = 10
```

Final result: `10`

---

# 3️⃣ Visualizing the Call Stack

```
sum(4)
sum(3)
sum(2)
sum(1)
```

Then stack unwinds:

```
sum(1) → returns 1
sum(2) → returns 3
sum(3) → returns 6
sum(4) → returns 10
```

This is called **stack unwinding**.

---

# 4️⃣ Factorial Example (Classic)

```
5! = 5 × 4 × 3 × 2 × 1
```

Recursive version:

```js
function factorial(n) {
  if (n === 0) return 1;     // Base case
  return n * factorial(n - 1);
}

console.log(factorial(5)); // 120
```

---

# 5️⃣ Recursion vs Loop

### Loop Version:

```js
function sumLoop(n) {
  let total = 0;
  for (let i = 1; i <= n; i++) {
    total += i;
  }
  return total;
}
```

### Recursive Version:

```js
function sumRec(n) {
  if (n === 1) return 1;
  return n + sumRec(n - 1);
}
```

### Comparison

| Loop                 | Recursion                |
| -------------------- | ------------------------ |
| Uses iteration       | Uses function calls      |
| Uses constant memory | Uses stack memory        |
| Usually faster       | Can cause stack overflow |

---

# 6️⃣ The Big Danger: Stack Overflow

If recursion doesn’t stop properly:

```js
function crash() {
  crash();
}

crash();
```

Error:

```
RangeError: Maximum call stack size exceeded
```

Because there is **no base case**.

---

# 7️⃣ Tail Recursion (Advanced)

Tail recursion happens when:

> The recursive call is the last thing executed.

Example:

```js
function sum(n, total = 0) {
  if (n === 0) return total;
  return sum(n - 1, total + n);
}
```

Here, nothing happens after the recursive call.

In theory, this allows **Tail Call Optimization (TCO)**.

TCO was specified in
ECMAScript 2015

However ⚠️

Most JavaScript engines (including V8 used in Node.js and Chrome) do **not** properly implement TCO.

So recursion still consumes stack memory.

---

# 8️⃣ Recursion with Arrays

## 🔹 Sum Array

```js
function sumArray(arr) {
  if (arr.length === 0) return 0;
  return arr[0] + sumArray(arr.slice(1));
}

console.log(sumArray([1, 2, 3, 4])); // 10
```

---

## 🔹 Flatten Array

```js
function flatten(arr) {
  let result = [];

  for (let item of arr) {
    if (Array.isArray(item)) {
      result = result.concat(flatten(item));
    } else {
      result.push(item);
    }
  }

  return result;
}

console.log(flatten([1, [2, [3, 4]], 5]));
// [1, 2, 3, 4, 5]
```

Recursion is powerful for nested structures.

---

# 9️⃣ Recursion with Objects (Tree Traversal)

Example: Nested category structure

```js
const tree = {
  name: "A",
  children: [
    { name: "B", children: [] },
    { 
      name: "C", 
      children: [{ name: "D", children: [] }] 
    }
  ]
};

function traverse(node) {
  console.log(node.name);
  for (let child of node.children) {
    traverse(child);
  }
}

traverse(tree);
```

Recursion is ideal for:

* Trees
* DOM traversal
* File systems
* Graphs

---

# 🔟 Fibonacci (Famous but Inefficient)

```js
function fib(n) {
  if (n <= 1) return n;
  return fib(n - 1) + fib(n - 2);
}
```

Problem:

This has **exponential time complexity**.

Better solution: Memoization.

---

# 1️⃣1️⃣ Memoization (Optimization)

```js
function memoFib(n, memo = {}) {
  if (n in memo) return memo[n];
  if (n <= 1) return n;

  memo[n] = memoFib(n - 1, memo) + memoFib(n - 2, memo);
  return memo[n];
}
```

Now time complexity becomes **O(n)** instead of **O(2ⁿ)**.

---

# 1️⃣2️⃣ When Should You Use Recursion?

✅ Good for:

* Tree structures
* Divide and conquer
* Backtracking
* Parsing
* Functional programming

❌ Avoid when:

* Very deep recursion
* Large datasets without TCO
* Performance-critical loops

---

# 🧠 Mental Model

Recursion works like:

> “Trust the function to solve a smaller version of the problem.”

Example:

To compute factorial(5), assume factorial(4) works.

---

# 🎯 Interview Patterns

Common recursion problems:

* Factorial
* Fibonacci
* Reverse string
* Palindrome check
* Binary tree traversal
* Merge sort
* Quick sort

---

# 🚀 Recursion vs Iteration — Deep Insight

Recursion is conceptually:

```
Problem → smaller problem → smaller problem → base case
```

Iteration is:

```
Repeat until condition met
```

Recursion expresses problems naturally when:

* The structure is recursive (trees)
* The solution depends on subproblems

---

# ⚡ Final Summary

Recursion:

* Calls itself
* Requires a base case
* Uses the call stack
* Can cause stack overflow
* Can be optimized with memoization
* Powerful for hierarchical data

---

# 1️⃣1️⃣ Function Methods in JavaScript (Deep Dive)

In JavaScript, **functions are objects**.

That means they:

* Can have properties
* Can have methods
* Can be passed around
* Can be modified

Because functions are objects, they come with powerful built-in methods.

The most important function methods are:

1. `call()`
2. `apply()`
3. `bind()`
4. `toString()`
5. `valueOf()`

Let’s go deep.

---

# 🔥 1️⃣ `call()`

## 📌 What It Does

`call()` invokes a function immediately and allows you to specify:

* What `this` should be
* Arguments individually

### Syntax

```js
functionName.call(thisArg, arg1, arg2, ...)
```

---

## 🔹 Basic Example

```js
function greet(age) {
  console.log(this.name, age);
}

const user = { name: "Alice" };

greet.call(user, 25);
```

Output:

```
Alice 25
```

Here:

* `this` becomes `user`
* Arguments passed normally

---

## 🔹 Function Borrowing

```js
const person1 = {
  name: "John",
  greet() {
    console.log("Hi " + this.name);
  }
};

const person2 = { name: "Sarah" };

person1.greet.call(person2);
// Hi Sarah
```

We borrowed `greet` from `person1`.

---

# 🔥 2️⃣ `apply()`

## 📌 What It Does

Same as `call()`, but arguments are passed as an array.

### Syntax

```js
functionName.apply(thisArg, [arg1, arg2])
```

---

## 🔹 Example

```js
function greet(age, city) {
  console.log(this.name, age, city);
}

const user = { name: "Bob" };

greet.apply(user, [30, "London"]);
```

Output:

```
Bob 30 London
```

---

## 🔹 Real-World Example (Math.max)

```js
const numbers = [5, 10, 2, 8];

const max = Math.max.apply(null, numbers);
console.log(max); // 10
```

Why `null`?

Because `Math.max` does not use `this`.

---

# 🔥 Difference Between `call()` and `apply()`

| Feature             | call()          | apply()       |
| ------------------- | --------------- | ------------- |
| Invokes immediately | ✅               | ✅             |
| Arguments format    | Comma-separated | Array         |
| Use case            | Known arguments | Dynamic array |

---

# 🔥 3️⃣ `bind()`

## 📌 What It Does

`bind()` does NOT execute immediately.

It returns a **new function** with `this` permanently set.

---

## 🔹 Example

```js
function greet() {
  console.log(this.name);
}

const user = { name: "Emma" };

const boundGreet = greet.bind(user);

boundGreet(); // Emma
```

---

## 🔹 Why `bind()` Is Important

Problem:

```js
const user = {
  name: "Alex",
  greet() {
    console.log(this.name);
  }
};

setTimeout(user.greet, 1000); 
// undefined 😬
```

Because `this` is lost.

Fix:

```js
setTimeout(user.greet.bind(user), 1000);
```

Now it works.

---

# 🔥 4️⃣ Hard Binding (bind Internals)

`bind()` creates a wrapper function:

```js
function bind(fn, obj) {
  return function() {
    return fn.apply(obj, arguments);
  };
}
```

That’s essentially what `bind()` does internally.

It was introduced in
ECMAScript 5

---

# 🔥 5️⃣ `toString()`

Returns function source code as string.

```js
function hello() {
  return "Hi";
}

console.log(hello.toString());
```

Output:

```
function hello() {
  return "Hi";
}
```

Sometimes used in debugging or metaprogramming.

---

# 🔥 6️⃣ `valueOf()`

Returns the function itself.

```js
function test() {}

console.log(test.valueOf() === test); // true
```

Rarely used directly.

---

# 🔥 7️⃣ Method Borrowing (Advanced Pattern)

You can borrow array methods:

```js
function showArgs() {
  const args = Array.prototype.slice.call(arguments);
  console.log(args);
}

showArgs(1, 2, 3);
```

Before ES6 rest parameters, this was common.

Now we use:

```js
function showArgs(...args) {
  console.log(args);
}
```

---

# 🔥 8️⃣ Constructor Binding Behavior

Important detail:

```js
function Person(name) {
  this.name = name;
}

const user = { name: "Fake" };

const BoundPerson = Person.bind(user);

const p = new BoundPerson("Real");

console.log(p.name); // "Real"
```

`new` overrides `bind()`.

Binding priority:

1. `new`
2. Explicit (`call`, `apply`, `bind`)
3. Implicit (object.method)
4. Default (global / undefined)

---

# 🔥 9️⃣ Partial Application with bind()

You can pre-fill arguments:

```js
function multiply(a, b) {
  return a * b;
}

const double = multiply.bind(null, 2);

console.log(double(5)); // 10
```

This is called **partial application**.

---

# 🔥 1️⃣0️⃣ Arrow Functions & Function Methods

Important:

Arrow functions:

* Do NOT have their own `this`
* Cannot change `this` with `call`, `apply`, or `bind`

Example:

```js
const arrow = () => {
  console.log(this);
};

arrow.call({ name: "Test" }); 
// still global or outer scope
```

Because arrow functions capture lexical `this`.

Arrow functions were introduced in
ECMAScript 2015

---

# 🔥 1️⃣1️⃣ Real Interview Scenario

```js
const obj = {
  name: "Sam",
  greet() {
    console.log(this.name);
  }
};

const fn = obj.greet;
fn(); 
```

Output:

```
undefined
```

Fix:

```js
const fn = obj.greet.bind(obj);
fn(); // Sam
```

---

# 🧠 Deep Understanding

Functions in JavaScript are instances of:

```js
Function
```

Meaning:

```js
function test() {}

console.log(test instanceof Function); // true
```

Because functions inherit from `Function.prototype`.

And that’s why they have:

* `call`
* `apply`
* `bind`

---

# 🚀 Summary

Function methods allow you to:

* Control `this`
* Borrow methods
* Create partially applied functions
* Fix lost context
* Manipulate execution

---

# 🎯 Quick Cheat Sheet

| Method  | Executes Immediately? | Sets `this`?    | Arguments       |
| ------- | --------------------- | --------------- | --------------- |
| call()  | ✅                     | Yes             | Comma-separated |
| apply() | ✅                     | Yes             | Array           |
| bind()  | ❌                     | Yes (permanent) | Comma-separated |

---

# 1️⃣2️⃣ Pure vs Impure Functions (Deep Dive)

Understanding pure vs impure functions is **fundamental to functional programming**, predictable code, and performance optimization.

---

# 🧼 What Is a Pure Function?

A **pure function** is a function that:

1. **Always returns the same output for the same input**
2. **Has no side effects**

That’s it. Only two rules.

---

## ✅ Rule 1: Same Input → Same Output

```js
function add(a, b) {
  return a + b;
}
```

```js
add(2, 3); // 5
add(2, 3); // 5
```

Always predictable.

---

## ✅ Rule 2: No Side Effects

A side effect is anything that:

* Modifies external variables
* Changes global state
* Modifies input parameters
* Makes API calls
* Writes to database
* Logs to console
* Changes DOM

Example of a pure function:

```js
function square(n) {
  return n * n;
}
```

It:

* Doesn't modify anything
* Doesn't depend on external data
* Just computes and returns

✔ Pure.

---

# 🔥 What Is an Impure Function?

An **impure function**:

* Violates at least one of the two rules.

---

## ❌ Example 1: Depends on External State

```js
let tax = 0.2;

function calculate(price) {
  return price + price * tax;
}
```

If `tax` changes:

```js
tax = 0.3;
```

Now same input → different output.

❌ Impure.

---

## ❌ Example 2: Modifies External Variable

```js
let count = 0;

function increment() {
  count++;
}
```

It changes external state.

❌ Impure.

---

## ❌ Example 3: Mutates Input

```js
function addItem(arr, item) {
  arr.push(item);
  return arr;
}
```

It modifies the original array.

❌ Impure.

---

# 🔄 Making Impure Code Pure

Instead of:

```js
function addItem(arr, item) {
  arr.push(item);
  return arr;
}
```

Do:

```js
function addItem(arr, item) {
  return [...arr, item];
}
```

Now:

* Original array untouched
* New array returned

✔ Pure.

---

# 🧠 Why Pure Functions Are Powerful

## 1️⃣ Predictable

You can reason about them easily.

## 2️⃣ Easy to Test

```js
expect(add(2, 3)).toBe(5);
```

No setup required.

## 3️⃣ No Hidden Dependencies

They don’t rely on outside state.

## 4️⃣ Enable Caching (Memoization)

```js
function memoize(fn) {
  const cache = {};
  return function(x) {
    if (cache[x]) return cache[x];
    cache[x] = fn(x);
    return cache[x];
  };
}
```

Only works correctly with pure functions.

---

# 🧬 Referential Transparency

Pure functions are **referentially transparent**.

Meaning:

You can replace the function call with its result without changing behavior.

Example:

```js
const result = add(2, 3);
```

You can replace `add(2, 3)` with `5` anywhere.

That’s not true for impure functions.

---

# 🌍 Real-World Impure Examples

Most real-world programs are impure:

* Fetching data
* Writing files
* Database updates
* Logging
* Reading time

Example:

```js
function getCurrentTime() {
  return new Date();
}
```

Impure because it depends on current system time.

---

# ⚡ Functional Programming & Purity

Libraries like:

* React
* Redux

Strongly encourage pure functions.

In Redux:

Reducers MUST be pure.

```js
function reducer(state, action) {
  switch (action.type) {
    case "ADD":
      return [...state, action.payload];
    default:
      return state;
  }
}
```

No mutation allowed.

---

# 🔥 Hidden Impurity Examples

### Console Logging

```js
function greet(name) {
  console.log(name);
}
```

Logging is a side effect.

Technically impure.

---

### Random Numbers

```js
function getRandom() {
  return Math.random();
}
```

Same input (none) → different output.

Impure.

---

# 🧩 Pure Functions with Objects

Objects don’t automatically make functions impure.

This is pure:

```js
function getFullName(user) {
  return user.first + " " + user.last;
}
```

This is impure:

```js
function updateName(user) {
  user.first = "New";
}
```

Mutation = impurity.

---

# 🔥 Deep Concept: Immutability

Purity often pairs with:

> Immutability — never modifying existing data.

Instead of:

```js
arr.push(4);
```

Do:

```js
const newArr = [...arr, 4];
```

---

# ⚖️ Pure vs Impure Comparison

| Feature                  | Pure | Impure           |
| ------------------------ | ---- | ---------------- |
| Same input → same output | ✅    | ❌                |
| Side effects             | ❌    | ✅                |
| Modifies external state  | ❌    | ✅                |
| Easy to test             | ✅    | Harder           |
| Predictable              | ✅    | Less predictable |

---

# 🏗 Real-World Strategy

You cannot build real apps with only pure functions.

Instead:

> Isolate impurity at the edges.

Example architecture:

```
[API / DB / DOM] → Impure Layer
        ↓
    Pure Logic Layer
```

Keep business logic pure.

---

# 🎯 Interview Trick

```js
let x = 10;

function foo(a) {
  return a + x;
}
```

Is it pure?

❌ No.

Because if `x` changes, result changes.

---

# 🧠 Mental Model

Pure function:

> "Math-like function"

Impure function:

> "Does something in the world"

---

# 🚀 Summary

A function is pure if:

1. Same input → same output
2. No side effects

Purity gives:

* Predictability
* Testability
* Performance optimizations
* Cleaner architecture

Impurity is unavoidable — but should be controlled.

---

# 1️⃣3️⃣ Currying (Deep Dive in JavaScript)

Currying is one of the most powerful functional programming techniques in JavaScript.

---

# 🧠 What Is Currying?

> **Currying is transforming a function that takes multiple arguments into a sequence of functions that each take one argument.**

Instead of:

```js
f(a, b, c)
```

We transform it into:

```js
f(a)(b)(c)
```

---

# 1️⃣ Basic Example

### Normal Function

```js
function add(a, b) {
  return a + b;
}

add(2, 3); // 5
```

### Curried Version

```js
function curriedAdd(a) {
  return function (b) {
    return a + b;
  };
}

curriedAdd(2)(3); // 5
```

Each function takes **one argument** and returns another function until all arguments are collected.

---

# 2️⃣ Why Currying Is Useful

Currying enables:

* Partial application
* Reusability
* Cleaner functional pipelines
* Configuration-first design
* Better composition

---

# 3️⃣ Real Power: Partial Application

```js
function multiply(a) {
  return function (b) {
    return a * b;
  };
}

const double = multiply(2);
const triple = multiply(3);

double(5); // 10
triple(5); // 15
```

We “locked in” part of the function.

---

# 4️⃣ Arrow Function Version (Modern Style)

```js
const add = a => b => c => a + b + c;

add(1)(2)(3); // 6
```

This is very common in modern JavaScript (introduced in
ECMAScript 2015).

---

# 5️⃣ Currying vs Partial Application

They are related but not identical.

### Currying:

Transforms:

```js
f(a, b, c)
```

into:

```js
f(a)(b)(c)
```

### Partial Application:

Fixes some arguments early:

```js
const add = (a, b, c) => a + b + c;

const add5 = add.bind(null, 5);

add5(10, 20); // 35
```

Currying always produces unary (one-argument) functions.

Partial application does not require that.

---

# 6️⃣ Manual Curry Utility Function

Let’s build a generic curry function.

```js
function curry(fn) {
  return function curried(...args) {
    if (args.length >= fn.length) {
      return fn.apply(this, args);
    } else {
      return function (...nextArgs) {
        return curried.apply(this, args.concat(nextArgs));
      };
    }
  };
}
```

---

## 🔹 Using It

```js
function sum(a, b, c) {
  return a + b + c;
}

const curriedSum = curry(sum);

curriedSum(1)(2)(3);     // 6
curriedSum(1, 2)(3);     // 6
curriedSum(1)(2, 3);     // 6
```

This works because:

* `fn.length` tells how many parameters original function expects.
* We collect arguments until we have enough.

---

# 7️⃣ Currying in Functional Programming

Currying is foundational in functional languages like:

* Haskell

In fact, in Haskell:

> All functions are automatically curried.

JavaScript does not automatically curry functions, but supports it naturally.

---

# 8️⃣ Practical Real-World Use Case

### Example: Logging Utility

```js
const log = level => message => {
  console.log(`[${level}] ${message}`);
};

const info = log("INFO");
const error = log("ERROR");

info("App started");
error("Something broke");
```

Cleaner, configurable, reusable.

---

# 9️⃣ Currying and Function Composition

Currying works beautifully with composition.

```js
const multiply = a => b => a * b;
const add = a => b => a + b;

const double = multiply(2);
const increment = add(1);

increment(double(5)); // 11
```

This pattern is common in libraries like:

* Lodash
* Ramda

Ramda heavily uses currying.

---

# 🔟 Currying and React

In React, currying is often used in event handlers:

```js
const handleChange = field => event => {
  console.log(field, event.target.value);
};

<input onChange={handleChange("email")} />
```

We pass a configured handler.

---

# 1️⃣1️⃣ Common Interview Example

Transform this:

```js
function sum(a, b, c) {
  return a + b + c;
}
```

Into:

```js
sum(1)(2)(3)
```

Answer:

```js
const sum = a => b => c => a + b + c;
```

---

# 1️⃣2️⃣ Advanced: Infinite Currying

```js
function add(a) {
  return function (b) {
    if (b !== undefined) {
      return add(a + b);
    }
    return a;
  };
}

add(1)(2)(3)(4)(); // 10
```

It keeps collecting values until called with no argument.

---

# 1️⃣3️⃣ When NOT to Use Currying

Avoid currying when:

* It reduces readability
* Team unfamiliar with functional style
* Simple function works fine
* Performance-critical inner loops

---

# 🔥 Mental Model

Currying turns:

```js
f(a, b, c)
```

Into:

```js
f(a) → returns f(b) → returns f(c) → result
```

Think of it as:

> “One argument at a time.”

---

# ⚡ Advantages

* Cleaner abstraction
* Reusable configurations
* Functional composition
* Avoid repeated parameters
* Better testability

---

# 🚀 Summary

Currying:

* Transforms multi-argument function → chain of unary functions
* Enables partial application
* Supports functional programming
* Used heavily in modern JS libraries
* Improves composability

---

# 1️⃣4️⃣ Function Composition (Deep Dive)

Function composition is one of the core ideas of functional programming.

---

# 🧠 What Is Function Composition?

> **Function composition is combining multiple functions to create a new function.**

Instead of writing:

```js
const result = add1(double(square(x)));
```

We create a pipeline:

```js
const transform = compose(add1, double, square);
transform(x);
```

---

# 📌 Mathematical Idea

In math:

```
f(g(x))
```

Means:

1. Run `g(x)`
2. Pass result into `f`

That’s composition.

---

# 1️⃣ Basic Example

```js
const double = x => x * 2;
const square = x => x * x;
const add1 = x => x + 1;
```

Without composition:

```js
add1(double(square(2))); // 9
```

Step by step:

```
square(2) → 4
double(4) → 8
add1(8) → 9
```

---

# 2️⃣ Building a `compose()` Function

Composition runs **right → left**.

```js
function compose(...fns) {
  return function (value) {
    return fns.reduceRight((acc, fn) => fn(acc), value);
  };
}
```

---

## 🔹 Using It

```js
const transform = compose(add1, double, square);

transform(2); // 9
```

Execution order:

```
square → double → add1
```

---

# 3️⃣ `pipe()` (Left to Right)

Some developers prefer left-to-right readability.

```js
function pipe(...fns) {
  return function (value) {
    return fns.reduce((acc, fn) => fn(acc), value);
  };
}
```

Usage:

```js
const transform = pipe(square, double, add1);
transform(2); // 9
```

Now it reads naturally:

```
square → double → add1
```

---

# 4️⃣ Why Composition Is Powerful

Composition allows:

* Cleaner code
* Reusability
* Predictable transformations
* Functional pipelines
* No intermediate variables

---

# 5️⃣ Real-World Example

Imagine processing user input:

```js
const trim = str => str.trim();
const toLower = str => str.toLowerCase();
const removeSpaces = str => str.replace(/\s+/g, "");
```

Compose:

```js
const cleanInput = pipe(trim, toLower, removeSpaces);

cleanInput("  Hello World  "); 
// "helloworld"
```

---

# 6️⃣ Composition + Currying

Composition works best with **curried functions**.

Currying was introduced in functional languages like
Haskell

JavaScript adopted the pattern widely after
ECMAScript 2015

Example:

```js
const multiply = a => b => a * b;
const add = a => b => a + b;

const double = multiply(2);
const increment = add(1);

const transform = compose(increment, double);

transform(5); // 11
```

---

# 7️⃣ Composition in Real Libraries

Libraries that use heavy composition:

* Lodash
* Ramda

Example in Ramda:

```js
R.compose(add1, double, square);
```

Ramda functions are automatically curried, making composition smooth.

---

# 8️⃣ Composition in React

In React, higher-order components (HOCs) often use composition:

```js
compose(
  withRouter,
  connect(mapState),
  memo
)(MyComponent);
```

Each function enhances the component.

---

# 9️⃣ Composition with Arrays

You can compose array transformations:

```js
const double = x => x * 2;
const isEven = x => x % 2 === 0;

const process = arr =>
  arr
    .map(double)
    .filter(isEven);

process([1, 2, 3, 4]);
// [4, 8]
```

This is pipeline-style composition.

---

# 🔟 Composition vs Nested Calls

Without composition:

```js
const result = add1(double(square(x)));
```

Harder to read when long.

With composition:

```js
const transform = compose(add1, double, square);
transform(x);
```

Reusable and cleaner.

---

# 1️⃣1️⃣ Key Requirement: Pure Functions

Composition works best with **pure functions**.

Why?

Because:

* No side effects
* Predictable outputs
* Safe chaining

If functions mutate data, composition becomes unreliable.

---

# 1️⃣2️⃣ Advanced: Composing Multiple Arguments

Basic compose assumes one argument.

To support multiple:

```js
function compose(...fns) {
  return function (...args) {
    return fns.reduceRight(
      (acc, fn, index) =>
        index === fns.length - 1
          ? fn(...acc)
          : fn(acc),
      args
    );
  };
}
```

But most functional pipelines use unary functions.

---

# 🔥 Mental Model

Composition is like:

```
Raw Data → Step1 → Step2 → Step3 → Final Result
```

Each function:

* Receives data
* Transforms it
* Returns new data

---

# ⚡ Composition vs Inheritance

Composition in functional programming is different from OOP composition.

But both share idea:

> Build complex behavior by combining smaller pieces.

Functional composition focuses on **data transformation pipelines**.

---

# 🧠 Big Idea

Instead of:

```js
let result = x;
result = square(result);
result = double(result);
result = add1(result);
```

We write:

```js
const transform = pipe(square, double, add1);
```

Declarative > Imperative.

---

# 🚀 Summary

Function composition:

* Combines small functions into one
* Enables pipelines
* Encourages pure functions
* Works beautifully with currying
* Improves readability and reuse
* Common in modern functional libraries

---

# 1️⃣5️⃣ Generators (Deep Dive in JavaScript)

Generators are one of the most powerful — and underused — features in JavaScript.

They were introduced in
ECMAScript 2015.

---

# 🧠 What Is a Generator?

> A **generator** is a special type of function that can pause execution and resume later.

Normal functions:

* Run once
* Return one value
* Finish execution

Generators:

* Can pause (`yield`)
* Resume later
* Produce multiple values over time
* Maintain internal state between pauses

---

# 1️⃣ Basic Syntax

A generator function is defined using `function*`:

```js
function* myGenerator() {
  yield 1;
  yield 2;
  yield 3;
}
```

Calling it does NOT execute it immediately.

```js
const gen = myGenerator();
```

It returns a **generator object (iterator)**.

---

# 2️⃣ How `yield` Works

`yield`:

* Pauses the function
* Returns a value
* Saves execution state

Example:

```js
function* numbers() {
  console.log("Start");
  yield 1;
  console.log("Middle");
  yield 2;
  console.log("End");
}
```

Using it:

```js
const gen = numbers();

console.log(gen.next());
console.log(gen.next());
console.log(gen.next());
console.log(gen.next());
```

Output:

```js
Start
{ value: 1, done: false }

Middle
{ value: 2, done: false }

End
{ value: undefined, done: true }
```

---

# 3️⃣ Understanding `.next()`

Each call to:

```js
gen.next();
```

Returns an object:

```js
{ value: something, done: boolean }
```

* `value` → yielded value
* `done` → whether generator finished

---

# 4️⃣ Generator Execution Flow

Imagine this:

```js
function* demo() {
  yield "A";
  yield "B";
  yield "C";
}
```

Execution timeline:

```text
Call demo() → returns generator
next() → "A"
next() → "B"
next() → "C"
next() → done
```

It behaves like a **controlled pause/resume machine**.

---

# 5️⃣ Generators Are Iterators

Generators automatically implement the iterator protocol.

That means they work with:

* `for...of`
* Spread operator
* `Array.from()`

Example:

```js
function* nums() {
  yield 10;
  yield 20;
  yield 30;
}

for (let n of nums()) {
  console.log(n);
}
```

Output:

```js
10
20
30
```

---

# 6️⃣ Infinite Sequences (Very Powerful)

Generators can produce infinite data safely.

```js
function* infiniteCounter() {
  let i = 0;
  while (true) {
    yield i++;
  }
}

const counter = infiniteCounter();

console.log(counter.next().value); // 0
console.log(counter.next().value); // 1
console.log(counter.next().value); // 2
```

It doesn’t crash because values are generated lazily.

---

# 7️⃣ Passing Values INTO Generators

Generators can receive values via `next()`.

```js
function* greet() {
  const name = yield "What is your name?";
  yield `Hello ${name}`;
}

const gen = greet();

console.log(gen.next().value);
console.log(gen.next("Alice").value);
```

Output:

```js
What is your name?
Hello Alice
```

The value passed to `next()` becomes the result of `yield`.

---

# 8️⃣ Generator Return vs Yield

`yield` → pause and send value
`return` → finish generator

```js
function* test() {
  yield 1;
  return 2;
  yield 3; // never runs
}
```

After `return`, `done` becomes `true`.

---

# 9️⃣ `yield*` (Delegating to Another Generator)

You can delegate to another generator.

```js
function* genA() {
  yield 1;
  yield 2;
}

function* genB() {
  yield* genA();
  yield 3;
}

[...genB()]; // [1, 2, 3]
```

`yield*` flattens another iterator into the current one.

---

# 🔟 Real-World Use Case: Custom Iterable

```js
const range = {
  from: 1,
  to: 5,
  *[Symbol.iterator]() {
    for (let i = this.from; i <= this.to; i++) {
      yield i;
    }
  }
};

console.log([...range]); // [1,2,3,4,5]
```

Generators make objects iterable easily.

---

# 1️⃣1️⃣ Generators and Async (Historical Importance)

Before `async/await`, generators were used for async flow control.

Libraries like:

* Redux (Redux-Saga)
* Express.js middleware ecosystems

Used generator-based async patterns.

Example pattern (simplified):

```js
function* fetchData() {
  const data = yield fetch("/api");
  console.log(data);
}
```

Later replaced mostly by `async/await`.

---

# 1️⃣2️⃣ Generators vs Normal Functions

| Feature            | Normal Function | Generator |
| ------------------ | --------------- | --------- |
| Runs immediately   | ✅               | ❌         |
| Can pause          | ❌               | ✅         |
| Multiple values    | ❌               | ✅         |
| Maintains state    | ❌               | ✅         |
| Infinite sequences | ❌               | ✅         |

---

# 1️⃣3️⃣ When Should You Use Generators?

✅ Good for:

* Lazy evaluation
* Infinite data streams
* Custom iterators
* Complex state machines
* Controlling async flows
* Middleware engines

❌ Avoid when:

* Simple loops work fine
* You don’t need pause/resume

---

# 1️⃣4️⃣ Mental Model

A generator is like:

> A function that remembers where it left off.

Each `yield`:

* Saves memory state
* Suspends execution
* Waits for next call

---

# 1️⃣5️⃣ Advanced: Generator as State Machine

```js
function* trafficLight() {
  while (true) {
    yield "Green";
    yield "Yellow";
    yield "Red";
  }
}
```

Each call cycles state without external variables.

---

# 🚀 Summary

Generators:

* Use `function*`
* Use `yield` to pause
* Return iterator objects
* Maintain internal state
* Can create infinite sequences
* Work with `for...of`
* Support delegation via `yield*`

They provide:

* Lazy evaluation
* Controlled execution
* Powerful iteration patterns

---

# 1️⃣6️⃣ Async Functions (Deep Dive in JavaScript)

Async functions are one of the most important modern JavaScript features.

They were introduced in
ECMAScript 2017.

They provide a **cleaner way to work with Promises**.

---

# 🧠 What Is an Async Function?

An async function is declared with the `async` keyword:

```js
async function example() {
  return "Hello";
}
```

Key rule:

> An async function ALWAYS returns a Promise.

Even if you return a normal value.

---

# 1️⃣ Async Function Always Returns a Promise

```js
async function greet() {
  return "Hello";
}

console.log(greet());
```

Output:

```js
Promise { "Hello" }
```

JavaScript automatically wraps the return value inside a Promise.

Equivalent to:

```js
function greet() {
  return Promise.resolve("Hello");
}
```

---

# 2️⃣ The `await` Keyword

`await` can only be used inside async functions.

It:

* Pauses execution
* Waits for a Promise to resolve
* Returns resolved value

---

## 🔹 Basic Example

```js
function getData() {
  return new Promise(resolve => {
    setTimeout(() => resolve("Data received"), 1000);
  });
}

async function fetchData() {
  const result = await getData();
  console.log(result);
}

fetchData();
```

Execution:

1. `await` pauses `fetchData`
2. Promise resolves
3. Execution resumes

---

# 3️⃣ Async vs Then()

Without async/await:

```js
getData()
  .then(result => {
    console.log(result);
  })
  .catch(error => {
    console.error(error);
  });
```

With async/await:

```js
async function fetchData() {
  try {
    const result = await getData();
    console.log(result);
  } catch (error) {
    console.error(error);
  }
}
```

Cleaner, more readable.

---

# 4️⃣ Error Handling

If a Promise rejects:

```js
function fail() {
  return Promise.reject("Something went wrong");
}
```

Handle with try/catch:

```js
async function test() {
  try {
    await fail();
  } catch (err) {
    console.log(err);
  }
}
```

Async/await uses normal try/catch — very powerful.

---

# 5️⃣ Sequential vs Parallel Execution

## 🔹 Sequential (Slower)

```js
async function run() {
  const a = await getData1();
  const b = await getData2();
}
```

`getData2()` waits for `getData1()`.

---

## 🔹 Parallel (Faster)

```js
async function run() {
  const p1 = getData1();
  const p2 = getData2();

  const a = await p1;
  const b = await p2;
}
```

Even better:

```js
const [a, b] = await Promise.all([getData1(), getData2()]);
```

---

# 6️⃣ Await Only Works with Promises

If you await a non-Promise:

```js
async function test() {
  const value = await 5;
  console.log(value);
}
```

It automatically becomes:

```js
Promise.resolve(5)
```

---

# 7️⃣ Async Arrow Functions

```js
const fetchData = async () => {
  const data = await getData();
  return data;
};
```

Works exactly the same.

---

# 8️⃣ Async Functions and the Event Loop

Important:

`await` does NOT block the thread.

It pauses only that function.

JavaScript continues running other tasks in the:

* Call stack
* Task queue
* Microtask queue

Async/await is built on top of Promises and the event loop.

---

# 9️⃣ Async Functions Internally

Async/await is syntactic sugar over Promises.

Internally, it behaves similarly to generators + Promises.

Before async/await, libraries used generator-based control flow (via
ECMAScript 2015 generators).

Async/await simplified that pattern.

---

# 🔟 Real-World Example: Fetch API

```js
async function loadUser() {
  const response = await fetch("https://api.example.com/user");
  const data = await response.json();
  return data;
}
```

Very readable compared to nested `.then()` chains.

---

# 1️⃣1️⃣ Top-Level Await

Modern environments allow:

```js
const data = await fetch(url);
```

At top-level inside ES modules.

This was added later (ES2022).

---

# 1️⃣2️⃣ Common Mistakes

### ❌ Forgetting await

```js
async function test() {
  const data = getData();
  console.log(data); // Promise, not result
}
```

Fix:

```js
const data = await getData();
```

---

### ❌ Mixing await and then unnecessarily

```js
await getData().then(...)
```

Choose one style.

---

# 1️⃣3️⃣ Async Function Return Behavior

```js
async function test() {
  throw new Error("Fail");
}
```

This automatically becomes:

```js
Promise.reject(new Error("Fail"));
```

Throw inside async = rejected Promise.

---

# 1️⃣4️⃣ When to Use Async Functions

Use async/await when:

* Working with APIs
* Database calls
* File operations
* Timers
* Network requests
* Any asynchronous workflow

---

# 1️⃣5️⃣ Async vs Generators

Generators (from
ECMAScript 2015):

* Can pause execution
* Require manual `.next()`

Async functions (from
ECMAScript 2017):

* Built on Promises
* Automatically handle async flow
* Much simpler

---

# 🧠 Mental Model

Async function:

```text
Start →
  await →
    pause →
      resume when promise resolves →
Continue →
Return Promise
```

It looks synchronous, but runs asynchronously.

---

# ⚡ Async vs Promise Summary

| Feature         | Promise   | Async/Await |
| --------------- | --------- | ----------- |
| Readability     | Moderate  | High        |
| Error handling  | .catch()  | try/catch   |
| Nested calls    | Can chain | Cleaner     |
| Returns Promise | Yes       | Yes         |

---

# 🚀 Final Summary

Async functions:

* Declared with `async`
* Always return a Promise
* Use `await` to pause
* Use try/catch for errors
* Built on top of Promises
* Do not block the event loop

They make asynchronous code:

* Cleaner
* More readable
* Easier to debug
* Easier to reason about

---

# 1️⃣7️⃣ Debouncing & Throttling (Deep Dive)

Debouncing and throttling are **rate-limiting techniques** used to control how often a function runs.

They’re critical for:

* Performance optimization
* Handling rapid events
* Preventing unnecessary API calls
* Improving UX

Commonly used in libraries like Lodash and frameworks like React.

---

# 🧠 The Core Problem

Some browser events fire **very frequently**:

* `scroll`
* `resize`
* `mousemove`
* `keyup`
* `input`

Example:

```js
window.addEventListener("scroll", () => {
  console.log("Scrolling...");
});
```

Scroll 1 second → function may run **100+ times**.

This can:

* Freeze UI
* Overload APIs
* Cause layout thrashing
* Kill performance

Solution → Debounce or Throttle.

---

# 🔥 1️⃣ Debouncing

## 📌 Definition

> Debouncing delays execution until after a specified time has passed since the last event.

Think:

> “Wait until user stops doing something.”

---

## 🔹 Visual Timeline

User types:

```text
a - b - c - d - e
```

With debounce(500ms):

```text
(wait...) → run once
```

Only runs after typing stops.

---

## 🔹 Example: Search Input

Instead of calling API on every keystroke:

```js
input.addEventListener("input", search);
```

Use debounce.

---

## 🔹 Implement Debounce (Basic)

```js
function debounce(fn, delay) {
  let timer;

  return function (...args) {
    clearTimeout(timer);

    timer = setTimeout(() => {
      fn.apply(this, args);
    }, delay);
  };
}
```

---

## 🔹 Usage

```js
const handleSearch = debounce(function (event) {
  console.log("Searching for:", event.target.value);
}, 500);

input.addEventListener("input", handleSearch);
```

Now:

* User types continuously → function doesn't run
* User stops typing 500ms → function runs once

---

## 🔹 Why It Works

Each new event:

1. Clears previous timer
2. Sets new timer
3. Only last timer executes

---

# 🔥 2️⃣ Throttling

## 📌 Definition

> Throttling ensures a function runs at most once every specified interval.

Think:

> “Run at controlled intervals.”

---

## 🔹 Visual Timeline

If throttled at 1 second:

```text
Event Event Event Event Event
|-----1s-----|-----1s-----|
Run         Run
```

It runs every 1 second regardless of how many events occur.

---

## 🔹 Example: Scroll Handler

```js
function throttle(fn, delay) {
  let lastTime = 0;

  return function (...args) {
    const now = Date.now();

    if (now - lastTime >= delay) {
      lastTime = now;
      fn.apply(this, args);
    }
  };
}
```

---

## 🔹 Usage

```js
const handleScroll = throttle(() => {
  console.log("Scrolling...");
}, 1000);

window.addEventListener("scroll", handleScroll);
```

Now it runs:

* Maximum once per second.

---

# 🔥 Debounce vs Throttle (Side-by-Side)

| Feature                     | Debounce | Throttle |
| --------------------------- | -------- | -------- |
| Executes after delay        | ✅        | ❌        |
| Executes at fixed intervals | ❌        | ✅        |
| Best for typing/search      | ✅        | ❌        |
| Best for scroll/resize      | ❌        | ✅        |
| Waits for inactivity        | ✅        | ❌        |

---

# 🧠 Real-World Use Cases

## 🔹 Debounce

* Search autocomplete
* Form validation
* Saving drafts
* API calls after typing stops

## 🔹 Throttle

* Scroll position tracking
* Infinite scrolling
* Window resize calculations
* Mouse position updates
* Game loops

---

# 🔥 Advanced Debounce (Leading + Trailing)

Sometimes we want:

* Run immediately (leading)
* Or run after delay (trailing)
* Or both

Advanced version:

```js
function debounce(fn, delay, immediate = false) {
  let timer;

  return function (...args) {
    const callNow = immediate && !timer;

    clearTimeout(timer);

    timer = setTimeout(() => {
      timer = null;
      if (!immediate) fn.apply(this, args);
    }, delay);

    if (callNow) fn.apply(this, args);
  };
}
```

---

# 🔥 Advanced Throttle (Timeout-Based)

Alternative throttle:

```js
function throttle(fn, delay) {
  let timer = null;

  return function (...args) {
    if (!timer) {
      timer = setTimeout(() => {
        fn.apply(this, args);
        timer = null;
      }, delay);
    }
  };
}
```

This version ensures consistent intervals.

---

# 🧠 Internal Mechanism

Both techniques rely on:

* `setTimeout`
* Closures
* Maintaining internal state

They work because:

* Functions remember their timer state
* Closures preserve `timer` or `lastTime`

---

# ⚡ Performance Example

Without debounce:

```text
1000 key presses → 1000 API calls
```

With debounce(500ms):

```text
1000 key presses → 1 API call
```

Massive performance improvement.

---

# 🧩 In Lodash

Lodash provides:

```js
_.debounce(fn, delay)
_.throttle(fn, delay)
```

These are production-tested and configurable.

---

# 🎯 Interview Question Example

What’s the difference between:

```js
debounce(fn, 500)
```

and

```js
throttle(fn, 500)
```

Answer:

* Debounce waits for inactivity.
* Throttle limits frequency.

---

# 🔥 Mental Model

Debounce:

> “Wait until quiet.”

Throttle:

> “Control the pace.”

---

# 🚀 Summary

Debouncing:

* Delays execution
* Runs after inactivity
* Great for search inputs

Throttling:

* Limits execution rate
* Runs at fixed intervals
* Great for scroll/resize

Both:

* Improve performance
* Prevent unnecessary work
* Use closures + timers
* Essential in frontend optimization

---

# 1️⃣8️⃣ Memoization (Deep Dive)

Memoization is one of the most powerful performance optimization techniques in JavaScript.

---

# 🧠 What Is Memoization?

> **Memoization is an optimization technique where you cache the results of expensive function calls and return the cached result when the same inputs occur again.**

Instead of recomputing:

```js
slowFunction(5);
slowFunction(5);
slowFunction(5);
```

We compute once → store result → reuse it.

---

# 1️⃣ Why Memoization Matters

Imagine a function that takes 2 seconds to compute:

```js
function slowSquare(n) {
  console.log("Computing...");
  for (let i = 0; i < 1e9; i++) {} // simulate heavy work
  return n * n;
}
```

Calling it multiple times with the same input wastes CPU.

Memoization fixes that.

---

# 2️⃣ Basic Memoization Example

```js
function memoizedSquare() {
  const cache = {};

  return function (n) {
    if (n in cache) {
      console.log("From cache");
      return cache[n];
    }

    console.log("Computing...");
    const result = n * n;
    cache[n] = result;
    return result;
  };
}

const square = memoizedSquare();

square(5); // Computing...
square(5); // From cache
```

---

# 3️⃣ Generic Memoize Function

Let’s build a reusable version:

```js
function memoize(fn) {
  const cache = {};

  return function (...args) {
    const key = JSON.stringify(args);

    if (key in cache) {
      return cache[key];
    }

    const result = fn.apply(this, args);
    cache[key] = result;
    return result;
  };
}
```

---

## 🔹 Usage

```js
function add(a, b) {
  return a + b;
}

const memoAdd = memoize(add);

memoAdd(2, 3); // computes
memoAdd(2, 3); // cached
```

---

# 4️⃣ Memoization + Recursion (Very Important)

Memoization becomes extremely powerful with recursion.

Example: Fibonacci (inefficient version)

```js
function fib(n) {
  if (n <= 1) return n;
  return fib(n - 1) + fib(n - 2);
}
```

Time complexity: **O(2ⁿ)** ❌

---

## 🔥 Optimized with Memoization

```js
function memoFib(n, cache = {}) {
  if (n in cache) return cache[n];
  if (n <= 1) return n;

  cache[n] = memoFib(n - 1, cache) + memoFib(n - 2, cache);
  return cache[n];
}
```

Time complexity becomes: **O(n)** ✅

Huge improvement.

---

# 5️⃣ How Memoization Works Internally

It relies on:

* Closures
* Cache storage (object or Map)
* Function arguments as keys

It works best when functions are:

* Pure
* Deterministic
* Expensive to compute

---

# 6️⃣ Using Map Instead of Object (Better)

```js
function memoize(fn) {
  const cache = new Map();

  return function (...args) {
    const key = JSON.stringify(args);

    if (cache.has(key)) {
      return cache.get(key);
    }

    const result = fn.apply(this, args);
    cache.set(key, result);
    return result;
  };
}
```

Why Map?

* Better performance
* No prototype issues
* Cleaner API

---

# 7️⃣ Real-World Use Cases

Memoization is useful for:

* Expensive calculations
* Recursive algorithms
* API response caching
* Data transformation
* Derived state
* UI performance optimization

---

# 8️⃣ Memoization in React

In React, memoization is critical for performance.

React provides:

* `React.memo`
* `useMemo`
* `useCallback`

Example:

```js
const memoizedValue = useMemo(() => {
  return expensiveCalculation(data);
}, [data]);
```

Recomputes only when dependencies change.

---

# 9️⃣ Memoization in Lodash

Lodash provides:

```js
_.memoize(fn)
```

Production-ready memoization utility.

---

# 🔟 When NOT to Use Memoization

Avoid memoization when:

* Function is cheap
* Inputs are always unique
* Memory is limited
* Results are large
* Cache invalidation is complex

---

# 1️⃣1️⃣ Memory Consideration

Memoization trades:

```text
Memory → For → Speed
```

If inputs are large or numerous, cache grows indefinitely.

Solution:

* Limit cache size
* Use LRU cache
* Clear cache when needed

---

# 1️⃣2️⃣ Memoization vs Caching

Caching is broader:

* Can cache API responses
* Can cache database results
* Can store files

Memoization is specifically:

> Caching function results.

---

# 1️⃣3️⃣ Memoization vs Dynamic Programming

Dynamic Programming often uses memoization internally.

Two approaches:

1. Top-down (recursion + memoization)
2. Bottom-up (tabulation)

Memoization is top-down DP.

---

# 1️⃣4️⃣ Key Requirements for Safe Memoization

Function must be:

* Pure
* No side effects
* Deterministic
* Based only on inputs

Bad example:

```js
function getTime() {
  return Date.now();
}
```

Memoizing this makes no sense.

---

# 1️⃣5️⃣ Advanced: Memoizing Async Functions

```js
function memoizeAsync(fn) {
  const cache = new Map();

  return async function (...args) {
    const key = JSON.stringify(args);

    if (cache.has(key)) {
      return cache.get(key);
    }

    const promise = fn.apply(this, args);
    cache.set(key, promise);
    return promise;
  };
}
```

This prevents duplicate API calls.

---

# 🧠 Mental Model

Without memoization:

```text
Input → Compute → Output
Input → Compute → Output
Input → Compute → Output
```

With memoization:

```text
Input → Compute → Store
Input → Retrieve from cache
Input → Retrieve from cache
```

---

# ⚡ Performance Insight

Memoization:

* Reduces time complexity
* Improves responsiveness
* Minimizes repeated work

But:

* Uses extra memory
* Requires careful use

---

# 🚀 Summary

Memoization:

* Caches function results
* Works best with pure functions
* Powerful for recursion
* Reduces time complexity dramatically
* Trades memory for speed
* Used heavily in modern frameworks

---

# 1️⃣9️⃣ Functional Programming Concepts (Deep Dive in JavaScript)

Functional Programming (FP) is a programming paradigm where:

> Programs are built by composing **pure functions**, avoiding shared state and mutable data.

JavaScript supports FP very well because:

* Functions are first-class citizens
* Closures exist
* Higher-order functions are natural
* Arrow functions are concise

---

# 🧠 Core Philosophy of Functional Programming

Functional Programming emphasizes:

* Pure functions
* Immutability
* Declarative style
* Function composition
* Avoiding side effects

---

# 1️⃣ First-Class Functions

In JavaScript, functions are **first-class objects**, meaning they can:

* Be assigned to variables
* Be passed as arguments
* Be returned from other functions

```js
const greet = () => "Hello";

function execute(fn) {
  return fn();
}

execute(greet); // "Hello"
```

This capability was formalized in
ECMAScript 5 and enhanced further in
ECMAScript 2015 with arrow functions.

---

# 2️⃣ Pure Functions

A function is pure if:

1. Same input → same output
2. No side effects

✅ Pure:

```js
function add(a, b) {
  return a + b;
}
```

❌ Impure:

```js
let total = 0;

function addToTotal(n) {
  total += n;
}
```

Pure functions are:

* Predictable
* Testable
* Easier to debug

---

# 3️⃣ Immutability

Functional programming avoids mutating data.

Instead of modifying:

```js
const arr = [1, 2, 3];
arr.push(4); // mutates
```

Use immutable approach:

```js
const newArr = [...arr, 4];
```

Why?

Mutation causes:

* Unexpected bugs
* Hard-to-track state changes
* Race conditions

Immutability makes systems safer.

---

# 4️⃣ Higher-Order Functions (HOF)

A higher-order function:

* Takes a function as argument
* Or returns a function

Examples:

* `map`
* `filter`
* `reduce`

```js
const numbers = [1, 2, 3];

const doubled = numbers.map(n => n * 2);
```

HOFs allow declarative programming.

---

# 5️⃣ Declarative vs Imperative

Imperative:

```js
let result = [];
for (let i = 0; i < numbers.length; i++) {
  result.push(numbers[i] * 2);
}
```

Declarative:

```js
const result = numbers.map(n => n * 2);
```

Declarative focuses on **what**, not **how**.

---

# 6️⃣ Function Composition

Combining small functions to build larger behavior.

```js
const double = x => x * 2;
const square = x => x * x;

const compose = (f, g) => x => f(g(x));

const doubleThenSquare = compose(square, double);

doubleThenSquare(3); // 36
```

Composition builds complex logic from simple pieces.

---

# 7️⃣ Currying

Transforming:

```js
f(a, b, c)
```

Into:

```js
f(a)(b)(c)
```

Example:

```js
const multiply = a => b => a * b;

const double = multiply(2);

double(5); // 10
```

Currying increases reusability.

---

# 8️⃣ Referential Transparency

An expression is referentially transparent if it can be replaced with its value without changing program behavior.

Example:

```js
5 + 5
```

Always 10.

This concept makes reasoning about programs easier.

---

# 9️⃣ Avoiding Side Effects

Side effects include:

* Modifying global variables
* API calls
* DOM manipulation
* Logging
* Database writes

Functional programming tries to isolate side effects.

Instead of:

```js
fetchData();
updateUI();
```

Use pure transformation functions and handle effects separately.

---

# 🔟 Statelessness

Functional programming prefers stateless systems.

State is passed explicitly.

Bad:

```js
let user = {};
```

Better:

```js
function updateUser(user, data) {
  return { ...user, ...data };
}
```

---

# 1️⃣1️⃣ Recursion Over Loops

FP often prefers recursion instead of loops.

```js
function sum(arr) {
  if (arr.length === 0) return 0;
  return arr[0] + sum(arr.slice(1));
}
```

Though JavaScript does not optimize tail calls well in most engines.

---

# 1️⃣2️⃣ Idempotence

An idempotent function:

> Running it multiple times gives the same result.

Example:

```js
Math.abs(-5); // always 5
```

Idempotent operations are safe in distributed systems.

---

# 1️⃣3️⃣ Functional Libraries

JavaScript has powerful FP libraries:

* Lodash
* Ramda
* Redux (inspired by FP principles)

These libraries encourage immutability and composition.

---

# 1️⃣4️⃣ Functional Programming in React

React strongly embraces FP ideas:

* Components are pure functions
* State updates are immutable
* Hooks use composition
* `useReducer` is functional state management

---

# 1️⃣5️⃣ FP vs OOP

| Functional Programming | Object-Oriented Programming |
| ---------------------- | --------------------------- |
| Functions              | Classes                     |
| Immutability           | Mutable state               |
| Stateless              | Stateful                    |
| Composition            | Inheritance                 |
| Declarative            | Imperative                  |

Modern JavaScript often combines both.

---

# 🧠 Why Functional Programming Matters

It:

* Reduces bugs
* Improves testability
* Makes code predictable
* Encourages modularity
* Scales better in large systems

Especially in:

* Frontend frameworks
* Data transformation
* Backend services
* Concurrency-heavy systems

---

# 🚀 Big Picture Mental Model

Functional Programming is about:

```text
Input → Pure Function → Output
```

Instead of:

```text
Object → Mutate → Side Effect → Hidden Changes
```

---

# 🎯 Final Summary

Functional Programming in JavaScript focuses on:

* Pure functions
* Immutability
* Higher-order functions
* Composition
* Currying
* Declarative style
* Avoiding side effects
* Stateless design

JavaScript is multi-paradigm — but modern best practices lean heavily toward functional concepts.

---

# 🎯 JavaScript Interview Focus Areas (Deep, Practical + Interview-Ready)

This guide covers:

* Core concept
* Common traps
* Interview questions
* Practical examples

---

# 1️⃣ Closures

## 🔹 What Is a Closure?

> A closure is when a function remembers variables from its lexical scope even after the outer function has finished executing.

```js
function outer() {
  let count = 0;

  return function inner() {
    count++;
    return count;
  };
}

const counter = outer();

counter(); // 1
counter(); // 2
```

Even though `outer()` finished, `inner()` remembers `count`.

---

## 🔹 Why Closures Matter

Closures are used in:

* Data privacy
* Memoization
* Debounce/throttle
* Module pattern
* React hooks

---

## 🔹 Classic Interview Question

### ❓ What will this output?

```js
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 1000);
}
```

Output:

```
3
3
3
```

Why?

* `var` is function-scoped
* All callbacks share same `i`

Fix:

```js
for (let i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 1000);
}
```

---

# 2️⃣ `this` Keyword

## 🔹 What Determines `this`?

`this` depends on how a function is called (not where defined).

Rules:

1. Global
2. Object method
3. Constructor (`new`)
4. Explicit binding (`call`, `apply`, `bind`)
5. Arrow functions (lexical `this`)

---

## 🔹 Example

```js
const obj = {
  name: "JS",
  show() {
    console.log(this.name);
  }
};

obj.show(); // JS
```

---

## 🔹 Arrow Function Trap

```js
const obj = {
  name: "JS",
  show: () => {
    console.log(this.name);
  }
};

obj.show(); // undefined
```

Arrow functions don’t have their own `this`.

---

## 🔹 Hard Binding

```js
function greet() {
  console.log(this.name);
}

const user = { name: "Aman" };

greet.call(user); // Aman
```

---

## 🔹 Interview Favorite

```js
const obj = {
  name: "JS",
  log() {
    setTimeout(function () {
      console.log(this.name);
    }, 1000);
  }
};

obj.log(); // undefined
```

Fix:

```js
setTimeout(() => {
  console.log(this.name);
}, 1000);
```

---

# 3️⃣ Hoisting

## 🔹 What Is Hoisting?

JavaScript moves declarations to the top during compilation.

---

## 🔹 Function Hoisting

```js
sayHi();

function sayHi() {
  console.log("Hi");
}
```

Works.

---

## 🔹 Variable Hoisting

```js
console.log(a);
var a = 5;
```

Output:

```
undefined
```

---

## 🔹 Let & Const (Temporal Dead Zone)

```js
console.log(a);
let a = 5;
```

ReferenceError.

---

# 4️⃣ Async/Await

Introduced in
ECMAScript 2017.

---

## 🔹 Key Rules

* Always returns a Promise
* `await` pauses execution
* Doesn’t block event loop

---

## 🔹 Example

```js
async function fetchData() {
  const res = await fetch("url");
  return res.json();
}
```

---

## 🔹 Common Trap

```js
async function test() {
  return 5;
}

console.log(test()); // Promise {5}
```

---

# 5️⃣ Callbacks

## 🔹 What Is a Callback?

A function passed into another function.

```js
function greet(name, callback) {
  console.log("Hi " + name);
  callback();
}

greet("JS", () => console.log("Done"));
```

---

## 🔹 Callback Hell

```js
getUser(() => {
  getOrders(() => {
    getPayments(() => {});
  });
});
```

Solved using:

* Promises
* Async/await

---

# 6️⃣ Currying

Transform:

```js
f(a, b)
```

Into:

```js
f(a)(b)
```

---

## 🔹 Example

```js
const multiply = a => b => a * b;

const double = multiply(2);
double(5); // 10
```

---

## 🔹 Interview Question

```js
sum(1)(2)(3)()
```

Implement infinite currying.

---

# 7️⃣ Recursion

A function calling itself.

---

## 🔹 Example

```js
function factorial(n) {
  if (n === 0) return 1;
  return n * factorial(n - 1);
}
```

---

## 🔹 Interview Trap

Missing base case → stack overflow.

---

# 8️⃣ Higher-Order Functions

A function that:

* Takes function as argument
* Returns a function

---

## 🔹 Examples

```js
array.map()
array.filter()
array.reduce()
```

Example:

```js
const nums = [1, 2, 3];
const doubled = nums.map(n => n * 2);
```

---

# 9️⃣ Debouncing & Throttling

---

## 🔹 Debounce

Runs function after delay of inactivity.

Used for:

* Search input
* API calls

```js
function debounce(fn, delay) {
  let timer;

  return function (...args) {
    clearTimeout(timer);
    timer = setTimeout(() => fn.apply(this, args), delay);
  };
}
```

---

## 🔹 Throttle

Runs function at most once per interval.

Used for:

* Scroll
* Resize

```js
function throttle(fn, delay) {
  let last = 0;

  return function (...args) {
    const now = Date.now();

    if (now - last > delay) {
      last = now;
      fn.apply(this, args);
    }
  };
}
```

---

# 🧠 How Interviewers Think

They test:

* Your understanding of scope
* Execution context
* Event loop knowledge
* Memory model
* Real-world debugging ability

Not just definitions.

---

# 🔥 Most Asked Combined Question

```js
console.log(a);

var a = 10;

function test() {
  console.log(a);
  var a = 20;
}

test();
```

Answer:

```
undefined
undefined
```

Why?

* Global `a` hoisted → undefined
* Inside function, `a` shadowed → hoisted locally

---















