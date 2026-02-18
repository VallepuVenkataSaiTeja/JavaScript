# JavaScript Data Types

Every value in JavaScript has a **type**. The type determines what kind of data it is and what operations you can perform on it.

---

# What is a Data Type?

A data type is a **classification of values** that tells JavaScript how to treat the data.

### Why does it matter?

```javascript
"5" + 2;   // "52"  (string concatenation)
5 + 2;     // 7     (numeric addition)
```

The **same operator** (`+`) produces completely different results depending on the **type** of the values involved.

---

## JavaScript is Dynamically Typed

In many languages (like Java or C), you must declare the type of a variable upfront. JavaScript does **not** require this.

```javascript
let x = 10;      // x holds a number
x = "hello";     // now x holds a string — no error
```

Types are checked at **runtime**, not at compile time. This gives you flexibility — but also more responsibility.

### Key Insight

> **Variables don't have types — values do.**

The variable `x` doesn't "become" a string. It simply holds a string value now.

---

# Primitive vs Non-Primitive (Overview)

JavaScript types fall into two categories:

| Category | Stored By | Mutable? | Examples |
|----------|-----------|----------|----------|
| Primitive | **Value** | ❌ No | string, number, boolean, undefined, null, symbol, bigint |
| Non-Primitive | **Reference** | ✅ Yes | object, array, function |

- **Primitive** = a single, simple, immutable value. When you assign it to another variable, the value is **copied**.
- **Non-Primitive** = complex data stored by reference. When you assign it, both variables **point to the same data** in memory.

We will deep dive into non-primitives (objects, arrays, functions) later. For now, just understand that these two categories exist and behave differently.

---

# The 7 Primitive Types

```
string  •  number  •  boolean  •  undefined  •  null  •  symbol  •  bigint
```

Out of these seven:

- **string**, **number**, and **boolean** → you will use these **every single day**
- **undefined** and **null** → you will encounter these constantly
- **symbol** and **bigint** → rare in beginner code — awareness is enough

Don't feel overwhelmed. Focus on string, number, and boolean first.

---

# string

A string represents **text data** — a sequence of characters.

---

## Three Ways to Create Strings

```javascript
let single = 'Hello';       // single quotes
let double = "Hello";       // double quotes
let backtick = `Hello`;     // backticks (template literal)
```

All three create valid strings. Single and double quotes work the same way — pick one style and be consistent.

---

## Template Literals (Backticks)

Backticks unlock two powerful features:

### 1. String Interpolation with `${}`

Instead of messy concatenation:

```javascript
let name = "Alex";
let age = 22;

// Old way — concatenation
console.log("My name is " + name + " and I am " + age + " years old.");

// Modern way — template literal
console.log(`My name is ${name} and I am ${age} years old.`);
```

You can put **any expression** inside `${}`:

```javascript
console.log(`2 + 3 = ${2 + 3}`);  // "2 + 3 = 5"
```

### 2. Multi-line Strings

```javascript
let message = `This is line one
and this is line two`;
```

With single or double quotes, you would need `\n` to achieve the same thing.

---

## Escape Sequences

Special characters that start with a backslash (`\`):

| Sequence | Meaning |
|----------|---------|
| `\n` | New line |
| `\t` | Tab |
| `\\` | Backslash |
| `\"` | Double quote inside a double-quoted string |
| `\'` | Single quote inside a single-quoted string |

### Example:

```javascript
console.log("She said \"Hello\"");   // She said "Hello"
console.log("Line1\nLine2");         // prints on two lines
```

---

## String Length

The `.length` property returns the number of characters:

```javascript
let greeting = "Hello";
console.log(greeting.length);  // 5
```

Technically, `.length` counts **UTF-16 code units** — but for everyday strings, think of it as the character count.

---

## Strings Are Immutable

You **cannot** change individual characters of a string:

```javascript
let str = "hello";
str[0] = "H";         // ❌ Does nothing — no error, but no change
console.log(str);      // "hello" — unchanged
```

To get `"Hello"`, you would create a **new** string:

```javascript
str = "H" + str.slice(1);   // "Hello" — a brand new string
```

We will cover string methods like `.slice()` in detail later. For now, just remember: **strings cannot be modified in place.**

---

# number

JavaScript has **one** numeric type — there is no separate integer or float type like in other languages.

```javascript
let integer = 42;
let decimal = 3.14;
let negative = -7;
```

All of these are just `number`.

---

## Special Numeric Values

### NaN (Not a Number)

`NaN` is the result of a **failed numeric operation**:

```javascript
let result = "abc" * 2;
console.log(result);        // NaN
```

### Important NaN facts:

```javascript
typeof NaN;       // "number"  — yes, NaN is technically a number
NaN === NaN;      // false     — NaN is NOT equal to itself!
```

To check for NaN, use:

```javascript
isNaN("abc" * 2);           // true
Number.isNaN("abc" * 2);    // true (more reliable)
```

### NaN Propagation

Once NaN enters a calculation, it **spreads** to every result:

```javascript
NaN + 5;      // NaN
NaN * 10;     // NaN
NaN - 1;      // NaN
```

---

### Infinity and -Infinity

```javascript
console.log(1 / 0);    // Infinity
console.log(-1 / 0);   // -Infinity
```

These are the result of dividing by zero or exceeding the numeric range.

---

## Floating-Point Quirk

```javascript
console.log(0.1 + 0.2);           // 0.30000000000000004
console.log(0.1 + 0.2 === 0.3);   // false
```

This is **not** a JavaScript bug — it happens in every language that uses IEEE 754 floating-point math. Just be aware of it when comparing decimal numbers.

---

# boolean

A boolean has only **two possible values**: `true` or `false`.

```javascript
let isLoggedIn = true;
let hasPermission = false;
```

---

## Where Booleans Are Used

Booleans power **all decision-making** in code:

```javascript
if (isLoggedIn) {
    console.log("Welcome back!");
}
```

---

## Comparison Operators Return Booleans

```javascript
5 > 3;       // true
10 === 10;   // true
"a" === "b"; // false
```

Every time you write a condition, you are working with booleans.

---

# undefined

`undefined` means: **"a value has not been assigned yet."**

It is set **by the system**, not by you.

---

## When Does undefined Appear?

### 1. Uninitialized variables

```javascript
let x;
console.log(x);  // undefined
```

### 2. Missing function parameters

```javascript
function greet(name) {
    console.log(name);
}

greet();  // undefined
```

### 3. Functions that don't return a value

```javascript
function doSomething() {
    // no return statement
}

let result = doSomething();
console.log(result);  // undefined
```

### 4. Missing object properties

```javascript
let user = { name: "Alex" };
console.log(user.age);  // undefined
```

---

## Simple Rule

> `undefined` = the **system** says "nothing here yet"

---

# null

`null` means: **"intentionally empty."**

It is set **by the developer** to explicitly say "no value."

```javascript
let user = null;   // "no user right now"
```

---

## null vs undefined

This is one of the most common points of confusion:

| | undefined | null |
|---|-----------|------|
| Set by | System | Developer |
| Meaning | "Not assigned yet" | "Intentionally empty" |
| Type | `typeof undefined` → `"undefined"` | `typeof null` → `"object"` (bug) |

### Simple Rule:

> **undefined → system says "nothing here yet"**
> **null → developer says "intentionally empty"**

### Example:

```javascript
let score;            // undefined — not assigned yet
let winner = null;    // null — no winner has been decided
```

---

# symbol (Light Coverage)

A symbol is a **unique and immutable** identifier.

```javascript
let id1 = Symbol("id");
let id2 = Symbol("id");

console.log(id1 === id2);  // false — every symbol is unique!
```

Even though both have the description `"id"`, they are **not the same**.

---

## Why Symbols Exist

Symbols are mainly used as **unique object property keys** to avoid accidental name collisions:

```javascript
let secret = Symbol("secret");
let obj = {};
obj[secret] = "hidden value";
```

No other code can accidentally access or overwrite `obj[secret]` because every symbol is unique.

---

## For Now

Symbols are **rare in beginner code**. Just know they exist and that they are unique. We will revisit well-known symbols (like `Symbol.iterator`) in a later phase.

---

# bigint (Light Coverage)

`bigint` is used for **very large integers** that exceed the safe range of regular numbers.

```javascript
console.log(Number.MAX_SAFE_INTEGER);  // 9007199254740991
```

Beyond this limit, regular numbers lose precision:

```javascript
console.log(9007199254740991 + 2);  // 9007199254740992 — wrong!
```

---

## Creating BigInts

```javascript
let big1 = 123n;              // add 'n' at the end
let big2 = BigInt(123);       // or use BigInt()
```

---

## Rules

- ❌ Cannot mix BigInt and Number directly:
  ```javascript
  1n + 2;  // ❌ TypeError
  ```
- ❌ No decimals allowed:
  ```javascript
  1.5n;    // ❌ SyntaxError
  ```

---

## For Now

BigInt is **rare in everyday code**. Just know it exists for handling extremely large numbers.

---

# typeof Operator

`typeof` returns a **string** that tells you the type of a value.

```javascript
typeof "hello";        // "string"
typeof 42;             // "number"
typeof true;           // "boolean"
typeof undefined;      // "undefined"
typeof Symbol();       // "symbol"
typeof 123n;           // "bigint"
typeof {};             // "object"
typeof function(){};   // "function"
```

---

## The typeof null Quirk

```javascript
typeof null;  // "object"  — ⚠️ This is WRONG
```

This is a **historical bug** from 1995 (the first version of JavaScript). `null` is NOT an object — it is a primitive.

This bug **cannot be fixed** because doing so would break millions of existing websites.

### How to properly check for null:

```javascript
let value = null;
value === null;  // true — use strict equality instead
```

---

## typeof in Practice

Use `typeof` to check types before performing operations:

```javascript
function double(value) {
    if (typeof value === "number") {
        return value * 2;
    }
    return "Not a number!";
}

double(5);       // 10
double("hello"); // "Not a number!"
```

---

# Immutability of Primitives

All primitive values are **immutable** — they cannot be changed after creation.

### Example:

```javascript
let x = "hello";
x = "world";
```

It looks like we "changed" the string. But here is what actually happened:

1. The string `"hello"` was created in memory.
2. The variable `x` pointed to `"hello"`.
3. A **new** string `"world"` was created.
4. `x` now points to `"world"`.
5. The string `"hello"` was **never modified** — it was **replaced**.

### Mental Model:

> You don't modify a primitive — you **replace** it.

This applies to all primitives: strings, numbers, booleans, etc.

---

# Copy by Value

When you assign a primitive to another variable, the **actual value is copied**.

```javascript
let a = 5;
let b = a;   // b gets its own copy of the value 5

b = 100;

console.log(a);  // 5   — unchanged
console.log(b);  // 100
```

Each variable holds its own **independent copy**. Changing one does **not** affect the other.

---

## Visual Model

```
Before:     a → [ 5 ]      b → [ 5 ]
After:      a → [ 5 ]      b → [ 100 ]
```

They are completely separate.

---

## Why This Matters

Objects (non-primitives) work **differently** — they copy by **reference**, meaning two variables can point to the **same** data. This is a major source of bugs in JavaScript.

We will cover this in detail when we learn about objects. For now, just remember:

> **Primitives = copy by value (safe, independent copies)**

---

# Quick Reference Table

| Type | Example | typeof Result |
|------|---------|---------------|
| string | `"hello"` | `"string"` |
| number | `42`, `3.14`, `NaN` | `"number"` |
| boolean | `true`, `false` | `"boolean"` |
| undefined | `undefined` | `"undefined"` |
| null | `null` | `"object"` ⚠️ |
| symbol | `Symbol("id")` | `"symbol"` |
| bigint | `123n` | `"bigint"` |

---

# Key Takeaways

✅ JavaScript has **7 primitive types**: string, number, boolean, undefined, null, symbol, bigint

✅ **Variables don't have types — values do** (dynamic typing)

✅ Primitives are **immutable** — you replace them, not modify them

✅ Primitives are copied **by value** — each variable gets an independent copy

✅ Use `typeof` to check the type of a value

✅ `typeof null === "object"` is a **historical bug** — always check null with `=== null`

✅ `NaN !== NaN` — use `Number.isNaN()` to check for NaN

✅ Focus on **string, number, and boolean** first — you will use them daily

---

# Interview Tip ⭐

👉 **What is the difference between null and undefined?**

- `undefined` → assigned by the **system** when no value has been given
- `null` → assigned by the **developer** to intentionally indicate "no value"

👉 **Why does `typeof null` return `"object"`?**

- It is a bug from the original JavaScript implementation in 1995. It was never fixed because changing it would break existing code.

👉 **What are the primitive types in JavaScript?**

- string, number, boolean, undefined, null, symbol, bigint — **seven** in total
