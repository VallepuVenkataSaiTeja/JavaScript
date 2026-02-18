# 1.7 Control Flow (JavaScript)

Control flow determines **the order in which your code executes**. Instead of executing every line sequentially, programs use decisions, loops, and control statements to manage behavior.

Think of control flow like traffic rules:

- **Green → Execute**
- **Red → Stop**
- **Yellow → Decide**

Without control flow, programs would not be able to respond dynamically to data or user input.

---

# ✅ 1. Conditional Statements

Conditional statements allow programs to **execute code only when certain conditions are met**.

---

## 🔹 if Statement

Runs a block of code if the condition evaluates to **true** (truthy).

```javascript
let age = 20;

if (age >= 18) {
  console.log("You are an adult");
}
```

### How it works:
1. Condition is evaluated.
2. If truthy → block executes.
3. If falsy → block is skipped.

---

## 🔹 if...else

Provides an alternate path when the condition is false.

```javascript
let age = 16;

if (age >= 18) {
  console.log("Adult");
} else {
  console.log("Minor");
}
```

👉 Only **one block** will execute.

---

## 🔹 else if (Multiple Conditions)

Used when there are multiple possible outcomes.

```javascript
let marks = 82;

if (marks >= 90) {
  console.log("Grade A");
}
else if (marks >= 75) {
  console.log("Grade B");
}
else if (marks >= 50) {
  console.log("Grade C");
}
else {
  console.log("Fail");
}
```

### ✅ Best Practice:
Order conditions from **most specific → least specific**.

Bad:
```javascript
if (marks >= 50)
```

Good:
```javascript
if (marks >= 90)
else if (marks >= 75)
else if (marks >= 50)
```

---

# ✅ switch Statement

Best when comparing **one variable against many fixed values**.

Cleaner than writing many `else if` blocks.

---

## Syntax

```javascript
switch(expression) {

  case value1:
    // code
    break;

  case value2:
    // code
    break;

  default:
    // fallback
}
```

---

## Example

```javascript
let day = 3;

switch(day) {

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

---

## ⚠️ Forgetting `break` Causes Fall-Through

```javascript
let day = 1;

switch(day) {
  case 1:
    console.log("Monday");

  case 2:
    console.log("Tuesday");
}
```

### Output:
```
Monday
Tuesday
```

Execution continues until a `break` is encountered.

---

## ✅ Intentional Fall-Through (Advanced)

Sometimes multiple cases should execute the same code.

```javascript
let role = "editor";

switch(role) {

  case "admin":
  case "editor":
    console.log("Permission granted");
    break;
}
```

---

# ✅ 2. Loops

Loops repeat code automatically until a condition is no longer true.

Without loops:

```javascript
console.log(1);
console.log(2);
console.log(3);
```

With loops → cleaner, scalable, maintainable.

---

## 🔹 for Loop (Most Important)

Best when the number of iterations is known.

### Syntax

```javascript
for (initialization; condition; update) {

}
```

### Example

```javascript
for (let i = 1; i <= 5; i++) {
  console.log(i);
}
```

### Execution Order:
1. Initialization runs once.
2. Condition is checked.
3. Code executes.
4. Update runs.
5. Repeat until condition becomes false.

---

## ⚠️ Infinite Loop Danger

```javascript
for (let i = 1; i <= 5; ) {
  console.log(i);
}
```

No update step → loop never ends.

Always ensure the condition eventually becomes false.

---

## 🔹 while Loop

Executes **while a condition remains true**.

Best when the number of iterations is unknown.

```javascript
let count = 1;

while (count <= 3) {
  console.log(count);
  count++;
}
```

### Common Uses:
- Waiting for user input  
- Game loops  
- Retry mechanisms  
- Streaming data  

---

## 🔹 do...while Loop

Guarantees the code runs **at least once**, even if the condition is false.

```javascript
let number = 10;

do {
  console.log("Runs once!");
} while (number < 5);
```

---

## 🔹 for...of (Modern & Preferred)

Iterates over **values** of iterable objects.

Works with:
- Arrays
- Strings
- Maps
- Sets

```javascript
const fruits = ["apple", "banana", "mango"];

for (const fruit of fruits) {
  console.log(fruit);
}
```

### Why developers prefer it:
✅ Cleaner  
✅ Less error-prone  
✅ No index management  

---

## ❌ Does NOT Work on Plain Objects

```javascript
const user = {name: "Alex"};

for (const val of user) {
}
```

Objects are not iterable.

---

## 🔹 for...in

Iterates over **keys (properties)** of an object.

```javascript
const user = {
  name: "Alex",
  age: 25
};

for (const key in user) {
  console.log(key, user[key]);
}
```

### Output:
```
name Alex
age 25
```

---

## ⚠️ Important Warning

`for...in` also iterates over properties from the prototype chain.

Safer version:

```javascript
for (const key in user) {
  if (user.hasOwnProperty(key)) {
    console.log(key);
  }
}
```

---

# ⭐ Loop Selection Guide

| Loop | Best Use Case |
|--------|---------------|
| for | Known iteration count |
| while | Unknown iteration count |
| for...of | Arrays / iterable values |
| for...in | Object keys |

---

# ✅ 3. Control Statements

These statements immediately alter loop execution.

---

## 🔹 break

Terminates the loop completely.

```javascript
for (let i = 1; i <= 10; i++) {

  if (i === 5) break;

  console.log(i);
}
```

### Output:
```
1
2
3
4
```

---

## 🔹 continue

Skips the current iteration and proceeds to the next.

```javascript
for (let i = 1; i <= 5; i++) {

  if (i === 3) continue;

  console.log(i);
}
```

### Output:
```
1
2
4
5
```

---

## 🔹 Labels (Rare but Powerful)

Used to control nested loops.

```javascript
outer:

for (let i = 1; i <= 3; i++) {

  for (let j = 1; j <= 3; j++) {

    if (j === 2) {
      break outer;
    }

    console.log(i, j);
  }
}
```

Stops **both loops instantly**.

⚠ Use sparingly — labels can reduce readability.

---

# ✅ Choosing the Right Structure

### Use `if`
When evaluating ranges or complex conditions.

### Use `switch`
When comparing one value against many fixed constants.

### Use `for`
When iteration count is known.

### Use `while`
When iteration count is unknown.

### Use `for...of`
For arrays and iterable data (modern best practice).

---

# ⭐ Common Beginner Mistakes

## ❌ Using assignment instead of comparison
```javascript
if (x = 5)
```
This assigns instead of compares.

✅ Correct:
```javascript
if (x === 5)
```

---

## ❌ Infinite loops
Forgetting the update condition.

---

## ❌ Missing `break` in switch
Leads to unintended fall-through.

---

## ❌ Using `for...in` on arrays
Order is not guaranteed.

Prefer:
```
for...of ✅
```

---

# 🔥 Interview-Level Insight

Control flow is about **predictability**.

Good developers write code where execution order is obvious.

Always ask yourself:

> “What runs next?”

If the answer is not immediately clear — simplify the code.

---

# ✅ One-Line Summary

**Control flow enables programs to make decisions, repeat operations, and manage execution order using conditionals, loops, and control statements.**
