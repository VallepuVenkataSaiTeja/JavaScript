## What is JavaScript (JS)?

**JavaScript (JS)** is a high-level, dynamic, interpreted programming language mainly used to make web pages interactive. It allows you to create things like:

* Interactive forms
* Animations
* Dynamic content updates
* Games
* Web applications

It is one of the core technologies of the web, alongside:

* **HTML** – Structure of web pages
* **CSS** – Styling and layout
* **JavaScript** – Behavior and interactivity

---

## Where Does JavaScript Run?

### 1️⃣ In the Browser (Client-Side)

JavaScript runs inside web browsers like:

* Google Chrome
* Mozilla Firefox
* Safari
* Microsoft Edge

In the browser, JavaScript can:

* Manipulate the DOM (Document Object Model)
* Respond to user actions (clicks, typing)
* Communicate with servers (APIs)
* Update content without reloading the page

Each browser has its own JavaScript engine, such as:

* **V8** (used in Chrome)
* **SpiderMonkey** (used in Firefox)

---

### 2️⃣ On the Server (Node.js)

JavaScript can also run outside the browser using **Node.js**.

Node.js allows you to:

* Build backend servers
* Create APIs
* Work with databases
* Build real-time applications (chat apps, streaming apps)
* Create command-line tools

Node.js uses the **V8 engine** from Google Chrome to execute JavaScript.

---

## Brief History of JavaScript

### 🔹 1995 – Creation

* JavaScript was created in 1995 by **Brendan Eich**.
* It was developed at **Netscape**.
* It was built in just **10 days**.
* Originally called **Mocha**, then **LiveScript**, and finally renamed **JavaScript** (for marketing reasons related to Java’s popularity).

---

### 🔹 1997 – Standardization (ECMAScript)

To ensure consistency across browsers, JavaScript was standardized as **ECMAScript** by **ECMA International**.

ECMAScript defines the official language specification.

---

### 🔹 2009 – Node.js Released

* **Node.js** was created by **Ryan Dahl**.
* This allowed JavaScript to run on servers, not just browsers.
* It significantly expanded JavaScript’s use beyond front-end development.

---

### 🔹 2015 – ES6 (Major Update)

**ECMAScript 2015 (ES6)** introduced major features like:

* `let` and `const`
* Arrow functions (`=>`)
* Classes
* Modules
* Promises

This made JavaScript more powerful and structured.

---

## Why JavaScript Is So Popular

* Runs in every web browser
* Full-stack capability (frontend + backend)
* Huge ecosystem (npm packages)
* Strong community support
* Used in frameworks like React, Angular, and Vue

---

## Simple Summary

| Topic              | Explanation                                  |
| ------------------ | -------------------------------------------- |
| What is JS?        | A programming language for web interactivity |
| Where does it run? | Browser and server (Node.js)                 |
| Created by         | Brendan Eich (1995)                          |
| Standard name      | ECMAScript                                   |
| Why important?     | Powers modern web applications               |

---

## JavaScript Variables: `var`, `let`, and `const`

In **JavaScript**, variables are used to store data. There are three main ways to declare variables:

```js
var
let
const
```

They differ mainly in **scope**, **reassignment**, and **hoisting behavior**.

---

# 1️⃣ `var`

### ✅ Scope: Function-scoped

### ✅ Can be reassigned

### ✅ Can be redeclared

### ⚠️ Hoisted (initialized as `undefined`)

### Example:

```js
function test() {
  if (true) {
    var x = 10;
  }
  console.log(x); // 10 (accessible outside block)
}
```

`var` ignores block scope (`{}`) and is only limited by function scope.

### Hoisting behavior:

```js
console.log(a); // undefined
var a = 5;
```

Behind the scenes:

```js
var a;
console.log(a); // undefined
a = 5;
```

---

# 2️⃣ `let`

### ✅ Scope: Block-scoped

### ✅ Can be reassigned

### ❌ Cannot be redeclared in same scope

### ⚠️ Hoisted but NOT initialized (Temporal Dead Zone)

### Example:

```js
if (true) {
  let y = 20;
}
console.log(y); // ❌ Error (block scoped)
```

### Reassignment allowed:

```js
let count = 1;
count = 2; // ✅ allowed
```

### Redeclaration not allowed:

```js
let z = 5;
let z = 10; // ❌ Error
```

### Temporal Dead Zone (TDZ):

```js
console.log(a); // ❌ ReferenceError
let a = 10;
```

The variable exists but cannot be accessed before its declaration line.

---

# 3️⃣ `const`

### ✅ Scope: Block-scoped

### ❌ Cannot be reassigned

### ❌ Cannot be redeclared

### ⚠️ Must be initialized when declared

### Example:

```js
const PI = 3.14;
PI = 3.14159; // ❌ Error
```

### Must initialize immediately:

```js
const x; // ❌ Error
```

### Important: Objects with `const`

`const` prevents reassignment — **not mutation**.

```js
const user = { name: "John" };
user.name = "Mike"; // ✅ Allowed
user = {}; // ❌ Not allowed
```

---

# 🔎 Scope Comparison

| Feature                   | var         | let     | const   |
| ------------------------- | ----------- | ------- | ------- |
| Scope                     | Function    | Block   | Block   |
| Reassignment              | ✅ Yes       | ✅ Yes   | ❌ No    |
| Redeclaration             | ✅ Yes       | ❌ No    | ❌ No    |
| Hoisted                   | ✅ Yes       | ✅ Yes   | ✅ Yes   |
| Access before declaration | `undefined` | ❌ Error | ❌ Error |

---

# 📦 Block Scope vs Function Scope

### Block Scope (`let`, `const`)

```js
{
  let a = 1;
  const b = 2;
}
console.log(a); // ❌ Error
```

### Function Scope (`var`)

```js
{
  var c = 3;
}
console.log(c); // ✅ 3
```

---

# 🚀 Best Practice (Modern JavaScript)

* Use `const` by default.
* Use `let` if you need to reassign.
* Avoid `var` in modern code.

Example:

```js
const API_URL = "https://api.example.com";
let counter = 0;
```

---

# 🧠 Simple Rule to Remember

* `var` → Old way (avoid)
* `let` → Changeable value
* `const` → Fixed reference

---

## JavaScript Data Types

In **JavaScript**, data types define what kind of value a variable can hold.

JavaScript has **7 primitive types** and **1 non-primitive type (Object)**.

---

# 🔹 1. String

Represents **text**.

```js
let name = "John";
let message = 'Hello';
let greeting = `Hi ${name}`; // Template literal
```

* Can use `" "`, `' '`, or backticks `` ` ``
* Immutable (cannot change individual characters)

Example:

```js
let str = "Hello";
str[0] = "Y";   // ❌ Won’t change
console.log(str); // "Hello"
```

---

# 🔹 2. Number

Represents **numeric values** (both integers and decimals).

```js
let age = 25;
let price = 99.99;
let negative = -10;
```

JavaScript has only **one number type** (no separate int/float).

Special numeric values:

```js
Infinity
-Infinity
NaN  // Not a Number
```

Example:

```js
console.log(10 / 0);   // Infinity
console.log("abc" / 2); // NaN
```

---

# 🔹 3. Boolean

Represents **true or false**.

```js
let isLoggedIn = true;
let hasPermission = false;
```

Commonly used in conditions:

```js
if (isLoggedIn) {
  console.log("Welcome!");
}
```

---

# 🔹 4. Undefined

A variable declared but **not assigned a value**.

```js
let x;
console.log(x); // undefined
```

It means:
👉 "Value not assigned yet"

---

# 🔹 5. Null

Represents an **intentional empty value**.

```js
let selectedUser = null;
```

It means:
👉 "No value on purpose"

⚠️ Important quirk:

```js
typeof null; // "object" (this is a historical bug)
```

---

# 🔹 6. Symbol (ES6)

Used to create **unique identifiers**.

```js
let id1 = Symbol("id");
let id2 = Symbol("id");

console.log(id1 === id2); // false
```

Even with same description, Symbols are always unique.

Commonly used in advanced object property handling.

---

# 🔹 7. Object (Non-Primitive)

Objects store **collections of data**.

```js
let user = {
  name: "John",
  age: 30
};
```

Arrays and functions are also objects:

```js
let arr = [1, 2, 3];     // Array (object)
function greet() {}      // Function (object)
```

Objects are **reference types**, not copied by value.

Example:

```js
let a = { x: 1 };
let b = a;
b.x = 2;

console.log(a.x); // 2 (same reference)
```

---

# 📊 Primitive vs Non-Primitive

| Feature   | Primitive                                        | Object                  |
| --------- | ------------------------------------------------ | ----------------------- |
| Stored by | Value                                            | Reference               |
| Mutable   | ❌ No                                             | ✅ Yes                   |
| Examples  | String, Number, Boolean, Undefined, Null, Symbol | Object, Array, Function |

---

# 🔍 `typeof` Operator

Used to check data type:

```js
typeof "Hello";     // "string"
typeof 10;          // "number"
typeof true;        // "boolean"
typeof undefined;   // "undefined"
typeof null;        // "object" (bug)
typeof {};          // "object"
typeof Symbol();    // "symbol"
```

---

# 🧠 Quick Summary

### ✅ Primitive Types (7)

* String
* Number
* Boolean
* Undefined
* Null
* Symbol
* (BigInt – newer numeric type)

### ✅ Non-Primitive

* Object

---

## JavaScript Operators

In **JavaScript**, operators are symbols that perform operations on values (operands).

Example:

```js
let sum = 5 + 3;
```

Here `+` is the operator.

---

# 1️⃣ Arithmetic Operators

Used for mathematical calculations.

| Operator | Meaning             | Example      |
| -------- | ------------------- | ------------ |
| `+`      | Addition            | `5 + 2` → 7  |
| `-`      | Subtraction         | `5 - 2` → 3  |
| `*`      | Multiplication      | `5 * 2` → 10 |
| `/`      | Division            | `10 / 2` → 5 |
| `%`      | Modulus (remainder) | `10 % 3` → 1 |
| `**`     | Exponent            | `2 ** 3` → 8 |

Example:

```js
let a = 10;
let b = 3;

console.log(a % b);  // 1
console.log(a ** 2); // 100
```

---

# 2️⃣ Assignment Operators

Used to assign values.

| Operator | Example  | Same As     |
| -------- | -------- | ----------- |
| `=`      | `x = 5`  |             |
| `+=`     | `x += 2` | `x = x + 2` |
| `-=`     | `x -= 2` | `x = x - 2` |
| `*=`     | `x *= 2` | `x = x * 2` |
| `/=`     | `x /= 2` | `x = x / 2` |

Example:

```js
let x = 10;
x += 5;  // 15
```

---

# 3️⃣ Comparison Operators

Used to compare values (result is Boolean).

| Operator | Meaning          |
| -------- | ---------------- |
| `==`     | Equal (loose)    |
| `===`    | Strict equal     |
| `!=`     | Not equal        |
| `!==`    | Strict not equal |
| `>`      | Greater than     |
| `<`      | Less than        |
| `>=`     | Greater or equal |
| `<=`     | Less or equal    |

### 🔎 `==` vs `===`

```js
console.log(5 == "5");   // true (type conversion)
console.log(5 === "5");  // false (strict check)
```

✅ Best practice: Use `===`

---

# 4️⃣ Logical Operators

Used for combining conditions.

| Operator | Meaning |   |    |
| -------- | ------- | - | -- |
| `&&`     | AND     |   |    |
| `        |         | ` | OR |
| `!`      | NOT     |   |    |

Example:

```js
let age = 20;

if (age > 18 && age < 60) {
  console.log("Working age");
}
```

Short-circuit example:

```js
console.log(true || false);  // true
console.log(false && true);  // false
```

---

# 5️⃣ Increment / Decrement

| Operator | Meaning       |
| -------- | ------------- |
| `++`     | Increase by 1 |
| `--`     | Decrease by 1 |

```js
let x = 5;
x++; // 6
x--; // 5
```

### Prefix vs Postfix

```js
let a = 5;
console.log(a++); // 5 (then becomes 6)
console.log(++a); // 7
```

---

# 6️⃣ String Operator

`+` is also used for string concatenation.

```js
let first = "Hello";
let second = "World";

console.log(first + " " + second);
```

---

# 7️⃣ Ternary Operator (Conditional)

Short form of `if...else`.

```js
let age = 18;
let status = age >= 18 ? "Adult" : "Minor";
```

Syntax:

```js
condition ? valueIfTrue : valueIfFalse;
```

---

# 8️⃣ Type Operators

| Operator     | Purpose            |
| ------------ | ------------------ |
| `typeof`     | Returns type       |
| `instanceof` | Checks object type |

Example:

```js
typeof "Hello"; // "string"

let arr = [];
console.log(arr instanceof Array); // true
```

---

# 9️⃣ Nullish Coalescing (`??`)

Returns right side only if left side is `null` or `undefined`.

```js
let name = null;
console.log(name ?? "Guest"); // "Guest"
```

---

# 🔟 Optional Chaining (`?.`)

Safely access nested properties.

```js
let user = {};
console.log(user.address?.city); // undefined (no error)
```

---

# 🧠 Operator Precedence

Some operators run before others:

```js
console.log(2 + 3 * 4); // 14 (multiplication first)
```

Use parentheses to control order:

```js
console.log((2 + 3) * 4); // 20
```

---

# 🚀 Quick Summary

### Main Operator Categories:

* Arithmetic
* Assignment
* Comparison
* Logical
* Increment/Decrement
* Ternary
* Type operators
* Nullish & Optional chaining

---

## Conditionals in JavaScript

In **JavaScript**, conditionals allow your program to make decisions based on conditions.

They control the flow of execution.

---

# 1️⃣ `if` Statement

Executes code **only if** the condition is true.

```js
let age = 20;

if (age >= 18) {
  console.log("You are an adult");
}
```

If the condition is `true`, the block runs.
If `false`, it is skipped.

---

# 2️⃣ `if...else`

Runs one block if true, another if false.

```js
let age = 16;

if (age >= 18) {
  console.log("Adult");
} else {
  console.log("Minor");
}
```

---

# 3️⃣ `if...else if...else`

Used for multiple conditions.

```js
let score = 85;

if (score >= 90) {
  console.log("Grade A");
} else if (score >= 75) {
  console.log("Grade B");
} else if (score >= 50) {
  console.log("Grade C");
} else {
  console.log("Fail");
}
```

The first true condition runs, and the rest are skipped.

---

# 4️⃣ `switch` Statement

Used when checking a single variable against multiple values.

```js
let day = 2;

switch (day) {
  case 1:
    console.log("Monday");
    break;
  case 2:
    console.log("Tuesday");
    break;
  case 3:
    console.log("Wednesday");
    break;
  default:
    console.log("Invalid day");
}
```

### 🔎 Important:

* `break` stops execution.
* Without `break`, it will continue to next case (fall-through).

Example without break:

```js
let x = 1;

switch (x) {
  case 1:
    console.log("One");
  case 2:
    console.log("Two");
}
```

Output:

```
One
Two
```

---

# 5️⃣ Ternary Operator (Short if-else)

Shorter version of `if...else`.

```js
let age = 18;

let result = age >= 18 ? "Adult" : "Minor";
console.log(result);
```

Syntax:

```js
condition ? valueIfTrue : valueIfFalse;
```

---

# 6️⃣ Truthy and Falsy Values

JavaScript automatically converts values to Boolean in conditions.

### ❌ Falsy values:

* `false`
* `0`
* `""` (empty string)
* `null`
* `undefined`
* `NaN`

Everything else is **truthy**.

Example:

```js
let name = "";

if (name) {
  console.log("Has name");
} else {
  console.log("No name");
}
```

Output:

```
No name
```

---

# 7️⃣ Logical Operators in Conditions

### AND (`&&`)

Both conditions must be true.

```js
if (age > 18 && age < 60) {
  console.log("Working age");
}
```

### OR (`||`)

At least one condition must be true.

```js
if (role === "admin" || role === "manager") {
  console.log("Access granted");
}
```

### NOT (`!`)

Reverses Boolean value.

```js
if (!isLoggedIn) {
  console.log("Please log in");
}
```

---

# 🧠 Best Practices

* Prefer `===` instead of `==`
* Use `switch` when comparing one variable to many values
* Keep conditions simple and readable
* Avoid deeply nested `if` statements when possible

---

# 🚀 Quick Summary

| Statement      | Use Case                     |
| -------------- | ---------------------------- |
| `if`           | Single condition             |
| `if...else`    | Two possibilities            |
| `if...else if` | Multiple conditions          |
| `switch`       | Many fixed values            |
| `? :`          | Short conditional expression |

---

## Loops in JavaScript

In **JavaScript**, loops are used to execute a block of code repeatedly until a condition is met.

---

# 1️⃣ `for` Loop

Used when you know **how many times** to run the loop.

### Syntax:

```js
for (initialization; condition; increment) {
  // code
}
```

### Example:

```js id="f1a2b3"
for (let i = 0; i < 5; i++) {
  console.log(i);
}
```

Output:

```
0
1
2
3
4
```

---

# 2️⃣ `while` Loop

Used when you **don’t know** how many times it will run (depends on condition).

### Syntax:

```js
while (condition) {
  // code
}
```

### Example:

```js id="g4h5i6"
let i = 0;

while (i < 5) {
  console.log(i);
  i++;
}
```

---

# 3️⃣ `do...while` Loop

Runs **at least once**, even if condition is false.

### Syntax:

```js
do {
  // code
} while (condition);
```

### Example:

```js id="j7k8l9"
let i = 0;

do {
  console.log(i);
  i++;
} while (i < 5);
```

---

# 4️⃣ `for...of` Loop (ES6)

Used to loop over **iterable values** like arrays and strings.

### Example with array:

```js id="m1n2o3"
let numbers = [10, 20, 30];

for (let num of numbers) {
  console.log(num);
}
```

### Example with string:

```js id="p4q5r6"
let text = "Hi";

for (let char of text) {
  console.log(char);
}
```

---

# 5️⃣ `for...in` Loop

Used to loop over **object properties (keys)**.

```js id="s7t8u9"
let user = {
  name: "John",
  age: 25
};

for (let key in user) {
  console.log(key, user[key]);
}
```

⚠️ Mostly used for objects, not arrays.

---

# 🔁 Loop Control Statements

## `break`

Stops the loop completely.

```js id="v1w2x3"
for (let i = 0; i < 10; i++) {
  if (i === 5) break;
  console.log(i);
}
```

---

## `continue`

Skips current iteration.

```js id="y4z5a6"
for (let i = 0; i < 5; i++) {
  if (i === 2) continue;
  console.log(i);
}
```

Output:

```
0
1
3
4
```

---

# 🔄 Nested Loops

Loop inside another loop.

```js id="b7c8d9"
for (let i = 1; i <= 3; i++) {
  for (let j = 1; j <= 2; j++) {
    console.log(i, j);
  }
}
```

---

# ⚠️ Infinite Loop (Be Careful)

If condition never becomes false:

```js
while (true) {
  console.log("Infinite!");
}
```

Always ensure the loop condition eventually becomes false.

---

# 🧠 When to Use What?

| Loop         | Best Used When                |
| ------------ | ----------------------------- |
| `for`        | You know number of iterations |
| `while`      | Condition-based looping       |
| `do...while` | Must run at least once        |
| `for...of`   | Iterating arrays/strings      |
| `for...in`   | Iterating object keys         |

---

# 🚀 Quick Example Comparison

```js id="e1f2g3"
let arr = [1, 2, 3];

// Traditional
for (let i = 0; i < arr.length; i++) {
  console.log(arr[i]);
}

// Modern
for (let value of arr) {
  console.log(value);
}
```

---

## Functions in JavaScript

In **JavaScript**, a **function** is a reusable block of code designed to perform a specific task.

Think of it as a machine:
👉 Input → Process → Output

---

# 1️⃣ Function Declaration

### Syntax:

```js
function functionName(parameters) {
  // code
  return value;
}
```

### Example:

```js
function greet(name) {
  return "Hello " + name;
}

console.log(greet("John")); // Hello John
```

✔️ Can be called before it's defined (because of hoisting).

---

# 2️⃣ Function Expression

Function stored inside a variable.

```js
const greet = function(name) {
  return "Hello " + name;
};
```

❌ Cannot be used before declaration.

---

# 3️⃣ Arrow Functions (ES6)

Shorter syntax.

```js
const greet = (name) => {
  return "Hello " + name;
};
```

### Shorter version (implicit return):

```js
const greet = name => "Hello " + name;
```

### Multiple parameters:

```js
const add = (a, b) => a + b;
```

---

# 4️⃣ Parameters vs Arguments

```js
function add(a, b) {   // a, b = parameters
  return a + b;
}

add(5, 3);  // 5, 3 = arguments
```

---

# 5️⃣ Default Parameters

```js
function greet(name = "Guest") {
  return "Hello " + name;
}

greet(); // Hello Guest
```

---

# 6️⃣ Return Statement

Stops function execution and sends value back.

```js
function square(num) {
  return num * num;
}

let result = square(4); // 16
```

Without `return`, function returns `undefined`.

---

# 7️⃣ Function Scope

Variables inside a function are not accessible outside.

```js
function test() {
  let x = 10;
}

console.log(x); // ❌ Error
```

Functions create their own scope.

---

# 8️⃣ Anonymous Functions

Functions without a name.

```js
setTimeout(function() {
  console.log("Hello");
}, 1000);
```

---

# 9️⃣ Immediately Invoked Function Expression (IIFE)

Runs immediately after being defined.

```js
(function() {
  console.log("I run immediately");
})();
```

---

# 🔟 Callback Functions

A function passed as an argument to another function.

```js
function greet(name, callback) {
  console.log("Hi " + name);
  callback();
}

function sayBye() {
  console.log("Goodbye!");
}

greet("John", sayBye);
```

Very common in asynchronous programming.

---

# 1️⃣1️⃣ Higher-Order Functions

A function that:

* Takes another function as argument OR
* Returns a function

Example:

```js
function multiplier(factor) {
  return function(number) {
    return number * factor;
  };
}

const double = multiplier(2);
console.log(double(5)); // 10
```

---

# 1️⃣2️⃣ Rest Parameters

Allows multiple arguments as array.

```js
function sum(...numbers) {
  return numbers.reduce((total, num) => total + num, 0);
}

sum(1, 2, 3, 4); // 10
```

---

# 1️⃣3️⃣ Function Hoisting

Only **function declarations** are hoisted:

```js
sayHello(); // Works

function sayHello() {
  console.log("Hello");
}
```

Function expressions and arrow functions are not hoisted the same way.

---

# 🧠 Function Types Summary

| Type                 | Hoisted? | Short Syntax? |
| -------------------- | -------- | ------------- |
| Function Declaration | ✅ Yes    | ❌ No          |
| Function Expression  | ❌ No     | ❌ No          |
| Arrow Function       | ❌ No     | ✅ Yes         |

---

# 🚀 Why Functions Are Powerful

* Reusable code
* Better organization
* Avoid repetition
* Enable abstraction
* Foundation for async programming

---

## Scope in JavaScript

In **JavaScript**, **scope** determines where variables are accessible in your code.

👉 In simple terms:
**Scope = Where you can use a variable.**

---

# 1️⃣ Global Scope

A variable declared outside any function or block.

```js
let name = "John";

function greet() {
  console.log(name);
}

greet(); // John
```

✔️ Accessible everywhere in the file.

⚠️ Avoid too many global variables — they can cause conflicts.

---

# 2️⃣ Function Scope

Variables declared inside a function are only accessible inside that function.

```js
function test() {
  let age = 25;
  console.log(age); // 25
}

console.log(age); // ❌ Error
```

Each function creates its own scope.

---

# 3️⃣ Block Scope (ES6)

Variables declared with `let` and `const` inside `{}` are block-scoped.

```js
if (true) {
  let x = 10;
  const y = 20;
}

console.log(x); // ❌ Error
console.log(y); // ❌ Error
```

### Important:

`var` does NOT follow block scope.

```js
if (true) {
  var z = 30;
}

console.log(z); // ✅ 30
```

---

# 4️⃣ Lexical Scope (Scope Chain)

JavaScript uses **lexical scoping**, meaning scope is determined by where variables are written in the code.

Inner functions can access outer function variables.

```js
function outer() {
  let message = "Hello";

  function inner() {
    console.log(message);
  }

  inner();
}

outer(); // Hello
```

The inner function looks up the scope chain to find `message`.

---

# 5️⃣ Scope Chain

If a variable is not found in the current scope, JavaScript looks in:

1. Local scope
2. Outer function scope
3. Global scope

If not found → ❌ ReferenceError

Example:

```js
let a = 10;

function test() {
  let b = 20;
  console.log(a + b);
}

test(); // 30
```

---

# 6️⃣ Shadowing

When a variable in inner scope has the same name as outer scope.

```js
let count = 5;

function test() {
  let count = 10;
  console.log(count);
}

test();        // 10
console.log(count); // 5
```

The inner variable “shadows” the outer one.

---

# 7️⃣ Temporal Dead Zone (TDZ)

Applies to `let` and `const`.

Variable exists but cannot be accessed before declaration.

```js
console.log(a); // ❌ Error
let a = 5;
```

This period before declaration is called the TDZ.

---

# 🔎 Scope Summary Table

| Type     | Created By              | Accessible Where       |
| -------- | ----------------------- | ---------------------- |
| Global   | Outside functions       | Everywhere             |
| Function | Inside function         | Inside function only   |
| Block    | `{}` with `let`/`const` | Inside block only      |
| Lexical  | Nested functions        | Inner can access outer |

---

# 🧠 Why Scope Is Important

* Prevents variable conflicts
* Controls data access
* Essential for closures
* Improves code security & organization

---

# 🚀 Quick Example Combining Everything

```js
let globalVar = "Global";

function outer() {
  let outerVar = "Outer";

  function inner() {
    let innerVar = "Inner";
    console.log(globalVar);
    console.log(outerVar);
    console.log(innerVar);
  }

  inner();
}

outer();
```

---

## Numbers in JavaScript

In **JavaScript**, the `Number` type represents **both integers and floating-point (decimal) values**.

Unlike many languages, JavaScript has **only one number type** (except for `BigInt`, introduced later).

---

# 1️⃣ Creating Numbers

```js
let age = 25;        // Integer
let price = 99.99;   // Decimal
let negative = -10;  // Negative number
```

You can also create numbers using the `Number` constructor:

```js
let num = Number("123"); // 123
```

---

# 2️⃣ Special Numeric Values

JavaScript includes some special number values:

```js
Infinity
-Infinity
NaN  // Not a Number
```

### Examples:

```js
console.log(10 / 0);     // Infinity
console.log(-10 / 0);    // -Infinity
console.log("abc" / 2);  // NaN
```

---

# 3️⃣ NaN (Not a Number)

`NaN` represents an invalid number result.

```js
let result = 0 / 0;  // NaN
```

To check for NaN:

```js
Number.isNaN(result); // true
```

⚠️ Important:

```js
NaN === NaN; // false
```

Use `Number.isNaN()` instead.

---

# 4️⃣ Floating-Point Precision Problem

JavaScript uses **IEEE 754** double-precision floating-point format.

This can cause precision issues:

```js
console.log(0.1 + 0.2); // 0.30000000000000004
```

### Solution:

```js
console.log((0.1 + 0.2).toFixed(2)); // "0.30"
```

Or:

```js
Math.round((0.1 + 0.2) * 100) / 100;
```

---

# 5️⃣ Number Methods

### `toFixed()`

Rounds to fixed decimal places (returns string).

```js
let num = 5.678;
num.toFixed(2); // "5.68"
```

### `toString()`

```js
let num = 100;
num.toString(); // "100"
```

---

# 6️⃣ Math Object

JavaScript provides the built-in `Math` object for mathematical operations.

### Common Methods:

```js
Math.round(4.6);  // 5
Math.floor(4.9);  // 4
Math.ceil(4.1);   // 5
Math.random();    // Random number between 0 and 1
Math.max(1, 5, 3); // 5
Math.min(1, 5, 3); // 1
Math.pow(2, 3);    // 8
Math.sqrt(16);     // 4
```

### Random number between 1–10:

```js
Math.floor(Math.random() * 10) + 1;
```

---

# 7️⃣ Number Conversion

### Convert string to number:

```js
Number("123");      // 123
parseInt("123px");  // 123
parseFloat("3.14"); // 3.14
```

⚠️ Difference:

```js
Number("123abc");   // NaN
parseInt("123abc"); // 123
```

---

# 8️⃣ BigInt (Large Numbers)

For very large integers beyond safe limit:

```js
let big = 123456789012345678901234567890n;
```

Or:

```js
BigInt("12345678901234567890");
```

Normal numbers are safe up to:

```js
Number.MAX_SAFE_INTEGER
```

---

# 9️⃣ Checking Numbers

```js
Number.isInteger(10);     // true
Number.isFinite(100);     // true
Number.isFinite(Infinity); // false
```

---

# 🔟 Arithmetic with Numbers

```js
let a = 10;
let b = 3;

a + b;  // 13
a - b;  // 7
a * b;  // 30
a / b;  // 3.333...
a % b;  // 1
a ** b; // 1000
```

---

# 🧠 Important Concepts Summary

| Concept            | Explanation             |
| ------------------ | ----------------------- |
| Single number type | No separate int/float   |
| IEEE 754           | Causes precision issues |
| NaN                | Invalid numeric result  |
| Infinity           | Division by zero        |
| BigInt             | For very large integers |
| MAX_SAFE_INTEGER   | Largest safe integer    |

---

# 🚀 Common Interview Tricky Examples

```js
typeof NaN;        // "number"
0.1 + 0.2 === 0.3; // false
9999999999999999;  // Precision loss
```

---









