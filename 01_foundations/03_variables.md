# JavaScript Variables

Variables are used to **store data values** in a program so they can be reused and manipulated later.

Think of a variable as a **container** that holds information.

---

# What is a Variable?

A variable is a named storage location in memory.

### Example:
```javascript
let age = 25;
```

Here:
- `age` → variable name  
- `25` → stored value  

---

# Ways to Declare Variables

JavaScript provides **three keywords**:

- `var` → Old way (NOT recommended)
- `let` → Modern way
- `const` → Modern and safest option

---

# 1. var (Avoid Using)

`var` was used before ES6 but is now discouraged due to unpredictable behavior.

## Characteristics:
- ✅ Can be **redeclared**
- ✅ Can be **reassigned**
- ❌ Function scoped (not block scoped)
- ⚠️ Hoisted and initialized with `undefined`

### Example:
```javascript
var x = 10;
var x = 20; // Allowed
x = 30;     // Allowed
```

## Why Avoid `var`?
Because it can create bugs due to:
- Scope confusion
- Accidental redeclaration
- Hoisting behavior

👉 **Best practice: Do NOT use `var` in modern JavaScript.**

---

# 2. let (Recommended for Changing Values)

`let` is the modern replacement for `var`.

## Characteristics:
- ❌ Cannot be redeclared
- ✅ Can be reassigned
- ✅ Block scoped
- ⚠️ Hoisted but placed in the **Temporal Dead Zone (TDZ)**

### Example:
```javascript
let score = 50;
score = 80; // ✅ Allowed

let score = 100; // ❌ Error
```

👉 Use `let` when the value **needs to change**.

Examples:
- counters  
- loops  
- user input  

---

# 3. const (MOST Recommended)

`const` is used for values that should **never be reassigned**.

## Characteristics:
- ❌ Cannot be redeclared
- ❌ Cannot be reassigned
- ✅ Block scoped
- ⚠️ Hoisted but in TDZ

### Example:
```javascript
const PI = 3.14159;
PI = 3.14; // ❌ Error
```

---

## Important Note About const (Very Common Interview Question)

`const` prevents **reassignment**, NOT mutation.

### ✅ Allowed:
```javascript
const user = { name: "John" };
user.name = "Mike"; // Allowed
```

### ❌ Not Allowed:
```javascript
user = {}; // Error
```

👉 The reference cannot change, but object contents can.

---

# Hoisting Explained Simply

Hoisting means JavaScript **moves declarations to the top** of their scope before execution.

---

## var Hoisting
```javascript
console.log(a); // undefined
var a = 5;
```

Behind the scenes:
```javascript
var a;
console.log(a);
a = 5;
```

---

## let & const Hoisting (Temporal Dead Zone)

```javascript
console.log(b); // ❌ ReferenceError
let b = 10;
```

The time between entering the scope and declaring the variable is called:

# 👉 Temporal Dead Zone (TDZ)

Accessing the variable here causes an error.

---

# Variable Naming Rules

## ✅ Allowed:
- Letters → `name`
- Dollar sign → `$price`
- Underscore → `_id`
- Can include numbers (not at start) → `user1`

---

## ❌ Not Allowed:
- Cannot start with numbers  
  ```javascript
  let 1user; // Error
  ```

- Cannot use reserved keywords  
  ```javascript
  let for = 10; // Error
  ```

- No special characters except `_` and `$`

---

## Case Sensitivity
JavaScript is case-sensitive.

```javascript
let user = "John";
let User = "Mike";
```

These are **two different variables.**

---

# Naming Best Practices

## camelCase → Recommended
Used for most variables.

```javascript
let firstName;
let totalPrice;
```

---

## UPPER_CASE → Constants
Used for fixed values.

```javascript
const MAX_USERS = 100;
const API_KEY = "abc123";
```

---

# Understanding Scope

Scope determines **where a variable can be accessed.**

---

# 1. Global Scope

A variable declared outside any function or block.

```javascript
let appName = "MyApp";
```

Accessible everywhere.

⚠️ Avoid too many global variables — they increase bug risk.

---

# 2. Function Scope

Created when using `var`.

```javascript
function test() {
    var message = "Hello";
}

console.log(message); // ❌ Error
```

Accessible **only inside the function.**

---

# 3. Block Scope (IMPORTANT)

Applies to `let` and `const`.

A block is anything inside `{ }`.

```javascript
{
    let x = 10;
}

console.log(x); // ❌ Error
```

---

## ⚠️ Correction from Your Notes:
👉 `var` is **NOT block scoped.**

```javascript
{
    var a = 5;
}

console.log(a); // ✅ Works
```

This is one reason `var` is unsafe.

---

# Shadowing

Shadowing happens when a variable inside a block has the **same name** as one outside.

The inner variable overrides the outer one **within its scope.**

### Example:
```javascript
let value = 10;

{
    let value = 20;
    console.log(value); // 20
}

console.log(value); // 10
```

---

# Quick Comparison Table

| Feature | var | let | const |
|--------|------|------|--------|
| Redeclare | ✅ | ❌ | ❌ |
| Reassign | ✅ | ✅ | ❌ |
| Scope | Function | Block | Block |
| Hoisted | Yes (undefined) | Yes (TDZ) | Yes (TDZ) |
| Recommended | ❌ | ✅ | ✅✅ |

---

# Best Practices (VERY Important)

## ✅ Prefer `const` by default  
Use `let` only when necessary.

👉 Modern developers follow this rule:

> **"Start with const. Change to let only if needed."**

---

## ❌ Avoid var completely
There is almost no modern use case for it.

---

## Keep Scope Small
Declare variables as close as possible to where they are used.

This improves:
- readability  
- maintainability  
- debugging  

---

# Interview Tip ⭐

👉 **Difference between let and const?**

- `let` → reassignment allowed  
- `const` → reassignment NOT allowed  

Both are:
- block scoped  
- hoisted with TDZ  

