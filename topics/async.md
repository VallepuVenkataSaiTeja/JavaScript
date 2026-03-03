# 🟢 1. Foundations (Before Async)

Make sure you’re comfortable with:

* Variables (`let`, `const`)
* Functions (declarations, expressions, arrow functions)
* Scope & closures
* Arrays & objects
* ES6 basics (destructuring, spread, modules)

---

# 🟡 2. JavaScript Execution Model

Understanding async starts here:

### 🔹 Single-Threaded Nature

* Call stack
* Blocking vs Non-blocking code

### 🔹 Event Loop

* Call Stack
* Web APIs
* Callback Queue (Task Queue)
* Microtask Queue

👉 Key Concept:
How the **Event Loop** handles async tasks.

---

# 🟠 3. Callbacks (The First Async Pattern)

### Topics to cover:

* What is a callback?
* Synchronous vs asynchronous callbacks
* Callback hell
* Inversion of control

### Practice:

* `setTimeout`
* `setInterval`
* Basic file/API simulation

---

# 🔵 4. Promises

The core building block of modern async JS.

### 🔹 Promise Basics

* States: pending, fulfilled, rejected
* `.then()`
* `.catch()`
* `.finally()`

### 🔹 Promise Chaining

* Returning values
* Returning promises
* Error propagation

### 🔹 Static Methods

* `Promise.all()`
* `Promise.allSettled()`
* `Promise.race()`
* `Promise.any()`

---

# 🟣 5. Async / Await

Built on top of Promises.

### Topics:

* `async` functions
* `await`
* Error handling with `try/catch`
* Sequential vs Parallel execution
* Await inside loops (common mistakes)

---

# 🔴 6. Fetch API & Real-World Async

Work with real APIs using:

* `fetch()`
* Handling JSON
* HTTP methods (GET, POST, PUT, DELETE)
* Handling errors properly
* AbortController

---

# 🟤 7. Advanced Event Loop Concepts

This separates intermediate from advanced devs.

* Microtasks vs Macrotasks
* `queueMicrotask`
* `process.nextTick()` (Node.js)
* `setImmediate()` (Node.js)
* Rendering cycle interaction (browser)

---

# ⚫ 8. Asynchronous Patterns & Control Flow

* Parallel execution
* Sequential execution
* Rate limiting
* Debouncing
* Throttling
* Retry mechanisms
* Timeout wrappers

---

# 🟢 9. Async in Node.js

If you're doing backend:

* EventEmitter
* Streams
* File system async APIs
* Timers in Node
* Worker Threads
* Cluster module

---

# 🔵 10. Error Handling Strategies

* Global unhandled rejections
* Graceful degradation
* Retrying failed requests
* Circuit breaker pattern
* Logging async errors

---

# 🟣 11. Concurrency vs Parallelism

Important theoretical concept:

* JS concurrency model
* Web Workers
* Worker Threads (Node)
* CPU-bound vs I/O-bound tasks

---

# 🔴 12. Performance & Optimization

* Avoiding blocking code
* Memory leaks with async
* Async stack traces
* Profiling async code (DevTools)

---

# 🟤 13. Testing Async Code

* Testing promises
* Testing async/await
* Mocking APIs
* Handling timers in tests

---

# ⚫ 14. Advanced Topics (Expert Level)

* Async Iterators (`for await...of`)
* Generators
* Observables (RxJS)
* Custom Promise implementation
* Understanding how V8 handles async internally

---

# 🧠 Recommended Learning Order

1. Execution model
2. Callbacks
3. Promises
4. Async/Await
5. Event Loop deep dive
6. Real-world API handling
7. Advanced patterns

---

# 🎯 Mini Project Ideas

* Build a weather app (fetch API)
* Create a retry wrapper for failed API calls
* Implement Promise.all manually
* Create a rate limiter
* Build a simple task scheduler

---


# 🟢 1. Variables (`let`, `const`)

## 🔹 `var` (Old Way – Function Scoped)

```js
function example() {
  if (true) {
    var x = 10;
  }
  console.log(x); // 10
}
```

`var` ignores block scope. It is **function-scoped**.

Problems:

* Can be redeclared
* Hoisted and initialized as `undefined`
* Causes bugs in loops

---

## 🔹 `let` (Block Scoped)

```js
if (true) {
  let x = 10;
}
console.log(x); // ❌ ReferenceError
```

`let`:

* Block-scoped
* Can be reassigned
* Cannot be redeclared in same scope

### 🔹 Temporal Dead Zone (TDZ)

```js
console.log(a); // ❌ ReferenceError
let a = 5;
```

With `let`, the variable exists but **cannot be accessed before declaration**.

---

## 🔹 `const` (Block Scoped + Immutable Binding)

```js
const x = 10;
x = 20; // ❌ Error
```

Important: `const` prevents reassignment — **not mutation**.

```js
const obj = { name: "John" };
obj.name = "Jane"; // ✅ allowed
```

The reference is constant. The object contents are not.

---

## 🧠 When to Use What?

* Use `const` by default
* Use `let` when reassignment is needed
* Avoid `var`

---

# 🟢 2. Functions

Functions create execution contexts — critical for async understanding.

---

## 🔹 Function Declaration

```js
function greet(name) {
  return `Hello ${name}`;
}
```

Characteristics:

* Hoisted completely
* Can be called before definition

```js
greet("Sam"); // Works
```

---

## 🔹 Function Expression

```js
const greet = function(name) {
  return `Hello ${name}`;
};
```

Not hoisted like declarations.

```js
greet("Sam"); // ❌ if called before definition
```

---

## 🔹 Arrow Functions

```js
const greet = (name) => {
  return `Hello ${name}`;
};
```

Short form:

```js
const greet = name => `Hello ${name}`;
```

---

### 🔹 Arrow vs Regular Function (CRITICAL)

#### 1️⃣ `this` behavior

Regular function:

```js
const obj = {
  name: "John",
  greet() {
    console.log(this.name);
  }
};
```

Arrow function:

```js
const obj = {
  name: "John",
  greet: () => {
    console.log(this.name);
  }
};
```

Arrow functions:

* Do NOT have their own `this`
* Inherit `this` from surrounding scope (lexical `this`)

This matters heavily in async callbacks.

---

# 🟢 3. Scope & Closures (Extremely Important)

## 🔹 What is Scope?

Scope determines where variables are accessible.

Types:

* Global scope
* Function scope
* Block scope

Example:

```js
let globalVar = "I'm global";

function test() {
  let localVar = "I'm local";
}
```

`localVar` is not accessible outside the function.

---

## 🔹 Lexical Scope

JavaScript uses **lexical scoping** — scope determined by where code is written.

```js
function outer() {
  let x = 10;

  function inner() {
    console.log(x);
  }

  inner();
}
```

`inner()` can access `x` because it was defined inside `outer`.

---

## 🔹 Closures (CRITICAL FOR ASYNC)

A closure is:

> A function that remembers variables from its outer scope even after that scope has finished execution.

Example:

```js
function counter() {
  let count = 0;

  return function() {
    count++;
    console.log(count);
  };
}

const increment = counter();
increment(); // 1
increment(); // 2
```

Why does this work?

Because the inner function **closes over** the `count` variable.

Closures are the backbone of:

* Async callbacks
* Timers
* Promises
* Event handlers
* Data privacy

---

# 🟢 4. Arrays & Objects (Core Data Structures)

Async often deals with collections and responses.

---

## 🔹 Arrays

```js
const numbers = [1, 2, 3];
```

Important methods:

```js
numbers.map(n => n * 2);
numbers.filter(n => n > 1);
numbers.reduce((acc, n) => acc + n, 0);
numbers.forEach(n => console.log(n));
```

Understanding `map()` is critical for:

```js
Promise.all(items.map(fetchItem));
```

---

## 🔹 Objects

```js
const user = {
  name: "Alice",
  age: 25
};
```

Access:

```js
user.name;
user["age"];
```

Dynamic keys:

```js
const key = "name";
console.log(user[key]);
```

---

## 🔹 Reference Behavior

Objects and arrays are reference types:

```js
const obj1 = { name: "John" };
const obj2 = obj1;

obj2.name = "Jane";
console.log(obj1.name); // Jane
```

Both variables point to same memory reference.

This is extremely important in async mutations.

---

# 🟢 5. ES6 Basics

These features are used everywhere in async code.

---

## 🔹 Destructuring

### Object destructuring

```js
const user = { name: "John", age: 30 };

const { name, age } = user;
```

Used heavily with API responses:

```js
const { data, status } = response;
```

---

### Array destructuring

```js
const [first, second] = [10, 20];
```

---

## 🔹 Spread Operator (`...`)

Clone arrays:

```js
const arr = [1, 2];
const newArr = [...arr, 3];
```

Clone objects:

```js
const user = { name: "John" };
const updatedUser = { ...user, age: 30 };
```

Important for immutable updates in async flows.

---

## 🔹 Rest Operator

```js
function sum(...numbers) {
  return numbers.reduce((a, b) => a + b);
}
```

---

## 🔹 Modules (Import/Export)

Modern JS uses modules:

### export

```js
export function greet() {}
export const name = "John";
```

### import

```js
import { greet, name } from "./file.js";
```

Why important?

Because async apps are modular:

* API layer
* Utility layer
* UI layer
* State management

---

# 🧠 Why All This Matters for Async

Async code relies on:

* Closures to preserve state
* Functions as first-class values
* Block scope inside loops
* Array methods for promise handling
* Object destructuring for API responses
* `this` behavior in callbacks
* Immutable updates using spread

If foundations are weak, async becomes confusing.

---

# 🟡 JavaScript Execution Context (In-Depth)

If the **call stack** tells us *what runs*,
the **execution context** explains *how it runs*.

Execution context is one of the most important concepts in JavaScript.

---

# 🔹 1. What Is an Execution Context?

An **execution context** is the **environment in which JavaScript code is evaluated and executed**.

Every time JS runs:

* A global environment is created
* Every function call creates a new environment

Think of it like:

> 📦 A box that contains everything needed to run a piece of code.

---

# 🔹 2. Types of Execution Contexts

There are 3 types:

## 1️⃣ Global Execution Context (GEC)

Created when:

* The JS file first loads.

There is only **one** global execution context.

In browsers like **Google Chrome**, the global object is:

```js
window
```

In **Node.js**, the global object is:

```js
global
```

---

## 2️⃣ Function Execution Context (FEC)

Created:

* Every time a function is called.

Each function call gets:

* Its own variables
* Its own scope
* Its own `this`
* Its own arguments object

---

## 3️⃣ Eval Execution Context (Rare)

Created when using:

```js
eval()
```

Avoid using `eval` in real-world applications.

---

# 🔹 3. What’s Inside an Execution Context?

Each execution context has **two main phases**:

---

# 🟢 Phase 1: Creation Phase (Memory Setup)

Before code runs, JavaScript:

1. Creates a Variable Object (VO)
2. Sets up the scope chain
3. Determines `this`

Nothing executes yet.

It just prepares memory.

---

### During Creation Phase:

### ✅ 1. Variables are Hoisted

```js
console.log(x); // undefined
var x = 10;
```

Behind the scenes:

```js
var x;  // allocated memory
console.log(x);
x = 10;
```

`var` is initialized with `undefined`.

---

### ✅ 2. Functions Are Fully Hoisted

```js
greet(); // works

function greet() {
  console.log("Hello");
}
```

Functions are stored in memory entirely.

---

### ✅ 3. `let` and `const` Behavior

```js
console.log(a); // ReferenceError
let a = 5;
```

They are hoisted but:

* Not initialized
* Stay in the **Temporal Dead Zone (TDZ)**

---

# 🟢 Phase 2: Execution Phase

Now JavaScript runs code line by line:

* Assigns real values
* Executes functions
* Evaluates expressions

---

# 🔹 4. Execution Context & Call Stack

Each execution context is pushed onto the **call stack**.

Example:

```js
function one() {
  two();
}

function two() {
  console.log("Hi");
}

one();
```

### Stack flow:

1. Global context created → pushed
2. `one()` called → new context pushed
3. `two()` called → new context pushed
4. `two()` finishes → popped
5. `one()` finishes → popped
6. Global finishes

---

# 🔹 5. Visual Representation

```
Call Stack:

| two()  |
| one()  |
| Global |
-----------
```

---

# 🔹 6. Deep Dive: What Exactly Is Stored?

Each execution context contains:

### 📦 1. Variable Environment

Stores:

* Variables
* Function declarations

### 📦 2. Lexical Environment

Stores:

* Outer reference (scope chain)

### 📦 3. `this` Binding

Determined by:

* How a function is called

Example:

```js
const obj = {
  name: "John",
  greet() {
    console.log(this.name);
  }
};

obj.greet(); // "John"
```

Here `this` refers to `obj`.

---

# 🔹 7. Lexical Scope & Scope Chain

Lexical = defined by where code is written.

Example:

```js
function outer() {
  let x = 10;

  function inner() {
    console.log(x);
  }

  inner();
}

outer();
```

How does `inner()` find `x`?

* It looks inside its own scope.
* If not found → goes to outer scope.
* Continues up the scope chain.

This chain is stored inside the execution context.

---

# 🔹 8. Important Concept: Execution Context vs Scope

| Execution Context      | Scope                        |
| ---------------------- | ---------------------------- |
| Created when code runs | Created when code is written |
| Lives on call stack    | Lives in memory              |
| Temporary              | Persistent                   |

---

# 🔹 9. Real Internal Flow (Engine Level)

When JS engine (like V8 inside Chrome) runs:

1. Creates Global Execution Context
2. Pushes it onto stack
3. Runs creation phase
4. Runs execution phase
5. When a function is called:

   * New execution context created
   * Pushed to stack
   * Runs creation phase
   * Runs execution phase
   * Popped when done

---

# 🔥 Why This Is CRITICAL for Async

Async behavior works because:

* Long operations leave the call stack
* Their callbacks re-enter as new execution contexts

If you don’t understand execution context:

* Closures won’t make sense
* `this` won’t make sense
* Hoisting won’t make sense
* Async won’t make sense

---

# 🧠 Master-Level Mental Model

Think of it like:

```
Execution Context = Memory Box
Call Stack = Execution Manager
Scope Chain = Variable Lookup Path
```

---

# 🟡 2. JavaScript Execution Model

Understanding **async** starts here.

To truly understand async behavior, you must understand three things:

* JavaScript is **single-threaded**
* It uses a **call stack**
* Blocking vs Non-blocking behavior depends on how tasks are handled

Let’s go deep.

---

# 🔹 Single-Threaded Nature

JavaScript runs on **one main thread**.

In environments like:

* **Google Chrome**
* **Node.js**

There is only **one call stack**.

That means:

> At any given moment, only one piece of JavaScript code is executing.

No parallel execution (by default).
No two functions running at the same time.

---

# 🔹 The Call Stack

The **call stack** is a data structure that keeps track of:

* Which function is currently running
* Who called it
* What should run next

It follows:

> LIFO — Last In, First Out

---

## Example

```js
function first() {
  console.log("First");
}

function second() {
  first();
  console.log("Second");
}

second();
```

### What happens internally:

1. Global Execution Context created → pushed to stack
2. `second()` called → pushed
3. Inside `second()`, `first()` called → pushed
4. `first()` runs → logs `"First"` → popped
5. Back to `second()` → logs `"Second"` → popped
6. Stack becomes empty

---

### Stack Visualization

```
| first()  |  ← running
| second() |
| global   |
------------
```

After `first()` finishes:

```
| second() |
| global   |
------------
```

---

# 🔹 Blocking Code

Because JavaScript is single-threaded:

If something takes a long time, **everything waits**.

Example:

```js
console.log("Start");

while (true) {}

console.log("End");
```

What happens?

* `"Start"` prints
* Infinite loop runs
* `"End"` never prints
* UI freezes
* Clicks stop working

This is **blocking code**.

---

## Why It Blocks

Because the call stack is busy.

As long as the stack is not empty:

* Nothing else can execute
* No events can be handled
* No callbacks can run

---

# 🔹 Non-Blocking Code

Non-blocking code allows JavaScript to:

* Start a task
* Continue running other code
* Handle the result later

Example:

```js
console.log("Start");

setTimeout(() => {
  console.log("Timeout finished");
}, 2000);

console.log("End");
```

Output:

```
Start
End
Timeout finished
```

Why?

Because `setTimeout` is **not handled by the call stack directly**.

Instead:

1. JS registers the timer
2. The timer runs in Web APIs (browser) or background system
3. When finished → callback goes to the queue
4. Event Loop pushes it back to the stack when it's empty

---

# 🔹 Where Does Non-Blocking Come From?

In browsers like **Google Chrome**, async APIs come from:

* Web APIs (Timers, DOM events, Fetch, etc.)

In **Node.js**, async APIs come from:

* libuv (event-driven system)

Important:

> JavaScript itself is single-threaded.
> The environment provides asynchronous capabilities.

---

# 🔥 Blocking vs Non-Blocking Comparison

| Blocking              | Non-Blocking               |
| --------------------- | -------------------------- |
| Stops everything      | Allows other code to run   |
| Call stack stays busy | Task handled outside stack |
| UI freezes            | UI remains responsive      |
| Synchronous           | Asynchronous               |

---

# 🔹 Key Insight

JavaScript achieves non-blocking behavior **not by multithreading**, but by:

* Offloading work
* Using queues
* Using the event loop

---

# 🧠 Core Mental Model

```
Call Stack → Executes code
Web APIs / Background → Handle async tasks
Callback Queue → Stores completed tasks
Event Loop → Moves tasks to stack when empty
```

---

# 🔹 Event Loop (The Heart of Async JavaScript)

If JavaScript is single-threaded…

How does it handle timers, network requests, promises, and user clicks without freezing?

👉 The answer is the **Event Loop**.

The event loop coordinates between:

* Call Stack
* Web APIs (or background APIs)
* Callback Queue (Task Queue / Macrotask Queue)
* Microtask Queue

Let’s break this down properly.

---

# 🧠 Big Picture

```text
Call Stack  ← Executes code
Web APIs    ← Handle async operations
Task Queue  ← Stores completed async callbacks
Microtask Queue ← Stores promise callbacks
Event Loop  ← Moves tasks when stack is empty
```

---

# 🔹 1. Call Stack

The **call stack** executes synchronous JavaScript.

It can only run **one thing at a time**.

If the stack is not empty:

* Nothing else runs.
* No async callbacks execute.

---

# 🔹 2. Web APIs (Browser / Runtime APIs)

JavaScript itself does NOT have timers or fetch built in.

Those come from the environment:

In browsers like **Google Chrome**, Web APIs include:

* `setTimeout`
* `setInterval`
* `fetch`
* DOM events

In **Node.js**, background APIs come from:

* libuv (file system, networking, timers)

When you call something async:

```js
setTimeout(() => {
  console.log("Done");
}, 2000);
```

What happens:

1. `setTimeout` is called.
2. Timer is handed off to Web APIs.
3. The stack continues running other code.

---

# 🔹 3. Callback Queue (Task Queue / Macrotask Queue)

When an async task completes:

* Its callback is placed in the **Task Queue**.

Examples of macrotasks:

* setTimeout
* setInterval
* DOM events
* setImmediate (Node)

These wait their turn.

But they cannot run immediately.

---

# 🔹 4. Microtask Queue (Higher Priority)

Microtasks are:

* Promise `.then()`
* Promise `.catch()`
* `queueMicrotask`
* `MutationObserver`

Microtasks have **higher priority** than the task queue.

Important rule:

> After every synchronous execution, JavaScript empties the entire microtask queue before touching the task queue.

This is critical.

---

# 🔥 5. The Event Loop Rule (Most Important Concept)

The **Event Loop** constantly checks:

```text
Is the Call Stack empty?
```

If YES:

1. Run ALL microtasks
2. Then run ONE macrotask
3. Repeat

That’s the core rule.

---

# 🧪 Example 1: Basic Async

```js
console.log("Start");

setTimeout(() => {
  console.log("Timeout");
}, 0);

console.log("End");
```

Output:

```
Start
End
Timeout
```

Why?

* Timeout callback goes to Task Queue
* Stack must finish first
* Then event loop pushes it onto stack

---

# 🧪 Example 2: Microtasks vs Macrotasks

```js
console.log("Start");

setTimeout(() => {
  console.log("Timeout");
}, 0);

Promise.resolve().then(() => {
  console.log("Promise");
});

console.log("End");
```

Output:

```
Start
End
Promise
Timeout
```

Why?

Step-by-step:

1. "Start" → printed
2. setTimeout → goes to Web API
3. Promise → microtask queue
4. "End" → printed
5. Stack empty
6. Event loop runs ALL microtasks → prints "Promise"
7. Then runs one macrotask → prints "Timeout"

Microtasks win.

---

# 🔬 Deep Internal Flow

Let’s simulate:

```text
Call Stack:      [global()]
Microtask Queue: []
Task Queue:      []
```

After execution:

```text
Call Stack:      []
Microtask Queue: [Promise callback]
Task Queue:      [Timeout callback]
```

Event Loop sees:

* Stack empty
* Run all microtasks
* Then one macrotask
* Repeat

---

# 🔥 Example 3: Microtask Starvation

```js
function loop() {
  Promise.resolve().then(loop);
}

loop();
```

What happens?

* Each microtask schedules another microtask.
* Microtask queue never empties.
* Macrotasks never execute.
* App freezes.

This is called **microtask starvation**.

---

# 🎯 Key Priority Order

Execution order priority:

1. Synchronous code
2. All microtasks
3. One macrotask
4. Repeat

---

# 🧠 Visual Mental Model

```text
          ┌──────────────┐
          │   Call Stack │
          └──────┬───────┘
                 │
         Is it empty?
                 │
          ┌──────▼───────┐
          │ Microtask Q  │  ← Promises (run all)
          └──────┬───────┘
                 │
          ┌──────▼───────┐
          │ Task Queue   │  ← setTimeout (run one)
          └──────────────┘
```

The Event Loop just keeps cycling forever.

---

# 🚀 Why This Explains Async/Await

`async/await` is built on Promises.

So:

* `await` pauses function execution
* The continuation goes to Microtask Queue
* It runs before macrotasks

That’s why async/await feels synchronous but is not blocking.

---

# 🧠 Final Core Understanding

JavaScript is:

* Single-threaded
* Non-blocking
* Event-driven
* Queue-based

The Event Loop ensures:

> "Nothing blocks, everything waits its turn."

---

# 🟠 3. Callbacks (The First Async Pattern)

Before **Promises** and **async/await**, JavaScript handled async using **callbacks**.

Understanding callbacks is critical because:

* Promises are built on them
* Async/await is built on Promises
* Many APIs still use them

Let’s go step by step.

---

# 🔹 1. What Is a Callback?

A **callback** is:

> A function passed as an argument to another function, to be executed later.

Simple example (synchronous):

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

Here:

* `greet` is passed as a callback
* `processUser` decides *when* to execute it

---

# 🔹 2. Synchronous vs Asynchronous Callbacks

## 🟢 A. Synchronous Callback

Runs immediately.

Example:

```js
[1, 2, 3].forEach(function (num) {
  console.log(num);
});
```

`forEach` executes the callback **immediately** for each element.

Everything happens in the call stack.

---

## 🔵 B. Asynchronous Callback

Runs later.

Example using `setTimeout` (browser or runtime):

```js
console.log("Start");

setTimeout(function () {
  console.log("Delayed");
}, 1000);

console.log("End");
```

Output:

```
Start
End
Delayed
```

The callback:

* Is handed off to environment APIs (browser or **Node.js**)
* Runs later via the event loop

---

# 🔹 3. Practicing with Timers

## 🟢 setTimeout

Runs once after delay.

```js
setTimeout(() => {
  console.log("Runs once after 2 seconds");
}, 2000);
```

---

## 🟢 setInterval

Runs repeatedly.

```js
let count = 0;

const intervalId = setInterval(() => {
  count++;
  console.log("Count:", count);

  if (count === 5) {
    clearInterval(intervalId);
  }
}, 1000);
```

Important:

* `setInterval` keeps scheduling callbacks
* You must manually stop it

---

# 🔹 4. Simulating Async (File/API)

Let’s simulate a fake API call:

```js
function fetchData(callback) {
  console.log("Fetching data...");

  setTimeout(() => {
    const data = { id: 1, name: "Product" };
    callback(data);
  }, 2000);
}

fetchData(function (data) {
  console.log("Received:", data);
});
```

What happens:

1. `fetchData` starts
2. Timer is scheduled
3. After 2s → callback runs with data

This mimics:

* File read
* Database query
* Network request

---

# 🔴 5. Callback Hell

Now the problem begins.

Imagine we need:

1. Get user
2. Get user’s orders
3. Get order details

Using callbacks:

```js
getUser(function (user) {
  getOrders(user.id, function (orders) {
    getOrderDetails(orders[0].id, function (details) {
      console.log(details);
    });
  });
});
```

This causes:

* Deep nesting
* Hard-to-read code
* Hard-to-handle errors

This is called:

> ❌ Callback Hell
> ❌ Pyramid of Doom

Visually:

```text
getUser(() => {
  getOrders(() => {
    getOrderDetails(() => {
      ...
    });
  });
});
```

Problems:

* Hard debugging
* Hard error handling
* Hard to maintain

---

# 🔴 6. Inversion of Control (Very Important Concept)

This is the **real danger** of callbacks.

When you pass a callback:

```js
doSomething(callback);
```

You are saying:

> "Hey doSomething, you control when and how my callback runs."

You lose control.

Problems that can happen:

* Callback called twice
* Callback never called
* Callback called too early
* Callback called with wrong data

You are trusting external code.

This is called:

> Inversion of Control (IoC)

Instead of you controlling execution…
Another function controls your code.

---

# 🔥 Example of Inversion Risk

```js
function riskyOperation(callback) {
  callback("First call");
  callback("Second call"); // Oops!
}

riskyOperation(function (msg) {
  console.log(msg);
});
```

Unexpected output:

```
First call
Second call
```

You didn’t expect it twice.

That’s dangerous.

---

# 🔹 7. Why Callbacks Were Replaced

Callbacks caused:

* Nested code
* Difficult error handling
* Inversion of control problems

So JavaScript introduced:

* **Promises**
* Then **async/await**

Which give:

* Better chaining
* Centralized error handling
* More predictable flow

---

# 🧠 Mental Model

```text
Synchronous callback → runs immediately
Asynchronous callback → runs later via event loop
Callback hell → deep nesting problem
Inversion of control → you lose execution control
```

---

# 🔵 4. Promises

The **core building block** of modern async JavaScript.

Promises were introduced to solve:

* Callback hell
* Inversion of control
* Poor error handling
* Unstructured async flow

Everything modern in JS async (`fetch`, `async/await`) is built on Promises.

Let’s go deep.

---

# 🔹 1. What Is a Promise?

A Promise is:

> An object representing the eventual completion (or failure) of an asynchronous operation.

It’s a **placeholder for a future value**.

---

# 🔹 2. Promise States

A Promise has exactly **three states**:

| State       | Meaning             |
| ----------- | ------------------- |
| `pending`   | Initial state       |
| `fulfilled` | Operation succeeded |
| `rejected`  | Operation failed    |

Important rules:

* A promise can transition only once.
* Once fulfilled or rejected → it becomes **settled**.
* It cannot go back to pending.

---

## Example

```js
const promise = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve("Success!");
  }, 1000);
});
```

Internally:

1. Starts as `pending`
2. After 1 second → `resolve()` called
3. Becomes `fulfilled`

---

# 🔹 3. Consuming a Promise

## 🟢 `.then()`

Runs when fulfilled.

```js
promise.then((value) => {
  console.log(value);
});
```

`.then()` receives the resolved value.

---

## 🔴 `.catch()`

Runs when rejected.

```js
promise.catch((error) => {
  console.error(error);
});
```

---

## 🟣 `.finally()`

Runs regardless of success or failure.

```js
promise.finally(() => {
  console.log("Cleanup runs always");
});
```

Use for:

* Stopping loaders
* Closing DB connections
* Cleanup logic

---

# 🔬 Internal Mechanism (Important)

When a promise resolves:

* Its `.then()` callback is placed into the **Microtask Queue**
* It does NOT execute immediately
* It waits until the call stack is empty

That’s why:

```js
console.log("A");

Promise.resolve().then(() => {
  console.log("B");
});

console.log("C");
```

Output:

```
A
C
B
```

Because `.then()` is a microtask.

---

# 🔹 4. Promise Chaining (The Real Power)

Promises shine when chaining.

---

## 🔹 Returning Values

```js
Promise.resolve(5)
  .then((num) => {
    return num * 2;
  })
  .then((result) => {
    console.log(result); // 10
  });
```

Key rule:

> Whatever you return from `.then()` becomes the value of the next `.then()`.

---

## 🔹 Returning Another Promise

```js
function asyncDouble(num) {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve(num * 2);
    }, 1000);
  });
}

asyncDouble(5)
  .then((result) => {
    return asyncDouble(result);
  })
  .then((final) => {
    console.log(final); // 20
  });
```

Important:

> If you return a Promise, the next `.then()` waits for it.

This is called **Promise Flattening**.

---

## 🔹 Error Propagation (Very Important)

Errors automatically move down the chain.

```js
Promise.resolve(10)
  .then((num) => {
    throw new Error("Something broke");
  })
  .then(() => {
    console.log("Will not run");
  })
  .catch((err) => {
    console.error("Caught:", err.message);
  });
```

Rules:

* Throwing inside `.then()` = rejection
* Returning a rejected promise = rejection
* `.catch()` catches everything above it

---

## 🔹 Centralized Error Handling

```js
doStep1()
  .then(doStep2)
  .then(doStep3)
  .catch(handleError);
```

Cleaner than nested callbacks.

---

# 🔥 Important Concept: Promise Resolution Procedure

If you return:

| Return Type | What Happens                  |
| ----------- | ----------------------------- |
| Value       | Wrapped in resolved promise   |
| Promise     | Waits for it                  |
| Error       | Converted to rejected promise |

This automatic wrapping makes chaining smooth.

---

# 🔹 5. Static Promise Methods

These help handle multiple promises.

---

## 🟢 1. `Promise.all()`

Waits for ALL promises.

```js
Promise.all([
  Promise.resolve(1),
  Promise.resolve(2),
  Promise.resolve(3),
]).then((values) => {
  console.log(values); // [1, 2, 3]
});
```

If ANY promise rejects → whole thing rejects.

Use when:

* You need all results
* Parallel API calls

---

## 🟢 2. `Promise.allSettled()`

Waits for ALL, regardless of rejection.

```js
Promise.allSettled([
  Promise.resolve("Success"),
  Promise.reject("Failed"),
]).then((results) => {
  console.log(results);
});
```

Output structure:

```js
[
  { status: "fulfilled", value: "Success" },
  { status: "rejected", reason: "Failed" }
]
```

Use when:

* You want all results, even failures.

---

## 🟢 3. `Promise.race()`

Resolves/rejects with the FIRST settled promise.

```js
Promise.race([
  new Promise((res) => setTimeout(() => res("Slow"), 2000)),
  new Promise((res) => setTimeout(() => res("Fast"), 500)),
]).then(console.log);
```

Output:

```
Fast
```

Use for:

* Timeout logic
* Competing async tasks

---

## 🟢 4. `Promise.any()`

Resolves with the FIRST fulfilled promise.

```js
Promise.any([
  Promise.reject("Error 1"),
  Promise.resolve("Success"),
  Promise.reject("Error 2"),
]).then(console.log);
```

Output:

```
Success
```

If ALL reject → throws `AggregateError`.

Use when:

* You want first successful result

---

# 🔥 Comparison Summary

| Method       | Waits For       | Fails When      |
| ------------ | --------------- | --------------- |
| `all`        | All fulfilled   | Any rejects     |
| `allSettled` | All settled     | Never           |
| `race`       | First settled   | First rejection |
| `any`        | First fulfilled | All reject      |

---

# 🧠 Why Promises Fixed Callbacks

They provide:

* Controlled execution
* One-time resolution guarantee
* Chainable structure
* Automatic error bubbling
* No inversion of control

Instead of:

```js
doSomething(callback);
```

You now have:

```js
doSomething().then(...);
```

You control the chain.

---

# 🔥 Deep Internal Truth

Promises are:

* Microtask-based
* Eager (executor runs immediately)
* Immutable once settled
* Chainable state machines

---

# 🔴 6. Fetch API & Real-World Async

Now we move from theory to **real-world async**.

The **Fetch API** is the modern way to make HTTP requests in browsers and in modern runtimes like **Node.js** (v18+ has built-in `fetch`).

It is **Promise-based**, meaning everything you learned about Promises directly applies.

---

# 🔹 1. What is `fetch()`?

`fetch()` is a function that:

> Sends an HTTP request and returns a Promise that resolves to a `Response` object.

Basic syntax:

```js
fetch(url, options)
```

It returns a **Promise**.

---

# 🔹 2. Basic GET Request

```js
fetch("https://jsonplaceholder.typicode.com/posts/1")
  .then(response => response.json())
  .then(data => {
    console.log(data);
  })
  .catch(error => {
    console.error("Error:", error);
  });
```

What happens:

1. `fetch()` sends request
2. Server responds
3. Promise resolves with a `Response`
4. `response.json()` parses body (returns another Promise)
5. Final `.then()` receives actual data

---

# 🔥 Important: `fetch()` Only Rejects On Network Errors

This is critical.

If the server responds with:

* 404
* 500
* 403

`fetch()` **does NOT reject**.

It still resolves successfully.

You must manually check:

```js
fetch(url)
  .then(response => {
    if (!response.ok) {
      throw new Error("HTTP error: " + response.status);
    }
    return response.json();
  })
  .then(data => console.log(data))
  .catch(err => console.error(err));
```

---

# 🔹 3. Using Async/Await (Cleaner)

```js
async function getPost() {
  try {
    const response = await fetch(
      "https://jsonplaceholder.typicode.com/posts/1"
    );

    if (!response.ok) {
      throw new Error("Failed request");
    }

    const data = await response.json();
    console.log(data);

  } catch (error) {
    console.error("Error:", error);
  }
}

getPost();
```

This is much easier to read.

---

# 🔹 4. Handling JSON

Important:

`response.json()` returns a Promise.

Common mistake:

```js
const data = response.json(); // ❌ wrong
```

Correct:

```js
const data = await response.json(); // ✅
```

Other response methods:

* `response.text()`
* `response.blob()`
* `response.formData()`

---

# 🔹 5. HTTP Methods

By default, `fetch()` uses:

```
GET
```

To use other methods, pass options.

---

## 🟢 POST (Create Data)

```js
fetch("https://jsonplaceholder.typicode.com/posts", {
  method: "POST",
  headers: {
    "Content-Type": "application/json"
  },
  body: JSON.stringify({
    title: "New Post",
    body: "Content here",
    userId: 1
  })
})
.then(res => res.json())
.then(data => console.log(data));
```

Key things:

* Set `method`
* Set `Content-Type`
* Use `JSON.stringify()` for body

---

## 🟢 PUT (Update Entire Resource)

```js
fetch("https://jsonplaceholder.typicode.com/posts/1", {
  method: "PUT",
  headers: {
    "Content-Type": "application/json"
  },
  body: JSON.stringify({
    id: 1,
    title: "Updated",
    body: "Updated content",
    userId: 1
  })
});
```

---

## 🟢 PATCH (Partial Update)

```js
fetch("https://jsonplaceholder.typicode.com/posts/1", {
  method: "PATCH",
  headers: {
    "Content-Type": "application/json"
  },
  body: JSON.stringify({
    title: "Partially Updated"
  })
});
```

---

## 🟢 DELETE

```js
fetch("https://jsonplaceholder.typicode.com/posts/1", {
  method: "DELETE"
});
```

---

# 🔹 6. Proper Error Handling Pattern (Production-Level)

Here’s a reusable pattern:

```js
async function request(url, options = {}) {
  try {
    const response = await fetch(url, options);

    if (!response.ok) {
      const errorBody = await response.text();
      throw new Error(`HTTP ${response.status}: ${errorBody}`);
    }

    return await response.json();
  } catch (error) {
    console.error("Request failed:", error);
    throw error; // rethrow for caller
  }
}
```

Usage:

```js
request("https://jsonplaceholder.typicode.com/posts/1")
  .then(data => console.log(data))
  .catch(err => console.error(err));
```

---

# 🔹 7. AbortController (Cancel Requests)

Sometimes you need to cancel a request:

* User navigates away
* User types new search
* Timeout exceeded

Use:

```js
const controller = new AbortController();

fetch("https://jsonplaceholder.typicode.com/posts", {
  signal: controller.signal
})
  .then(res => res.json())
  .then(data => console.log(data))
  .catch(err => {
    if (err.name === "AbortError") {
      console.log("Request aborted");
    } else {
      console.error(err);
    }
  });

// Abort after 2 seconds
setTimeout(() => {
  controller.abort();
}, 2000);
```

How it works:

* `AbortController` provides a `signal`
* When `abort()` is called → fetch rejects
* Error name becomes `"AbortError"`

---

# 🔥 Real-World Pattern: Timeout with fetch

```js
function fetchWithTimeout(url, timeout = 5000) {
  const controller = new AbortController();
  const timer = setTimeout(() => controller.abort(), timeout);

  return fetch(url, { signal: controller.signal })
    .finally(() => clearTimeout(timer));
}
```

Now requests auto-cancel after timeout.

---

# 🔹 8. Common Real-World Issues

## ❌ Forgetting `await`

Leads to Promise instead of data.

## ❌ Not checking `response.ok`

Leads to silent HTTP failures.

## ❌ Not handling network errors

Leads to uncaught rejections.

## ❌ Not cancelling outdated requests

Causes race conditions in UI apps.

---

# 🔥 Mental Model

```text
fetch() → returns Promise<Response>
response.json() → returns Promise<Data>
Errors → must check response.ok
AbortController → cancels request
```

---


# 🟤 7. Advanced Event Loop Concepts

This is where **intermediate** developers become **advanced**.

At this level, we stop thinking:

> “Async runs later.”

And start thinking:

> “Exactly *when* does it run in the event loop cycle?”

We’ll cover:

* Microtasks vs Macrotasks
* `queueMicrotask`
* `process.nextTick()` (Node)
* `setImmediate()` (Node)
* Browser rendering interaction

---

# 🔹 1. Microtasks vs Macrotasks (Deep Level)

You already know:

After synchronous code finishes:

1. Run **all microtasks**
2. Run **one macrotask**
3. Repeat

But let's refine that.

---

## 🟢 Macrotasks (Task Queue)

Examples:

* `setTimeout`
* `setInterval`
* DOM events
* `setImmediate()` (Node)
* I/O callbacks (Node)

Each event loop cycle:

* Only **one macrotask** is executed.

---

## 🔵 Microtasks (Higher Priority Queue)

Examples:

* `Promise.then`
* `Promise.catch`
* `Promise.finally`
* `queueMicrotask`
* `MutationObserver`
* `process.nextTick()` (Node — even higher priority)

Important:

> The microtask queue is drained completely before moving to the next macrotask.

---

## 🔥 Execution Order Example

```js
console.log("1");

setTimeout(() => console.log("2"), 0);

Promise.resolve().then(() => console.log("3"));

console.log("4");
```

Output:

```
1
4
3
2
```

Because:

* Sync first
* Microtasks next
* Macrotasks last

---

# 🔹 2. `queueMicrotask()`

This explicitly schedules a microtask.

```js
queueMicrotask(() => {
  console.log("Microtask");
});
```

Why use it?

* When you want Promise-like scheduling
* But without creating a Promise
* More performant and intention-revealing

---

## Example

```js
console.log("Start");

queueMicrotask(() => {
  console.log("Microtask");
});

setTimeout(() => {
  console.log("Timeout");
}, 0);

console.log("End");
```

Output:

```
Start
End
Microtask
Timeout
```

Because microtasks always run before macrotasks.

---

# 🔥 Microtask Starvation (Advanced Problem)

```js
function loop() {
  queueMicrotask(loop);
}

loop();
```

What happens?

* Microtasks continuously refill themselves
* Macrotasks never execute
* UI freezes
* Rendering never happens

This is called:

> Microtask Starvation

Microtasks can block rendering.

---

# 🔹 3. `process.nextTick()` (Node.js)

Available in **Node.js**

This is NOT part of the browser.

It schedules a callback to run:

> Immediately after the current operation,
> BEFORE other microtasks.

It has **higher priority than Promises**.

---

## Example (Node)

```js
process.nextTick(() => {
  console.log("nextTick");
});

Promise.resolve().then(() => {
  console.log("promise");
});
```

Output:

```
nextTick
promise
```

Priority order in Node:

1. `process.nextTick`
2. Promise microtasks
3. Other phases

---

⚠️ Warning:

Excessive `nextTick` usage can freeze I/O phases.

---

# 🔹 4. `setImmediate()` (Node.js)

Also Node-only.

It schedules a callback to run:

> In the "check" phase of the Node event loop.

Example:

```js
setImmediate(() => {
  console.log("Immediate");
});
```

---

## `setTimeout(0)` vs `setImmediate()`

In Node:

Order is NOT always guaranteed.

Depends on:

* Whether you're inside I/O callback
* Current event loop phase

But generally:

* `setTimeout(fn, 0)` → timers phase
* `setImmediate(fn)` → check phase

In I/O callbacks:

`setImmediate()` usually runs before `setTimeout(0)`.

---

# 🔥 Node Event Loop Phases (Advanced)

Node’s event loop has phases:

1. Timers
2. Pending callbacks
3. Idle/prepare
4. Poll (I/O)
5. Check (`setImmediate`)
6. Close callbacks

Between each phase:

* Microtasks run
* `process.nextTick` runs immediately after each phase

This makes Node’s loop more complex than browsers.

---

# 🔹 5. Rendering Cycle Interaction (Browser)

In browsers like **Google Chrome**, the event loop also interacts with rendering.

Important:

> Rendering happens between macrotasks, not during them.

And:

> Rendering never happens during microtask execution.

---

## Rendering Steps (Simplified)

1. Run one macrotask
2. Drain microtasks
3. Update layout
4. Paint
5. Next frame

---

## 🔥 Why This Matters

Example:

```js
button.addEventListener("click", () => {
  element.style.color = "red";

  while (true) {} // blocking
});
```

The color change never appears.

Why?

Because:

* Rendering happens after task completion
* Infinite loop blocks completion
* No paint occurs

---

# 🔥 Microtasks Can Block Rendering

```js
button.addEventListener("click", () => {
  element.style.color = "red";

  Promise.resolve().then(function loop() {
    Promise.resolve().then(loop);
  });
});
```

This also blocks rendering.

Because:

* Microtasks are drained before painting
* Infinite microtask chain prevents paint

---

# 🔹 requestAnimationFrame (Bonus Advanced Concept)

Used for animation timing.

It runs:

> Right before the browser repaints.

```js
requestAnimationFrame(() => {
  console.log("Before paint");
});
```

Useful for:

* Smooth animations
* Layout calculations

---

# 🔥 Full Priority Order (Browser)

1. Synchronous code
2. Microtasks (Promises, queueMicrotask)
3. Rendering (if needed)
4. One macrotask
5. Repeat

---

# 🔥 Full Priority Order (Node.js)

1. Synchronous
2. `process.nextTick`
3. Promise microtasks
4. Event loop phases
5. `setImmediate`
6. Timers

---

# 🧠 Master Mental Model

Think of it like layers:

```
Call Stack
  ↓
process.nextTick (Node only)
  ↓
Microtask Queue
  ↓
Render (browser only)
  ↓
Macrotask Queue
```

---

# 🎯 Advanced Developer Insight

Most async bugs come from:

* Not understanding microtask timing
* Creating microtask starvation
* Misusing `nextTick`
* Assuming `setTimeout(0)` runs immediately
* Ignoring rendering timing

Senior engineers debug async issues by thinking in **event loop cycles**, not just “async vs sync”.

---

# ⚫ 8. Asynchronous Patterns & Control Flow

This is where you move from *knowing async* to **engineering async systems**.

We’re not learning syntax anymore.
We’re learning **control over execution timing and concurrency**.

---

# 🔹 1. Parallel Execution

Run multiple async operations at the same time.

### ❌ Slow (Sequential)

```js
await fetchUser();
await fetchOrders();
await fetchProducts();
```

Each waits for the previous → slow.

---

### ✅ Parallel with `Promise.all`

```js
const [user, orders, products] = await Promise.all([
  fetchUser(),
  fetchOrders(),
  fetchProducts()
]);
```

All start immediately.
Total time = slowest request.

---

### ⚠️ Failure Behavior

`Promise.all` fails fast:

* If one rejects → entire promise rejects.

If you need all results regardless:

```js
await Promise.allSettled([...]);
```

---

# 🔹 2. Sequential Execution (Controlled Order)

Sometimes order matters.

Example:

* Create user
* Then create profile
* Then send email

```js
const user = await createUser();
const profile = await createProfile(user.id);
await sendWelcomeEmail(user.email);
```

Sequential = predictable but slower.

---

## Sequential Loop Pattern (Important)

Wrong:

```js
array.forEach(async (item) => {
  await process(item);
});
```

`forEach` does NOT await properly.

Correct:

```js
for (const item of array) {
  await process(item);
}
```

This guarantees sequence.

---

# 🔹 3. Rate Limiting (Concurrency Control)

Sometimes you must limit:

* API request bursts
* Database connections
* External service quotas

---

## Example: Limit to 3 at a time

Basic concurrency pool:

```js
async function runWithLimit(tasks, limit) {
  const results = [];
  const executing = [];

  for (const task of tasks) {
    const p = task().then(res => {
      executing.splice(executing.indexOf(p), 1);
      return res;
    });

    results.push(p);
    executing.push(p);

    if (executing.length >= limit) {
      await Promise.race(executing);
    }
  }

  return Promise.all(results);
}
```

This ensures:

* Only `limit` promises run simultaneously.

---

# 🔹 4. Debouncing

Used for:

* Search inputs
* Resize events
* Typing suggestions

Definition:

> Delay execution until activity stops.

---

## Example

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

Usage:

```js
const handleSearch = debounce((query) => {
  fetchResults(query);
}, 500);
```

If user types continuously:

* Function runs only once after typing stops.

---

# 🔹 5. Throttling

Definition:

> Ensure a function runs at most once per interval.

Used for:

* Scroll events
* Mouse movement
* Window resizing

---

## Example

```js
function throttle(fn, limit) {
  let inThrottle = false;

  return function (...args) {
    if (!inThrottle) {
      fn.apply(this, args);
      inThrottle = true;

      setTimeout(() => {
        inThrottle = false;
      }, limit);
    }
  };
}
```

Difference from debounce:

| Debounce                   | Throttle                 |
| -------------------------- | ------------------------ |
| Waits until activity stops | Runs at fixed intervals  |
| Good for search            | Good for scroll tracking |

---

# 🔹 6. Retry Mechanisms

Real-world networks fail.

We retry intelligently.

---

## Basic Retry Pattern

```js
async function retry(fn, retries = 3) {
  try {
    return await fn();
  } catch (err) {
    if (retries === 0) throw err;
    return retry(fn, retries - 1);
  }
}
```

---

## Exponential Backoff (Professional Pattern)

```js
async function retryWithBackoff(fn, retries = 3, delay = 500) {
  try {
    return await fn();
  } catch (err) {
    if (retries === 0) throw err;

    await new Promise(res => setTimeout(res, delay));
    return retryWithBackoff(fn, retries - 1, delay * 2);
  }
}
```

Backoff pattern:

* 500ms
* 1000ms
* 2000ms
* 4000ms

Used in production systems.

---

# 🔹 7. Timeout Wrappers

Sometimes you want:

> "If this takes longer than X ms, cancel it."

---

## Timeout with Promise.race

```js
function withTimeout(promise, ms) {
  const timeout = new Promise((_, reject) => {
    setTimeout(() => reject(new Error("Timeout")), ms);
  });

  return Promise.race([promise, timeout]);
}
```

Usage:

```js
await withTimeout(fetchData(), 3000);
```

If fetch takes longer than 3s → reject.

---

## Advanced: Timeout + AbortController

Better approach for fetch:

```js
function fetchWithTimeout(url, ms) {
  const controller = new AbortController();

  const timer = setTimeout(() => {
    controller.abort();
  }, ms);

  return fetch(url, { signal: controller.signal })
    .finally(() => clearTimeout(timer));
}
```

This actually cancels network request.

---

# 🔥 Combining Patterns (Real Example)

Search bar:

* Debounce user input
* Cancel previous request
* Retry if fails
* Timeout if slow

This is real-world async engineering.

---

# 🧠 Pattern Selection Guide

| Problem                 | Pattern                    |
| ----------------------- | -------------------------- |
| Many independent calls  | Parallel (`Promise.all`)   |
| Ordered dependent steps | Sequential (`await` chain) |
| Too many requests       | Rate limiting              |
| Rapid user input        | Debounce                   |
| Continuous events       | Throttle                   |
| Unstable network        | Retry                      |
| Slow operations         | Timeout                    |

---

# 🟢 9. Async in Node.js

If you’re building backend systems with **Node.js**, async isn’t just about `fetch()` and Promises.

It’s about:

* Handling thousands of connections
* Managing I/O efficiently
* Avoiding blocking the event loop
* Scaling across CPU cores

Let’s go deep.

---

# 🔹 1. EventEmitter (Event-Driven Architecture)

Node is built around **events**.

Core class: `EventEmitter`

It allows objects to:

* Emit events
* Listen for events

---

## Basic Example

```js
const EventEmitter = require("events");

const emitter = new EventEmitter();

emitter.on("greet", (name) => {
  console.log(`Hello ${name}`);
});

emitter.emit("greet", "Alice");
```

Output:

```
Hello Alice
```

---

## How It Works Internally

* `emit()` triggers listeners
* Listeners run synchronously
* If async work inside → handled separately

Important:

> EventEmitter itself is synchronous.

---

## Real-World Usage

Used heavily in Node core:

* Streams
* HTTP server
* Process signals

Example:

```js
process.on("exit", () => {
  console.log("Process exiting");
});
```

---

# 🔹 2. Streams (Memory-Efficient Async)

Streams handle large data piece-by-piece instead of loading everything into memory.

Why streams matter:

* Efficient for large files
* Efficient for network data
* Prevent memory overflow

---

## Stream Types

1. Readable
2. Writable
3. Duplex
4. Transform

---

## Example: Reading File as Stream

```js
const fs = require("fs");

const stream = fs.createReadStream("largefile.txt");

stream.on("data", (chunk) => {
  console.log("Received chunk");
});

stream.on("end", () => {
  console.log("Finished reading");
});
```

Instead of:

```js
fs.readFile(...)
```

This prevents loading entire file into memory.

---

## Pipe Example (Powerful)

```js
const fs = require("fs");

fs.createReadStream("input.txt")
  .pipe(fs.createWriteStream("output.txt"));
```

`pipe()` handles:

* Backpressure
* Flow control
* Error propagation

---

# 🔥 Backpressure (Advanced Concept)

Backpressure occurs when:

> Data is being produced faster than consumed.

Streams automatically pause/resume to balance flow.

This is critical for high-performance systems.

---

# 🔹 3. File System Async APIs

Node provides both:

* Sync (blocking)
* Async (non-blocking)

---

## ❌ Blocking (Avoid in production)

```js
const data = fs.readFileSync("file.txt");
```

Blocks entire event loop.

---

## ✅ Non-blocking

```js
const fs = require("fs");

fs.readFile("file.txt", "utf8", (err, data) => {
  if (err) throw err;
  console.log(data);
});
```

---

## Modern Promise Version

```js
const fs = require("fs/promises");

async function readFile() {
  const data = await fs.readFile("file.txt", "utf8");
  console.log(data);
}
```

Recommended for modern code.

---

# 🔹 4. Timers in Node

Timers in Node are similar to browsers but tied to event loop phases.

Available:

* `setTimeout`
* `setInterval`
* `setImmediate`
* `process.nextTick`

---

## Execution Priority (Simplified)

1. Synchronous code
2. `process.nextTick`
3. Promise microtasks
4. Timers phase (`setTimeout`)
5. Check phase (`setImmediate`)

Example:

```js
setTimeout(() => console.log("timeout"), 0);
setImmediate(() => console.log("immediate"));
```

Order may vary depending on context.

---

# 🔹 5. Worker Threads (True Parallelism)

Important:

> Node is single-threaded for JS execution.

But CPU-heavy tasks block event loop.

Example blocking:

```js
while (true) {}
```

Kills server responsiveness.

---

## Worker Threads Fix That

Worker Threads allow:

* Running JS in parallel
* Using multiple CPU cores

---

## Basic Example

```js
const { Worker } = require("worker_threads");

const worker = new Worker("./worker.js");

worker.on("message", (msg) => {
  console.log("From worker:", msg);
});
```

Inside `worker.js`:

```js
const { parentPort } = require("worker_threads");

parentPort.postMessage("Hello from worker");
```

Workers:

* Run separate V8 instance
* Separate memory
* Communicate via message passing

---

## When to Use Workers

Use for:

* Image processing
* Crypto operations
* Large computations
* Data parsing

Do NOT use for simple I/O.

---

# 🔹 6. Cluster Module (Multi-Core Scaling)

Cluster allows:

> Running multiple Node processes to use all CPU cores.

Each process:

* Has its own event loop
* Shares same server port

---

## Example

```js
const cluster = require("cluster");
const http = require("http");
const os = require("os");

if (cluster.isMaster) {
  const numCPUs = os.cpus().length;

  for (let i = 0; i < numCPUs; i++) {
    cluster.fork();
  }
} else {
  http.createServer((req, res) => {
    res.end("Hello World");
  }).listen(3000);
}
```

Now:

* One process per CPU core
* Requests distributed automatically

---

# 🔥 Worker Threads vs Cluster

| Worker Threads                    | Cluster                 |
| --------------------------------- | ----------------------- |
| Same process                      | Multiple processes      |
| Shared memory possible            | No shared memory        |
| Good for CPU tasks                | Good for scaling server |
| Communication via message passing | IPC                     |

---

# 🧠 Backend Async Mental Model

In Node:

* I/O is non-blocking (libuv thread pool)
* JS runs on single main thread
* CPU-heavy tasks block event loop
* Use Workers for CPU
* Use Cluster for scaling across cores
* Use Streams for large data
* Use EventEmitter for event-driven design

---

# 🔵 10. Error Handling Strategies

Async systems don’t fail *if* — they fail *when*.

Senior engineers design systems assuming:

* Networks fail
* Services go down
* Timeouts happen
* Promises reject

This section is about building **resilient async systems**.

We’ll cover:

* Global unhandled rejections
* Graceful degradation
* Retrying failed requests
* Circuit breaker pattern
* Logging async errors

All in the context of **Node.js** (but principles apply everywhere).

---

# 🔹 1. Global Unhandled Rejections

## 🔥 The Problem

If a Promise rejects and no `.catch()` handles it:

```js
Promise.reject("Something broke");
```

Node will emit:

```
UnhandledPromiseRejectionWarning
```

In modern Node versions, unhandled rejections can **crash the process**.

---

## ✅ Global Handler

```js
process.on("unhandledRejection", (reason, promise) => {
  console.error("Unhandled Rejection:", reason);
});
```

Also handle:

```js
process.on("uncaughtException", (err) => {
  console.error("Uncaught Exception:", err);
  process.exit(1); // recommended
});
```

---

## 🎯 Best Practice

For backend systems:

* Log the error
* Gracefully shut down
* Restart process (use process manager like PM2 or Docker)

Do NOT ignore unhandled rejections.

---

# 🔹 2. Graceful Degradation

Definition:

> When something fails, the system still provides partial functionality.

---

## Example: Fallback Cache

```js
async function getUser(id) {
  try {
    return await fetchUserFromAPI(id);
  } catch (err) {
    console.log("Falling back to cache");
    return getUserFromCache(id);
  }
}
```

If API fails:

* Return cached data
* App continues functioning

---

## Real-World Examples

* Payment service down → save order, retry later
* Analytics fails → skip tracking
* Image fails → show placeholder

Resilience > Perfection.

---

# 🔹 3. Retrying Failed Requests

You already saw basic retry.
Now let’s do it properly.

---

## ❌ Bad Retry (Blind Retry)

```js
retry(apiCall, 5);
```

This can:

* Overload failing service
* Cause cascading failure

---

## ✅ Smart Retry Strategy

Retry only for:

* Network errors
* 5xx server errors
* Timeout errors

Do NOT retry:

* 400 errors
* Validation failures
* Auth errors

---

## Production-Level Retry with Backoff

```js
async function retryWithBackoff(fn, retries = 3, delay = 500) {
  try {
    return await fn();
  } catch (err) {
    if (retries === 0 || !shouldRetry(err)) {
      throw err;
    }

    await new Promise(res => setTimeout(res, delay));
    return retryWithBackoff(fn, retries - 1, delay * 2);
  }
}

function shouldRetry(err) {
  return err.code === "ECONNRESET" || err.status >= 500;
}
```

This prevents retry storms.

---

# 🔹 4. Circuit Breaker Pattern (Advanced Reliability)

This is serious production-level architecture.

Problem:

If a service keeps failing,
You keep retrying,
You overload it more,
Everything collapses.

---

## Circuit Breaker States

1. **Closed** → Normal operation
2. **Open** → Fail fast (don’t call service)
3. **Half-Open** → Test if service recovered

---

## Basic Implementation

```js
class CircuitBreaker {
  constructor(fn, failureThreshold = 3, timeout = 5000) {
    this.fn = fn;
    this.failureThreshold = failureThreshold;
    this.timeout = timeout;
    this.failures = 0;
    this.state = "CLOSED";
  }

  async call(...args) {
    if (this.state === "OPEN") {
      throw new Error("Circuit is open");
    }

    try {
      const result = await this.fn(...args);
      this.failures = 0;
      return result;
    } catch (err) {
      this.failures++;

      if (this.failures >= this.failureThreshold) {
        this.state = "OPEN";
        setTimeout(() => {
          this.state = "CLOSED";
        }, this.timeout);
      }

      throw err;
    }
  }
}
```

Now:

* After 3 failures → stop calling service
* Wait 5 seconds
* Try again

This protects your system.

---

# 🔹 5. Logging Async Errors Properly

Bad logging:

```js
catch (err) {
  console.log(err);
}
```

Good logging includes:

* Timestamp
* Stack trace
* Context
* Correlation ID (for distributed systems)

---

## Example Structured Logging

```js
catch (err) {
  console.error({
    message: err.message,
    stack: err.stack,
    service: "user-service",
    timestamp: new Date().toISOString()
  });
}
```

In real systems you’d use:

* Winston
* Pino
* Bunyan

But the principle matters more than the tool.

---

# 🔥 Async Error Propagation Best Practices

## ✅ Always return or throw inside async functions

Wrong:

```js
async function test() {
  try {
    await something();
  } catch (err) {
    console.log(err);
  }
}
```

This swallows the error.

Correct:

```js
catch (err) {
  console.error(err);
  throw err;
}
```

---

# 🔹 6. Centralized Express Error Handling (Backend Pattern)

In an Express app:

```js
app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).json({ error: "Internal Server Error" });
});
```

Wrap async routes:

```js
const asyncHandler = fn =>
  (req, res, next) =>
    Promise.resolve(fn(req, res, next)).catch(next);
```

Prevents unhandled promise rejections.

---

# 🔥 Defensive Async Design Principles

Senior-level mindset:

* Fail fast
* Retry wisely
* Protect dependencies
* Log everything meaningful
* Never swallow errors silently
* Assume external systems are unreliable

---

# 🧠 Error Strategy Decision Table

| Situation                  | Strategy             |
| -------------------------- | -------------------- |
| Network glitch             | Retry with backoff   |
| External service unstable  | Circuit breaker      |
| Optional feature fails     | Graceful degradation |
| Programming bug            | Crash & restart      |
| Unexpected async rejection | Global handler       |

---

# 🟣 11. Concurrency vs Parallelism

This is a **core theoretical concept** that separates:

* “I know async JavaScript”
  from
* “I understand how systems actually execute work.”

Let’s build this properly.

---

# 🔹 1. Concurrency vs Parallelism (Conceptual Difference)

## 🟢 Concurrency

> Multiple tasks making progress during overlapping time periods.

Not necessarily at the same time.

Think:

* One worker
* Switching between tasks
* Rapid context switching

Example:

* Handling 1000 HTTP requests with a single thread using non-blocking I/O.

---

## 🔵 Parallelism

> Multiple tasks executing literally at the same time.

Requires:

* Multiple CPU cores
* Multiple threads or processes

Example:

* Image processing on 4 cores simultaneously.

---

## 🧠 Simple Analogy

Concurrency = One chef juggling 5 dishes
Parallelism = 5 chefs cooking 5 dishes

---

# 🔹 2. JavaScript’s Concurrency Model

JavaScript (in both browser and **Node.js**) is:

* Single-threaded (for JS execution)
* Event-loop driven
* Non-blocking I/O

This means:

> JS achieves concurrency via asynchronous I/O, not parallel execution.

---

## How JS Achieves Concurrency

1. One call stack
2. Non-blocking I/O
3. Event loop
4. Callback queues
5. Background system threads (libuv in Node, browser APIs in browser)

The JS thread never waits for I/O.

It delegates.

---

## Example (Concurrent but Not Parallel)

```js
await Promise.all([
  fetch("/api/1"),
  fetch("/api/2"),
  fetch("/api/3")
]);
```

All requests happen concurrently.

But:

* JS thread is not running 3 things at once.
* The network stack handles I/O in background.
* JS reacts when results return.

That is concurrency.

---

# 🔹 3. CPU-Bound vs I/O-Bound Tasks

This is critical.

---

## 🟢 I/O-Bound Tasks

Spend most time waiting for:

* Network
* Disk
* Database
* File system

Example:

```js
await fetchData();
```

CPU usage is low.

JS concurrency model handles this beautifully.

---

## 🔴 CPU-Bound Tasks

Spend most time doing calculations:

* Image processing
* Cryptography
* Data compression
* Large JSON parsing
* Machine learning inference

Example:

```js
while (true) {}
```

This blocks:

* Event loop
* All incoming requests
* Everything

JS alone cannot handle CPU-bound concurrency safely.

This is where parallelism tools come in.

---

# 🔹 4. Web Workers (Browser Parallelism)

In browsers like **Google Chrome**, we use:

> Web Workers

They allow:

* Running JS in separate threads
* True parallel execution
* No blocking of UI thread

---

## Basic Example

Main thread:

```js
const worker = new Worker("worker.js");

worker.postMessage(10);

worker.onmessage = (event) => {
  console.log("Result:", event.data);
};
```

worker.js:

```js
onmessage = function(event) {
  const result = event.data * 2;
  postMessage(result);
};
```

Each worker:

* Has its own memory
* Has its own event loop
* Cannot access DOM

Communication happens via message passing.

---

# 🔹 5. Worker Threads (Node Parallelism)

In **Node.js**, we use:

> Worker Threads

They provide:

* True parallel execution
* Separate V8 instances
* Message-based communication

---

## Basic Example

Main file:

```js
const { Worker } = require("worker_threads");

const worker = new Worker("./worker.js");

worker.on("message", (msg) => {
  console.log("From worker:", msg);
});
```

worker.js:

```js
const { parentPort } = require("worker_threads");

parentPort.postMessage("Hello from worker");
```

---

## When to Use Worker Threads

Use for:

* Heavy CPU calculations
* Image manipulation
* Data transformation
* Encryption

Do NOT use for:

* Simple async I/O
* Regular HTTP handling

---

# 🔹 6. Cluster Module (Process-Level Parallelism)

Also in Node:

* Uses multiple processes
* One per CPU core
* Shared server port

Each process:

* Has its own memory
* Own event loop
* Own thread

This is parallelism at process level.

---

# 🔹 7. Comparing Models

| Feature                  | Concurrency     | Parallelism |
| ------------------------ | --------------- | ----------- |
| Executes at same time?   | Not necessarily | Yes         |
| Requires multiple cores? | No              | Yes         |
| JS event loop based?     | Yes             | No          |
| Uses Workers?            | No              | Yes         |

---

# 🔥 Key Insight

JavaScript is:

* Concurrent by default
* Not parallel by default

Parallelism must be explicitly enabled.

---

# 🔹 8. Performance Decision Framework

Ask:

Is the task I/O-bound?
→ Use async/await
→ Use Promise.all
→ Let event loop handle it

Is the task CPU-bound?
→ Use Worker Threads (Node)
→ Use Web Workers (browser)
→ Use Cluster if scaling server

---

# 🔥 Real Backend Scenario

Handling 10,000 HTTP requests:

* If mostly DB/network calls → concurrency is enough.
* If doing encryption on each request → need parallelism.

Otherwise:

* Event loop blocks
* Latency spikes
* Throughput drops

---

# 🔹 9. Advanced Insight: Why Node Is Still Fast

Even though JS is single-threaded:

* libuv uses a thread pool for I/O
* OS handles networking
* Kernel manages scheduling

So concurrency is achieved without blocking JS thread.

JS orchestrates.
System does heavy lifting.

---

# 🧠 Mental Model

Think of JavaScript as:

A conductor (event loop)
Not the orchestra (system threads).

Concurrency = Efficient orchestration
Parallelism = More musicians

---

# 🔴 12. Performance & Optimization

At this level, you’re no longer just writing async code —
you’re making sure it **scales, performs, and doesn’t break under load**.

We’ll cover:

* Avoiding blocking code
* Memory leaks with async
* Async stack traces
* Profiling async code (DevTools)

This applies to both browsers like **Google Chrome** and backend systems using **Node.js**.

---

# 🔹 1. Avoiding Blocking Code

JavaScript runs on a **single thread**.

If you block it:

* UI freezes (browser)
* All requests stall (Node)
* Throughput collapses

---

## 🔴 Blocking Example (CPU-bound)

```js
while (true) {}
```

Or:

```js
const data = JSON.parse(veryLargeJSON);
```

Or:

```js
crypto.pbkdf2Sync(...)
```

All block the event loop.

---

## 🟢 Fix Strategies

### 1️⃣ Break work into chunks

```js
function processLargeArray(arr) {
  let i = 0;

  function chunk() {
    const end = Math.min(i + 1000, arr.length);

    while (i < end) {
      doWork(arr[i]);
      i++;
    }

    if (i < arr.length) {
      setTimeout(chunk, 0);
    }
  }

  chunk();
}
```

This yields control back to the event loop.

---

### 2️⃣ Use Worker Threads (CPU tasks)

Move heavy work off main thread.

---

### 3️⃣ Avoid Sync APIs in Node

❌ Bad:

```js
fs.readFileSync("file.txt");
```

✅ Good:

```js
await fs.readFile("file.txt");
```

---

# 🔹 2. Memory Leaks with Async

Memory leaks in async systems are subtle and dangerous.

---

## 🔥 Common Causes

### 1️⃣ Unresolved Promises

```js
new Promise(() => {
  // never resolves
});
```

If references are held → memory retained.

---

### 2️⃣ Unbounded Caches

```js
const cache = {};

async function getUser(id) {
  if (!cache[id]) {
    cache[id] = await fetchUser(id);
  }
  return cache[id];
}
```

Without eviction → memory grows forever.

---

### 3️⃣ Event Listeners Not Removed

```js
emitter.on("event", handler);
```

If never removed:

* Listeners accumulate
* Memory increases

Use:

```js
emitter.removeListener("event", handler);
```

Or:

```js
emitter.once("event", handler);
```

---

### 4️⃣ Closures Capturing Large Objects

```js
function outer() {
  const bigData = new Array(1_000_000).fill("x");

  return function inner() {
    console.log("Still holding bigData");
  };
}
```

If `inner` survives → bigData stays in memory.

---

### 5️⃣ setInterval Without clearInterval

```js
setInterval(() => {
  doWork();
}, 1000);
```

If not cleared:

* Timer stays forever
* Memory + CPU cost accumulates

---

# 🔹 3. Async Stack Traces

In synchronous code:

Stack traces are clean.

In async code:

The call stack breaks across event loop ticks.

---

## Old Problem

Before modern engines:

```js
async function a() {
  await b();
}

async function b() {
  throw new Error("Boom");
}
```

Stack trace only showed `b`.

---

## Modern Solution

Modern engines (like V8 in **Google Chrome** and **Node.js**) support:

> Async stack traces

They preserve async call chains.

You’ll see:

```
Error: Boom
  at b
  at async a
```

---

## Improve Debugging

In Node:

Run with:

```bash
node --trace-warnings app.js
```

Or:

```bash
node --inspect app.js
```

---

# 🔹 4. Profiling Async Code (DevTools)

Now we move into performance engineering.

---

# 🟢 A. Browser Profiling (Chrome DevTools)

In **Google Chrome**:

1. Open DevTools
2. Go to "Performance"
3. Click Record
4. Interact with app
5. Stop recording

You’ll see:

* Main thread activity
* Long tasks (>50ms)
* Network calls
* Layout & paint timing

---

## 🔥 Look For:

* Long blocking tasks
* Large scripting time
* Repeated layout recalculations
* Excessive microtasks

---

# 🟢 B. Memory Profiling

DevTools → Memory tab

Use:

* Heap snapshot
* Allocation timeline

Look for:

* Detached DOM nodes
* Growing objects
* Retained closures

---

# 🟢 C. Node Profiling

In **Node.js**:

Start with:

```bash
node --inspect server.js
```

Then open Chrome → chrome://inspect

Use:

* CPU profiler
* Heap snapshots

---

## 🔥 Event Loop Blocking Detection

Use:

```js
const start = Date.now();

setInterval(() => {
  const delay = Date.now() - start - 1000;
  console.log("Event loop delay:", delay);
}, 1000);
```

Or use libraries like:

* `clinic.js`
* `0x`
* `autocannon` (for load testing)

---

# 🔹 5. Long Task Rule (Browser)

If a task runs longer than 50ms:

* It’s considered a long task
* It blocks rendering
* It hurts UX

Break tasks into smaller pieces.

---

# 🔹 6. Performance Optimization Checklist

## Backend (Node)

* Avoid sync APIs
* Limit concurrent promises
* Use streams for large data
* Monitor memory growth
* Use Worker Threads for CPU-heavy work

## Frontend (Browser)

* Avoid heavy work in click handlers
* Debounce input events
* Avoid infinite microtask loops
* Use requestAnimationFrame for animations

---

# 🔥 Senior-Level Insight

Performance problems in async systems usually come from:

* Too many concurrent promises
* Blocking JSON parsing
* Memory retention via closures
* Unbounded event listeners
* Microtask starvation
* Excessive retries

---

# 🧠 Final Mental Model

Performance =

(Event Loop Health)

* (Memory Stability)
* (CPU Usage Control)
* (Concurrency Control)

Async makes things *possible*.

Performance engineering makes them *scalable*.

---

# 🟤 13. Testing Async Code

Async code is harder to test because:

* Execution timing is non-linear
* Errors may happen in microtasks
* Timers introduce delays
* External APIs add unpredictability

Professional testing means making async code:

* Deterministic
* Fast
* Isolated
* Observable

We’ll use common tools like **Jest** and concepts that apply to **Node.js** and browser environments.

---

# 🔹 1. Testing Promises

## ✅ Return the Promise

If you forget to return the Promise, the test may pass before it finishes.

### ❌ Wrong

```js
test("fetches data", () => {
  fetchData().then(data => {
    expect(data).toBe("hello");
  });
});
```

Test ends before `.then()` runs.

---

### ✅ Correct

```js
test("fetches data", () => {
  return fetchData().then(data => {
    expect(data).toBe("hello");
  });
});
```

Or better…

---

# 🔹 2. Testing async/await

Cleaner and safer.

```js
test("fetches data", async () => {
  const data = await fetchData();
  expect(data).toBe("hello");
});
```

If `fetchData` rejects → test automatically fails.

---

# 🔹 3. Testing Rejections

## Promise version

```js
test("throws error", () => {
  return expect(fetchData()).rejects.toThrow("Network error");
});
```

## Async/await version

```js
test("throws error", async () => {
  await expect(fetchData()).rejects.toThrow("Network error");
});
```

Important:

> Use `.rejects`, not try/catch inside test unless necessary.

---

# 🔹 4. Mocking APIs

You should NOT call real APIs in unit tests.

Reasons:

* Slow
* Flaky
* Dependent on network
* Break CI

---

## 🟢 Mocking fetch (Jest)

```js
global.fetch = jest.fn(() =>
  Promise.resolve({
    ok: true,
    json: () => Promise.resolve({ name: "Alice" })
  })
);
```

Now your code:

```js
const data = await fetchUser();
expect(data.name).toBe("Alice");
```

No real HTTP request happens.

---

## 🟢 Mocking Modules

```js
jest.mock("./api");

const api = require("./api");

api.fetchUser.mockResolvedValue({ name: "Bob" });
```

Or:

```js
api.fetchUser.mockRejectedValue(new Error("Fail"));
```

This gives full control over behavior.

---

# 🔹 5. Handling Timers in Tests

Timers cause delays in tests.

Instead of waiting real time, use **fake timers**.

---

## 🟢 Using Fake Timers (Jest)

```js
jest.useFakeTimers();
```

Example:

```js
function delayed() {
  return new Promise(resolve => {
    setTimeout(() => resolve("done"), 2000);
  });
}
```

Test:

```js
test("resolves after timeout", async () => {
  jest.useFakeTimers();

  const promise = delayed();

  jest.advanceTimersByTime(2000);

  await expect(promise).resolves.toBe("done");
});
```

No real 2-second wait.

---

## 🟢 Flushing Microtasks

Promises run in microtask queue.

Sometimes you need to flush them:

```js
await Promise.resolve();
```

Or in Jest:

```js
await jest.runAllTicks();
```

---

# 🔹 6. Testing setInterval

Example:

```js
function startCounter(callback) {
  let count = 0;

  const id = setInterval(() => {
    count++;
    callback(count);
  }, 1000);

  return id;
}
```

Test:

```js
jest.useFakeTimers();

test("calls callback every second", () => {
  const mock = jest.fn();

  startCounter(mock);

  jest.advanceTimersByTime(3000);

  expect(mock).toHaveBeenCalledTimes(3);
});
```

---

# 🔹 7. Testing Concurrency

If testing `Promise.all`:

```js
test("runs in parallel", async () => {
  const spy = jest.fn();

  const tasks = [
    Promise.resolve().then(spy),
    Promise.resolve().then(spy)
  ];

  await Promise.all(tasks);

  expect(spy).toHaveBeenCalledTimes(2);
});
```

You verify behavior, not timing.

---

# 🔹 8. Testing Retry Logic

Example retry function:

```js
apiCall
  .mockRejectedValueOnce(new Error("fail"))
  .mockResolvedValueOnce("success");
```

Test:

```js
const result = await retry(apiCall, 2);

expect(apiCall).toHaveBeenCalledTimes(2);
expect(result).toBe("success");
```

---

# 🔹 9. Testing with AbortController

Mock aborted fetch:

```js
fetch.mockRejectedValue(
  Object.assign(new Error("Aborted"), { name: "AbortError" })
);
```

Test:

```js
await expect(fetchData()).rejects.toThrow("Aborted");
```

---

# 🔥 Common Async Testing Mistakes

### ❌ Forgetting to return Promise

### ❌ Mixing done() with async/await

### ❌ Not awaiting expect().resolves

### ❌ Using real timers in unit tests

### ❌ Not mocking external dependencies

---

# 🔹 10. done() Callback (Legacy Style)

Older pattern:

```js
test("callback test", done => {
  fetchData().then(data => {
    expect(data).toBe("hello");
    done();
  });
});
```

Avoid this unless testing raw callback APIs.

Prefer async/await.

---

# 🔥 Professional Testing Strategy

For async systems:

* Unit test pure logic
* Mock all I/O
* Use fake timers
* Test failure paths
* Test retries
* Test timeouts
* Test cancellation

---

# 🧠 Mental Model

Async testing =

Control time
Control dependencies
Control resolution

If you don’t control those, tests become flaky.

---

# ⚫ 14. Advanced Topics (Expert Level)

This is where you stop being “a JS developer”
and start thinking like a **runtime engineer**.

We’ll go deep into:

* Async Iterators (`for await...of`)
* Generators
* Observables (RxJS)
* Custom Promise implementation
* How V8 handles async internally

This applies to environments like **Node.js** and browsers powered by **Google Chrome**, which use the V8 engine.

---

# 🔹 1. Async Iterators (`for await...of`)

## 🧠 The Problem They Solve

When you have **asynchronous streams of values**, like:

* Reading a file chunk by chunk
* Receiving WebSocket messages
* Streaming API responses

You need to process values **as they arrive**.

---

## 🔹 What Is an Async Iterator?

An object that implements:

```js
Symbol.asyncIterator
```

And returns:

```js
{ value, done }
```

wrapped in a Promise.

---

## 🔹 Basic Example

```js
async function* asyncGenerator() {
  yield 1;
  yield 2;
  yield 3;
}
```

Consume it:

```js
for await (const value of asyncGenerator()) {
  console.log(value);
}
```

Output:

```
1
2
3
```

Each `yield` is wrapped in a Promise automatically.

---

## 🔹 Real-World Example (Streaming)

In **Node.js**:

```js
const fs = require("fs");

async function readFile() {
  const stream = fs.createReadStream("file.txt");

  for await (const chunk of stream) {
    console.log(chunk.toString());
  }
}
```

You’re consuming a stream asynchronously.

---

## 🔥 Why This Is Powerful

It combines:

* Iteration
* Streaming
* Backpressure
* Async control flow

Into a clean syntax.

---

# 🔹 2. Generators (Foundation of Async/Await)

Before async/await existed, we had generators.

---

## 🔹 Basic Generator

```js
function* generator() {
  yield 1;
  yield 2;
  yield 3;
}
```

Usage:

```js
const gen = generator();

gen.next(); // { value: 1, done: false }
gen.next(); // { value: 2, done: false }
gen.next(); // { value: 3, done: false }
gen.next(); // { value: undefined, done: true }
```

---

## 🔥 Key Idea

Generators can:

* Pause execution
* Resume later
* Maintain internal state

This is cooperative multitasking.

---

## 🔹 Generators + Promises = Async Before Async

Libraries used to do:

```js
function* fetchData() {
  const data = yield fetch("/api");
  return data.json();
}
```

A runner would manually resume generator when Promise resolved.

That’s literally how async/await works under the hood.

---

# 🔹 3. Observables (Reactive Programming)

Popularized by **RxJS**.

---

## 🧠 Difference from Promises

Promise:

* One value
* Once
* Then done

Observable:

* Multiple values
* Over time
* Push-based stream

---

## 🔹 Basic Example

```js
import { Observable } from "rxjs";

const observable = new Observable(subscriber => {
  subscriber.next(1);
  subscriber.next(2);
  subscriber.next(3);
  subscriber.complete();
});
```

Subscribe:

```js
observable.subscribe({
  next: value => console.log(value),
  complete: () => console.log("Done")
});
```

---

## 🔥 Why Observables Matter

They handle:

* Event streams
* UI events
* WebSockets
* Real-time data

With powerful operators:

```js
map
filter
debounceTime
merge
switchMap
```

Observables are like:

> Promise + EventEmitter + Streams combined.

---

# 🔹 4. Custom Promise Implementation (Core Concept)

Let’s simplify how a Promise works.

---

## 🔹 Minimal Implementation

```js
class MyPromise {
  constructor(executor) {
    this.state = "pending";
    this.value = undefined;
    this.handlers = [];

    const resolve = (value) => {
      if (this.state !== "pending") return;

      this.state = "fulfilled";
      this.value = value;

      this.handlers.forEach(h => h(value));
    };

    executor(resolve);
  }

  then(handler) {
    if (this.state === "fulfilled") {
      handler(this.value);
    } else {
      this.handlers.push(handler);
    }
  }
}
```

---

## 🔥 What Real Promises Add

Real ES Promises add:

* Rejection handling
* Microtask scheduling
* Chaining
* Thenable resolution
* Error bubbling
* Spec compliance

Real implementation is complex (~1000+ lines in V8).

---

# 🔹 5. How V8 Handles Async Internally

Used by **Google Chrome** and **Node.js**.

Let’s go lower level.

---

## 🔹 Step 1: Async Functions Become Generators

This:

```js
async function test() {
  const result = await fetchData();
  return result;
}
```

Is transformed roughly into:

```js
function test() {
  return new Promise((resolve, reject) => {
    const generator = internalGenerator();

    function step(nextValue) {
      const { value, done } = generator.next(nextValue);

      if (done) {
        resolve(value);
      } else {
        Promise.resolve(value).then(step, reject);
      }
    }

    step();
  });
}
```

So:

* `await` pauses generator
* Promise resolution resumes it

---

## 🔹 Step 2: Microtask Queue

When a Promise resolves:

* V8 schedules its `.then()` handlers
* Into the microtask queue
* Microtasks run before next macrotask

Execution order:

```
Call Stack
↓
Microtasks
↓
Rendering (browser)
↓
Macrotasks
```

---

## 🔹 Step 3: Hidden Classes & Optimization

V8 optimizes:

* Promise allocations
* Async function call frames
* Inline caching
* Escape analysis

Async stack traces are preserved by storing hidden metadata.

---

# 🔹 6. Memory & Optimization Details

V8 uses:

* Heap for objects
* Stack for execution frames
* Garbage collector (mark-and-sweep)

Async functions retain closures.

If you keep references:

* Memory won’t free
* Async leaks happen

---

# 🔥 Senior-Level Insight

Performance pitfalls:

* Massive Promise creation loops
* Deep microtask chains
* Unhandled rejections
* Promise inside tight loops
* Await inside hot CPU paths

---

# 🔹 7. Observables vs Async Iterators vs Promises

| Feature         | Promise | Async Iterator | Observable |
| --------------- | ------- | -------------- | ---------- |
| Single value    | ✅       | ❌              | ❌          |
| Multiple values | ❌       | ✅              | ✅          |
| Lazy            | ❌       | ✅              | ✅          |
| Cancelable      | ❌       | Limited        | ✅          |
| Push-based      | ❌       | Pull-based     | ✅          |

---

# 🧠 Final Mental Model

Promises → Future value
Async Iterators → Stream of async values
Generators → Pausable execution
Observables → Reactive streams
V8 → Optimized state machine + microtask scheduler

---

