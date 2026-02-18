# JavaScript

JavaScript is one of the core technologies of the web, alongside HTML and CSS. It is responsible for adding interactivity, logic, and dynamic behavior to websites and applications.

---

## What is JavaScript?

- JavaScript is a **high-level**, **dynamically typed**, **multi-paradigm**, and **general-purpose** programming language.
- It was created in **1995** by **Brendan Eich** in just **10 days**.
- Originally named **Mocha**, it was later renamed **LiveScript**, and finally **JavaScript**.

Today, JavaScript is one of the **most widely used programming languages in the world**.

---

# Where JavaScript is Used

JavaScript is no longer limited to browsers — it powers entire ecosystems.

## Frontend Development
Used to build interactive user interfaces.

Popular frameworks:
- React  
- Angular  
- Vue  

---

## Backend Development
JavaScript can run on servers using runtime environments.

Popular runtimes:
- Node.js  
- Deno  
- Bun  

---

## Mobile App Development
- React Native allows developers to build cross-platform mobile apps using JavaScript.

---

## Desktop Applications
- Electron enables developers to create desktop apps using web technologies.

Examples:
- VS Code  
- Slack  

---

## Build Tools
JavaScript powers modern tooling that improves developer productivity.

Examples:
- Webpack  
- Babel  
- Vite  

---

## Internet of Things (IoT)
JavaScript can also be used to control hardware devices and embedded systems.

---

# Key Features of JavaScript

## Dynamically Typed
- Variable types are determined at **runtime**, not during compilation.
- You do not need to explicitly declare types.

### Example:
```javascript
let value = 10;      // Number
value = "Hello";     // Now a String
```

✅ Flexible but requires careful coding to avoid runtime errors.

---

## High-Level Language
- JavaScript syntax is closer to human language.
- Developers don't need to manage low-level memory operations.

✅ Easier to learn and write compared to low-level languages.

---

## Multi-Paradigm Language

JavaScript supports multiple programming styles:

### 1. Procedural Programming
Step-by-step instructions.

```javascript
let total = 0;
total += 5;
```

---

### 2. Object-Oriented Programming (Prototype-Based)
Objects inherit from other objects using prototypes.

```javascript
const user = {
  name: "John",
  greet() {
    console.log("Hello!");
  }
};
```

---

### 3. Functional Programming
Functions are treated as first-class citizens.

```javascript
const add = (a, b) => a + b;
```

✅ This flexibility makes JavaScript extremely powerful.

---

# ECMAScript

## What is ECMAScript?

- **ECMAScript** is the official standard specification for JavaScript.
- Documented as **ECMA-262**.
- Maintained by the **TC39 committee**.

👉 JavaScript is an **implementation** of the ECMAScript standard.

---

## ES6 (ECMAScript 2015)

One of the biggest updates in JavaScript history.

### Major Features Introduced:
- `let` and `const`
- Arrow functions
- Classes
- Modules
- Promises
- Template literals
- Destructuring

### Example:
```javascript
const greet = name => `Hello, ${name}`;
```

---

## Continuous Evolution
JavaScript continues to improve with **annual updates**, adding modern features and performance enhancements.

---

# JavaScript Engine

A **JavaScript engine** is a program that reads and executes JavaScript code.

## Popular Engines

| Browser | Engine |
|--------|--------|
| Chrome / Edge | V8 |
| Firefox | SpiderMonkey |
| Safari | JavaScriptCore |

---

# Runtime Environment

A **runtime** is more than just the engine.

### Runtime = Engine + Environment + APIs

---

## Browser Runtime
Includes:
- JavaScript Engine (e.g., V8)
- DOM (Document Object Model)
- Fetch API
- Timers (`setTimeout`, `setInterval`)

Allows interaction with web pages.

---

## Node.js Runtime
Includes:
- V8 Engine
- File System access
- Networking capabilities
- Process management

Allows JavaScript to run outside the browser.

---

# Memory Management

JavaScript automatically manages memory using a **Garbage Collector**.

## Garbage Collection
- Detects unused objects.
- Frees memory automatically.

✅ Developers do NOT need to manually allocate or free memory.

This reduces common programming errors like memory leaks.

---

# Interpreted vs Compiled

JavaScript is traditionally known as an **interpreted language**, but modern engines are more advanced.

## Just-In-Time (JIT) Compilation
Modern engines:

1. Read the code  
2. Compile it into machine code  
3. Execute it immediately  

✅ Result: Much faster performance.

---

# Code Execution Process

When JavaScript runs, it follows these steps:

1. **Read the Code**
2. **Parse** it into an AST (Abstract Syntax Tree)
3. **Compile** into bytecode or machine code using JIT
4. **Execute** the code

This entire process happens extremely fast.

---

# Concurrency Model

## Single-Threaded Nature
JavaScript executes **one task at a time** using a single call stack.

👉 This means it can only process one piece of code at any given moment.

---

## How JavaScript Handles Async Operations

Instead of blocking execution, JavaScript uses the **Event Loop**.

### Components of the Event Loop:
- Call Stack  
- Web APIs  
- Task Queue  
  - Microtasks (Promises)  
  - Macrotasks (setTimeout, setInterval)  
- Event Loop  

✅ Enables **non-blocking** behavior, making apps faster and more responsive.

---

# Unique Advantage

> **“JavaScript is the only programming language that runs natively inside web browsers.”**

Every modern browser understands JavaScript without requiring additional installation.

This makes it the **foundation of modern web development.**

---

# Why Learn JavaScript?

- Powers the modern web  
- Massive ecosystem  
- High demand in the job market  
- Supports frontend + backend  
- Beginner-friendly yet powerful  
- Constantly evolving  

👉 Mastering JavaScript opens the door to frameworks like **React**, **Next.js**, and **Node.js**.
