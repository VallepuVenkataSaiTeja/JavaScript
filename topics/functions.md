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



