# 📘 1.6 Operators in JavaScript (Complete Guide)

Operators are special symbols that **perform operations on values and variables.**  
Mastering them is critical because operators are used in nearly **every line of real-world JavaScript code.**

👉 Think of operators as the **verbs of programming** — they make things happen.

---

# ✅ What is an Operator?

An operator takes one or more values (called operands) and produces a result.

```javascript
5 + 3
```

Here:

- `5` and `3` → operands  
- `+` → operator  

Result → `8`

---

# 🔥 1. Arithmetic Operators

Used for mathematical calculations.

| Operator | Meaning | Example | Result |
|--------|------------|---------|---------|
| `+` | Addition / Concatenation | `5 + 2` | `7` |
| `-` | Subtraction | `5 - 2` | `3` |
| `*` | Multiplication | `5 * 2` | `10` |
| `/` | Division | `10 / 2` | `5` |
| `%` | Remainder (Modulo) | `10 % 3` | `1` |
| `**` | Exponentiation | `2 ** 3` | `8` |

---

## ⭐ Special Arithmetic Operators

### ✅ Increment (`++`) and Decrement (`--`)

Increase or decrease a value by **1**.

### Prefix vs Postfix (VERY IMPORTANT)

#### Prefix → increments first, then returns value
```javascript
let x = 5;
++x;   // 6
```

#### Postfix → returns value first, then increments
```javascript
let x = 5;
x++;   // returns 5, but x becomes 6
```

👉 This difference matters inside expressions.

Example:

```javascript
let a = 5;
let b = a++;  // b = 5, a = 6
```

---

### ✅ Unary Plus (`+`) — Convert to Number

```javascript
+"5"   // 5
+true  // 1
+""    // 0
```

Fast alternative to `Number()`.

---

### ✅ Unary Minus (`-`) — Negates Value

```javascript
let x = 5;
-x;   // -5
```

Also converts strings to numbers:

```javascript
-"10"   // -10
```

---

# 🔥 2. Assignment Operators

Used to assign values to variables.

---

## Basic Assignment
```javascript
let x = 10;
```

---

## Compound Assignment (Cleaner & Faster)

| Operator | Equivalent |
|------------|--------------|
| `+=` | `x = x + y` |
| `-=` | `x = x - y` |
| `*=` | `x = x * y` |
| `/=` | `x = x / y` |
| `%=` | `x = x % y` |
| `**=` | `x = x ** y` |

Example:

```javascript
let x = 10;
x += 5;   // 15
```

👉 Cleaner than writing `x = x + 5`.

---

# 🔥 3. Comparison Operators

Used to compare values — always return **true or false**.

| Operator | Meaning |
|--------|------------|
| `>` | Greater than |
| `<` | Less than |
| `>=` | Greater than or equal |
| `<=` | Less than or equal |

---

## Numbers Example
```javascript
5 > 3    // true
5 < 3    // false
```

---

## Strings Are Compared Alphabetically

```javascript
"apple" < "banana"   // true
```

Why?

Because JavaScript compares **Unicode values** (dictionary order).

---

## Equality Operators

### Loose Equality
```javascript
"5" == 5   // true
```

👉 Performs type coercion.

---

### Strict Equality (ALWAYS PREFER)
```javascript
"5" === 5   // false
```

✔ No coercion  
✔ Safer  
✔ Predictable  

⭐ **Golden Rule:** Use `===` by default.

---

# 🔥 4. Logical Operators

Used to combine or invert conditions.

---

## ✅ AND (`&&`)

Returns:

👉 **First falsy value**, OR  
👉 **Last value if all are truthy**

```javascript
true && "Hello"   // "Hello"
false && "Hi"     // false
```

### Short-Circuiting
If the first condition fails, JavaScript **stops immediately.**

```javascript
false && expensiveFunction(); // function never runs
```

🔥 Great for performance.

---

## ✅ OR (`||`)

Returns:

👉 **First truthy value**, OR  
👉 Last value if all are falsy.

```javascript
0 || "default"   // "default"
"Hi" || "Hello"  // "Hi"
```

Often used for default values.

---

## ✅ NOT (`!`)

Flips boolean value.

```javascript
!true   // false
!0      // true
```

---

### Double NOT (`!!`) — Convert to Boolean

```javascript
!!"hello"   // true
!!0         // false
```

Fast boolean conversion trick.

---

# 🔥 5. Nullish Coalescing (`??`)

Returns the right side **ONLY if left is `null` or `undefined`.**

```javascript
let user = null;
user ?? "Guest";   // "Guest"
```

---

## ⭐ Difference from `||`

```javascript
0 || "default"   // "default"
0 ?? "default"   // 0
```

Why?

Because `||` treats **0 as falsy**, but `??` does NOT.

---

### ✅ When to Use `??`

Use it when values like these are valid:

- `0`
- `""`
- `false`

👉 Very important in modern JavaScript.

---

# 🔥 6. Optional Chaining (`?.`)

Prevents crashes when accessing nested properties.

Without it:

```javascript
user.address.city   // ❌ Error if address is undefined
```

With optional chaining:

```javascript
user?.address?.city   // undefined (safe)
```

---

## Works with Methods

```javascript
user?.login?.();
```

Won't execute if method doesn't exist.

---

## Works with Brackets

```javascript
user?.["name"];
```

---

⭐ Extremely useful when working with APIs.

---

# 🔥 7. Ternary Operator

Shorthand for simple `if...else`.

### Syntax:
```javascript
condition ? valueIfTrue : valueIfFalse;
```

Example:

```javascript
let age = 18;
let status = age >= 18 ? "Adult" : "Minor";
```

---

⚠ Avoid nesting — it becomes unreadable.

Bad:
```javascript
a ? b : c ? d : e;
```

---

# 🔥 8. Other Important Operators

---

## ✅ Comma Operator (`,`)

Evaluates left → right, returns the **last value.**

```javascript
let x = (1, 2, 3);
console.log(x);   // 3
```

Rarely used — mostly in advanced code.

---

## ✅ `in` Operator

Checks if a property exists in an object.

```javascript
"name" in user   // true or false
```

Also checks the prototype chain.

---

## ✅ `instanceof`

Checks whether an object belongs to a constructor.

```javascript
arr instanceof Array   // true
```

Useful for type checking.

---

## ✅ `delete`

Removes object properties.

```javascript
delete user.age;
```

⚠ Does NOT delete variables.

---

## ✅ `void`

Evaluates an expression and always returns `undefined`.

```javascript
void 0   // undefined
```

Rare — mostly seen in advanced patterns.

---

# 🔥 Logical Assignment Operators (Modern JS)

Combine logic + assignment.

---

## `&&=`
Assign only if the variable is truthy.

```javascript
user &&= "Guest";
```

---

## `||=`
Assign if the variable is falsy.

```javascript
username ||= "Anonymous";
```

---

## `??=`
Assign only if value is `null` or `undefined`.

```javascript
settings ??= {};
```

⭐ Very useful for defaults.

---

# 🔥 Spread vs Rest (`...`)

Same syntax — different purpose.

---

## ✅ Spread — Expands Values

```javascript
let arr = [1, 2, 3];
let newArr = [...arr, 4];
```

👉 Copies arrays safely.

Also works with objects:

```javascript
let user = {name: "Sam"};
let updated = {...user, age: 20};
```

---

## ✅ Rest — Collects Remaining Values

### In Destructuring:
```javascript
let [a, ...rest] = [1,2,3,4];
rest; // [2,3,4]
```

### In Functions:
```javascript
function sum(...numbers) {
  return numbers.reduce((a,b) => a+b);
}
```

---

# 🚨 Operator Precedence (VERY IMPORTANT)

JavaScript follows priority rules.

Example:

```javascript
5 + 2 * 3   // 11
```

Multiplication runs first.

👉 Use parentheses when unsure:

```javascript
(5 + 2) * 3   // 21
```

Never rely on memory — prioritize readability.

---

# 🎯 Pro Developer Rules

✅ Prefer `===` over `==`  
✅ Use `??` instead of `||` for safer defaults  
✅ Avoid overusing ternary  
✅ Use optional chaining to prevent crashes  
✅ Be explicit when mixing types  

---

# ⭐ Ultimate Summary

👉 Operators are the foundation of JavaScript logic.

If you master:

- Arithmetic  
- Logical  
- Comparison  
- Assignment  
- Modern operators (`??`, `?.`, `...`)  

You eliminate a huge percentage of beginner and intermediate bugs.

---

## 🧠 One-Line Master Insight:

> **Great JavaScript developers don’t just use operators — they understand exactly what JavaScript will do before it runs.**
