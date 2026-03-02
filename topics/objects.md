# 🟢 1. Fundamentals of Objects

* What is an object?
* Object literal syntax
* Key–value pairs
* Accessing properties

  * Dot notation
  * Bracket notation
* Adding, updating, deleting properties
* Nested objects
* Checking property existence (`in`, `hasOwnProperty()`)

---

# 🟢 2. Object Methods

* Adding functions inside objects
* `this` keyword
* Method shorthand syntax (ES6)
* Arrow functions vs regular functions in objects (important difference with `this`)

---

# 🟢 3. Object Utilities (Built-in Methods)

Study these thoroughly:

* `Object.keys()`
* `Object.values()`
* `Object.entries()`
* `Object.fromEntries()`
* `Object.assign()`
* `Object.freeze()`
* `Object.seal()`
* `Object.hasOwn()`

Also understand:

* Shallow vs deep copy
* Spread operator `{ ...obj }`

---

# 🟢 4. Object Destructuring (ES6)

* Basic destructuring
* Renaming variables
* Default values
* Nested destructuring
* Destructuring in function parameters

---

# 🟢 5. Object References & Memory

* Objects are reference types
* Reference vs primitive
* Comparing objects
* Cloning objects properly

---

# 🟢 6. Constructor Functions

* Creating objects using constructor functions
* `new` keyword
* How `new` works internally
* `instanceof`

---

# 🟢 7. Prototypes & Prototype Chain (VERY IMPORTANT)

This is a core JS concept.

* What is a prototype?
* `__proto__`
* `Object.getPrototypeOf()`
* Prototype chain lookup
* Adding methods to prototype
* Difference between instance methods and prototype methods

Understand how this connects to JavaScript’s OOP model.

---

# 🟢 8. Classes (ES6 Syntax)

* `class` syntax
* Constructor
* Methods
* Static methods
* Getters and setters
* Inheritance (`extends`)
* `super` keyword

Understand that classes are syntactic sugar over prototypes.

---

# 🟢 9. Advanced Object Concepts

* Property descriptors

  * `Object.getOwnPropertyDescriptor()`
  * `Object.defineProperty()`
* Writable, enumerable, configurable
* Object immutability patterns
* Object iteration patterns
* Symbols as object keys
* Computed property names

---

# 🟢 10. JSON & Objects

* `JSON.stringify()`
* `JSON.parse()`
* Differences between JS objects and JSON
* Common pitfalls

---

# 🟢 11. Object-Oriented Programming in JS

* Encapsulation
* Abstraction
* Inheritance
* Polymorphism
* Factory functions
* Module pattern
* Private fields (`#field`) in classes

---

# 🟢 12. Objects in Real-World Scenarios

* Objects in APIs
* Handling nested API responses
* Data modeling
* Merging configurations
* Deep cloning strategies

---

# 🟢 13. Interview-Level Topics

* Deep vs shallow copy
* Implement your own `Object.assign`
* Implement inheritance manually
* Create a polyfill for object methods
* Questions on prototype chain
* `this` behavior in tricky scenarios

---

# 🟢 14. Bonus (High-Level Mastery)

* Reflect API
* Proxy objects
* Meta-programming
* Immutable libraries (concept understanding)
* Performance considerations with large objects

---

# 📌 Suggested Learning Order

1. Basics →
2. Methods →
3. Destructuring →
4. Constructor Functions →
5. Prototypes →
6. Classes →
7. Advanced descriptors →
8. OOP patterns →
9. Proxy & Reflect

---

# 🟢 1. Fundamentals of Objects in JavaScript

This is the foundation of JavaScript. If you master this properly, everything else (prototypes, classes, OOP, frameworks) becomes easier.

---

# 1️⃣ What is an Object in JavaScript?

An **object** is a collection of **key–value pairs**.

Think of it like:

* A real-world entity (user, product, car)
* A dictionary (word → meaning)
* A container of related data

Example:

```js
const user = {
  name: "Aman",
  age: 22,
  isLoggedIn: true
};
```

Here:

* `name`, `age`, `isLoggedIn` → **keys (properties)**
* `"Aman"`, `22`, `true` → **values**

---

# 2️⃣ Object Literal Syntax

The most common way to create objects is using **object literal** syntax `{}`.

```js
const car = {
  brand: "Toyota",
  model: "Corolla",
  year: 2023
};
```

### Rules:

* Keys are strings (even if you don’t write them as strings).
* Keys must be unique.
* Values can be **any data type**:

  * String
  * Number
  * Boolean
  * Array
  * Function
  * Another object
  * `null`
  * `undefined`

Example with mixed types:

```js
const product = {
  name: "Laptop",
  price: 50000,
  inStock: true,
  tags: ["electronics", "computers"],
  details: {
    brand: "Dell",
    warranty: "2 years"
  }
};
```

---

# 3️⃣ How JavaScript Stores Objects (Important Concept)

Objects are stored in **heap memory**.

When you do:

```js
const obj1 = { a: 10 };
const obj2 = obj1;
```

Both `obj1` and `obj2` point to the **same memory location**.

So:

```js
obj2.a = 20;
console.log(obj1.a); // 20
```

⚠️ This is called **reference behavior**.

Objects are **reference types**, not primitive types.

---

# 4️⃣ Accessing Object Properties

There are **two ways**:

---

## ✅ 1. Dot Notation (Most Common)

```js
console.log(user.name);
```

Rules:

* Works when key is a valid identifier.
* Cleaner and preferred.

---

## ✅ 2. Bracket Notation

```js
console.log(user["name"]);
```

Used when:

* Key contains spaces
* Key is dynamic
* Key starts with a number

Example:

```js
const person = {
  "full name": "Rahul Sharma",
  "1stRank": true
};

console.log(person["full name"]);
console.log(person["1stRank"]);
```

---

## 🔥 Dynamic Property Access (Very Important)

```js
const key = "age";
console.log(user[key]);
```

You **cannot** do:

```js
user.key ❌
```

Because that literally looks for `"key"`.

---

# 5️⃣ Adding Properties

Objects are **mutable** (can change after creation).

```js
const student = {
  name: "Riya"
};

student.age = 20;
student["grade"] = "A";
```

Now object becomes:

```js
{
  name: "Riya",
  age: 20,
  grade: "A"
}
```

---

# 6️⃣ Updating Properties

```js
student.age = 21;
```

If property exists → it updates.
If not → it creates.

---

# 7️⃣ Deleting Properties

```js
delete student.grade;
```

After this, `grade` is removed.

---

# 8️⃣ Nested Objects

Objects can contain other objects.

```js
const user = {
  name: "Aman",
  address: {
    city: "Delhi",
    pincode: 110001
  }
};
```

Access nested value:

```js
console.log(user.address.city);
```

If unsure about existence:

```js
console.log(user.address?.city);
```

This is called **optional chaining**.

---

# 9️⃣ Checking if a Property Exists

### ✅ Using `in` operator

```js
console.log("name" in user); // true
```

---

### ✅ Using `hasOwnProperty()`

```js
console.log(user.hasOwnProperty("name"));
```

Difference:

* `in` checks prototype chain
* `hasOwnProperty()` checks only own properties

(Prototype will be covered later in roadmap.)

---

# 🔟 Iterating Over Objects

### Using `for...in`

```js
for (let key in user) {
  console.log(key, user[key]);
}
```

Important:

* Iterates over enumerable properties
* Includes inherited properties

---

# 1️⃣1️⃣ Property Names Rules

Valid:

```js
{
  name: "Aman",
  age1: 22,
  $value: 100
}
```

Invalid (without quotes):

```js
{
  full name: "Aman" ❌
}
```

Correct version:

```js
{
  "full name": "Aman"
}
```

---

# 1️⃣2️⃣ Computed Property Names (ES6)

You can dynamically create keys.

```js
const keyName = "score";

const result = {
  [keyName]: 95
};

console.log(result.score); // 95
```

Very important for dynamic data handling.

---

# 1️⃣3️⃣ Object vs Primitive (Critical Understanding)

| Primitive         | Object                |
| ----------------- | --------------------- |
| Stored by value   | Stored by reference   |
| Immutable         | Mutable               |
| Compared by value | Compared by reference |

Example:

```js
const a = { x: 1 };
const b = { x: 1 };

console.log(a === b); // false
```

Even though contents same, memory location different.

---

# 1️⃣4️⃣ Object.create()

Another way to create objects:

```js
const person = Object.create(null);
person.name = "Aman";
```

This creates object **without prototype**.

Normal object:

```js
const obj = {};
```

Is equivalent to:

```js
const obj = Object.create(Object.prototype);
```

---

# 1️⃣5️⃣ Object Constructor (Less Common Now)

```js
const obj = new Object();
obj.name = "Test";
```

Not recommended. Use literal `{}` instead.

---

# 1️⃣6️⃣ Empty Objects & Truthiness

```js
if ({}) {
  console.log("Runs");
}
```

Objects are always **truthy**.

Even empty object `{}` is truthy.

---

# 1️⃣7️⃣ Object Key Type Reality (Important Hidden Rule)

Even if you write:

```js
const obj = {
  1: "one"
};
```

Internally it becomes:

```js
{
  "1": "one"
}
```

Object keys are always:

* String
* Symbol

Never numbers internally.

---

# 1️⃣8️⃣ Common Beginner Mistakes

### ❌ Comparing objects directly

```js
{} === {} // false
```

---

### ❌ Forgetting bracket notation for dynamic keys

```js
obj.key ❌
obj[key] ✅
```

---

### ❌ Mutating original object unintentionally

```js
const a = { x: 1 };
const b = a;
b.x = 2; // changes a too
```

---

# 🎯 What You MUST Master from Fundamentals

If you truly understand:

* Reference behavior
* Dot vs bracket notation
* Nested object access
* Dynamic property names
* Mutation vs reassignment
* Object comparison behavior

You have solid object fundamentals.

---

# 🟢 2. Object Methods (In Depth)

This section is about **functions inside objects** and how they behave — especially the most misunderstood concept in JavaScript: **`this`**.

---

# 1️⃣ What is an Object Method?

When a function is stored inside an object, it’s called a **method**.

```js
const user = {
  name: "Aman",
  greet: function () {
    console.log("Hello!");
  }
};

user.greet(); // Hello!
```

Here:

* `greet` → method
* `user.greet()` → method invocation

A method is just a function attached to an object.

---

# 2️⃣ Method vs Normal Function

```js
function sayHi() {
  console.log("Hi");
}

const person = {
  sayHi: sayHi
};
```

Now:

```js
person.sayHi();
```

Same function, but behavior may differ when `this` is involved.

---

# 3️⃣ The `this` Keyword (VERY IMPORTANT)

Inside an object method, `this` refers to the **object that calls the method**.

Example:

```js
const user = {
  name: "Aman",
  greet: function () {
    console.log("Hi, I am " + this.name);
  }
};

user.greet(); 
// Hi, I am Aman
```

### Key Rule:

> `this` depends on **how the function is called**, not where it is written.

---

# 4️⃣ How `this` is Determined (Core Rule)

### ✅ Case 1: Method Call

```js
user.greet();
```

Here:

* `this` = `user`

---

### ❌ Case 2: Detached Function

```js
const greetFn = user.greet;
greetFn();
```

Now:

* `this` is `undefined` (in strict mode)
* or `window` (non-strict)

Because it’s no longer called as `user.greet()`.

This is a very common interview question.

---

# 5️⃣ Arrow Functions vs Regular Functions in Objects

⚠️ Extremely important difference.

---

## ❌ Arrow Function as Method (Common Mistake)

```js
const user = {
  name: "Aman",
  greet: () => {
    console.log("Hi " + this.name);
  }
};

user.greet();
```

Output:

```
Hi undefined
```

Why?

Because:

> Arrow functions do NOT have their own `this`.

They inherit `this` from the surrounding scope.

---

## ✅ Correct Way (Use Regular Function)

```js
const user = {
  name: "Aman",
  greet() {
    console.log("Hi " + this.name);
  }
};
```

This works correctly.

---

# 6️⃣ Method Shorthand (ES6)

Instead of:

```js
greet: function() {}
```

You can write:

```js
greet() {}
```

Example:

```js
const car = {
  brand: "Toyota",
  start() {
    console.log(this.brand + " started");
  }
};
```

Cleaner and modern syntax.

---

# 7️⃣ Methods Using Parameters

```js
const calculator = {
  add(a, b) {
    return a + b;
  }
};

console.log(calculator.add(5, 3)); // 8
```

Methods behave like normal functions but are attached to objects.

---

# 8️⃣ Methods Modifying Object Data

Methods often modify object properties.

```js
const counter = {
  count: 0,
  increment() {
    this.count++;
  }
};

counter.increment();
console.log(counter.count); // 1
```

This is common in state management.

---

# 9️⃣ Nested Object Methods

```js
const user = {
  name: "Aman",
  address: {
    city: "Delhi",
    getCity() {
      console.log(this.city);
    }
  }
};

user.address.getCity(); // Delhi
```

Here:

* `this` refers to `address`, not `user`.

Because `address` is the caller.

---

# 🔟 `this` Inside Callback (Tricky Area)

```js
const user = {
  name: "Aman",
  greet() {
    setTimeout(function () {
      console.log(this.name);
    }, 1000);
  }
};

user.greet();
```

Output:

```
undefined
```

Why?

Because inside `setTimeout`:

* Regular function → its own `this`
* Not called as object method

---

## ✅ Fix Using Arrow Function

```js
const user = {
  name: "Aman",
  greet() {
    setTimeout(() => {
      console.log(this.name);
    }, 1000);
  }
};
```

Now it works.

Because arrow function inherits `this` from `greet()`.

---

# 1️⃣1️⃣ `call()`, `apply()`, `bind()` (Controlling `this`)

These are function methods.

Example:

```js
function greet() {
  console.log("Hi " + this.name);
}

const user = { name: "Aman" };

greet.call(user);
```

Output:

```
Hi Aman
```

### Difference:

* `call()` → arguments individually
* `apply()` → arguments as array
* `bind()` → returns new function

Example:

```js
const boundFn = greet.bind(user);
boundFn();
```

---

# 1️⃣2️⃣ Object Methods and Memory Efficiency

Bad practice:

```js
function createUser(name) {
  return {
    name,
    greet() {
      console.log("Hi " + this.name);
    }
  };
}
```

Each object gets its own copy of `greet()`.

Better approach (advanced, coming later):
Use prototypes to share methods.

---

# 1️⃣3️⃣ Getters and Setters (Intro Level)

```js
const user = {
  firstName: "Aman",
  lastName: "Sharma",
  get fullName() {
    return this.firstName + " " + this.lastName;
  }
};

console.log(user.fullName);
```

Looks like property, behaves like method.

Setter example:

```js
set fullName(value) {
  const parts = value.split(" ");
  this.firstName = parts[0];
  this.lastName = parts[1];
}
```

---

# 1️⃣4️⃣ Method Chaining Pattern

```js
const calculator = {
  value: 0,
  add(num) {
    this.value += num;
    return this;
  },
  subtract(num) {
    this.value -= num;
    return this;
  }
};

calculator.add(5).subtract(2);
console.log(calculator.value); // 3
```

Returning `this` enables chaining.

---

# 🎯 What You MUST Master in Object Methods

If you truly understand:

* What makes a function a method
* How `this` works in:

  * Normal method
  * Detached function
  * Arrow function
  * Callback
* Method shorthand
* call/apply/bind basics
* Getter/setter fundamentals

Then your object method foundation is strong.

---


# 🟢 3. Object Utilities (Built-in Methods)

These are static methods on the global `Object` constructor that help you:

* Inspect objects
* Copy objects
* Merge objects
* Control mutability
* Transform objects

These are heavily used in:

* React
* Redux
* APIs
* Node.js
* Interview questions

We’ll go step-by-step and go deep.

---

# 1️⃣ `Object.keys()`

Returns an array of an object's **own enumerable property names (keys)**.

```js
const user = {
  name: "Aman",
  age: 22,
  isAdmin: false
};

console.log(Object.keys(user));
```

Output:

```js
["name", "age", "isAdmin"]
```

### Important Notes:

* Only returns **own properties**
* Does NOT include prototype properties
* Only returns **enumerable** properties
* Always returns **strings**

---

# 2️⃣ `Object.values()`

Returns an array of values.

```js
console.log(Object.values(user));
```

Output:

```js
["Aman", 22, false]
```

Used when:

* Extracting data
* Mapping over values
* Summing object values

---

# 3️⃣ `Object.entries()`

Returns key–value pairs as arrays.

```js
console.log(Object.entries(user));
```

Output:

```js
[
  ["name", "Aman"],
  ["age", 22],
  ["isAdmin", false]
]
```

### Very Powerful for Iteration

```js
for (let [key, value] of Object.entries(user)) {
  console.log(key, value);
}
```

This is cleaner than `for...in`.

---

# 4️⃣ `Object.fromEntries()`

The reverse of `Object.entries()`.

```js
const arr = [
  ["name", "Aman"],
  ["age", 22]
];

const obj = Object.fromEntries(arr);
console.log(obj);
```

Output:

```js
{ name: "Aman", age: 22 }
```

🔥 Extremely useful when transforming data.

Example:

```js
const updated = Object.fromEntries(
  Object.entries(user).map(([k, v]) => [k, String(v)])
);
```

Converts all values to strings.

---

# 5️⃣ `Object.assign()` (VERY IMPORTANT)

Used to copy or merge objects.

## Basic Copy

```js
const user = { name: "Aman", age: 22 };
const copy = Object.assign({}, user);

console.log(copy);
```

---

## Merge Multiple Objects

```js
const obj1 = { a: 1 };
const obj2 = { b: 2 };

const merged = Object.assign({}, obj1, obj2);
```

Output:

```js
{ a: 1, b: 2 }
```

---

## ⚠️ Overwriting Behavior

```js
const obj1 = { a: 1 };
const obj2 = { a: 5 };

const result = Object.assign({}, obj1, obj2);
```

Output:

```js
{ a: 5 }
```

Later objects overwrite earlier ones.

---

## ⚠️ IMPORTANT: Shallow Copy

```js
const user = {
  name: "Aman",
  address: { city: "Delhi" }
};

const copy = Object.assign({}, user);
copy.address.city = "Mumbai";

console.log(user.address.city); // Mumbai ❗
```

Because nested objects are copied by reference.

---

# 6️⃣ Spread Operator `{ ...obj }`

Modern alternative to `Object.assign()`.

```js
const copy = { ...user };
```

Merging:

```js
const merged = { ...obj1, ...obj2 };
```

Same shallow-copy behavior as `Object.assign()`.

Spread is cleaner and preferred in modern JS.

---

# 7️⃣ `Object.freeze()`

Makes object **immutable**.

```js
const user = { name: "Aman" };
Object.freeze(user);

user.name = "Rahul"; // ignored
```

* Cannot add
* Cannot delete
* Cannot modify

⚠️ But shallow only.

```js
const user = {
  name: "Aman",
  address: { city: "Delhi" }
};

Object.freeze(user);
user.address.city = "Mumbai"; // still works ❗
```

Because nested object not frozen.

---

# 8️⃣ `Object.seal()`

Less strict than freeze.

```js
const user = { name: "Aman" };
Object.seal(user);

user.name = "Rahul"; // allowed
user.age = 25; // ❌ not allowed
delete user.name; // ❌ not allowed
```

Seal:

* Cannot add
* Cannot delete
* Can modify existing

---

# 9️⃣ `Object.hasOwn()`

Modern replacement for `hasOwnProperty()`.

```js
Object.hasOwn(user, "name");
```

Better because:

* Safer
* Works even if object overrides `hasOwnProperty`

---

# 🔟 `Object.getOwnPropertyNames()`

Returns all property names (including non-enumerable).

```js
Object.getOwnPropertyNames(user);
```

Includes properties that `Object.keys()` ignores.

---

# 1️⃣1️⃣ `Object.getOwnPropertySymbols()`

Returns symbol properties only.

Objects can have Symbol keys:

```js
const id = Symbol("id");

const user = {
  name: "Aman",
  [id]: 123
};
```

`Object.keys()` won’t show symbol keys.

---

# 1️⃣2️⃣ `Object.create()`

Creates new object with specified prototype.

```js
const animal = {
  speak() {
    console.log("Sound");
  }
};

const dog = Object.create(animal);
dog.speak();
```

This is foundational for prototype inheritance.

---

# 1️⃣3️⃣ `Object.is()`

Better comparison than `===`.

```js
Object.is(NaN, NaN); // true
Object.is(+0, -0);   // false
```

Unlike:

```js
NaN === NaN // false
```

Rarely used but important conceptually.

---

# 🧠 ENUMERABLE vs NON-ENUMERABLE (Important Concept)

Some properties don’t show up in:

* `Object.keys()`
* `for...in`

Example:

```js
Object.defineProperty(obj, "hidden", {
  value: 42,
  enumerable: false
});
```

Now:

```js
Object.keys(obj); // won't include "hidden"
```

We’ll go deeper into this in Property Descriptors section later.

---

# 🔥 Shallow vs Deep Copy (Critical Interview Topic)

### Shallow Copy:

* Copies top-level
* Nested objects still referenced

Methods that do shallow copy:

* `Object.assign`
* Spread operator

---

### Deep Copy Options:

1. `structuredClone()` (modern)

```js
const deepCopy = structuredClone(user);
```

2. `JSON.parse(JSON.stringify(obj))` (limited)

---

# 🧠 Real-World Usage Example

Common React pattern:

```js
setUser(prev => ({
  ...prev,
  age: prev.age + 1
}));
```

Uses:

* Spread operator
* Immutable update
* Shallow copy logic

---

# 🎯 What You MUST Master Here

Absolutely understand:

* `Object.keys / values / entries`
* `Object.assign` vs spread
* Shallow copy behavior
* Freeze vs Seal
* FromEntries transformation pattern
* Enumerability basics

If you master this section, you are strong in practical JavaScript.

---


# 🟢 4. Object Destructuring (ES6)

Object destructuring lets you **extract properties from objects into variables** in a clean, readable way.

It is heavily used in:

* React
* API handling
* Function parameters
* Modern JS codebases
* Interviews

We’ll go step-by-step and cover beginner → advanced.

---

# 1️⃣ What is Object Destructuring?

Instead of doing:

```js
const user = {
  name: "Aman",
  age: 22
};

const name = user.name;
const age = user.age;
```

You can write:

```js
const { name, age } = user;
```

This extracts properties into variables.

---

# 2️⃣ Basic Syntax

```js
const { propertyName } = object;
```

Example:

```js
const product = {
  title: "Laptop",
  price: 50000,
  inStock: true
};

const { title, price } = product;

console.log(title); // Laptop
console.log(price); // 50000
```

⚠️ Important:

* Variable names must match property names.

---

# 3️⃣ Renaming Variables (Very Important)

What if you want a different variable name?

```js
const { title: productTitle } = product;

console.log(productTitle); // Laptop
```

Format:

```js
const { originalKey: newVariableName } = object;
```

This is extremely common in real projects.

---

# 4️⃣ Default Values

If property does not exist, you can provide default value.

```js
const user = {
  name: "Aman"
};

const { name, age = 18 } = user;

console.log(age); // 18
```

Default works only when:

* Property is `undefined`
* Or doesn't exist

---

# 5️⃣ Nested Object Destructuring

Very important.

```js
const user = {
  name: "Aman",
  address: {
    city: "Delhi",
    pincode: 110001
  }
};
```

Extract nested property:

```js
const { address: { city } } = user;

console.log(city); // Delhi
```

⚠️ Important:
This does NOT create `address` variable.
Only `city` is created.

If you want both:

```js
const { address, address: { city } } = user;
```

---

# 6️⃣ Renaming Nested Properties

```js
const { address: { city: userCity } } = user;

console.log(userCity);
```

This is common in API responses.

---

# 7️⃣ Default Value in Nested Destructuring

```js
const user = {};

const {
  address: {
    city = "Unknown"
  } = {}
} = user;

console.log(city); // Unknown
```

Without `= {}`, this would throw error.

This is an interview-level pattern.

---

# 8️⃣ Destructuring in Function Parameters (VERY IMPORTANT)

Instead of:

```js
function greet(user) {
  console.log(user.name);
}
```

You can do:

```js
function greet({ name }) {
  console.log(name);
}
```

Called like:

```js
greet({ name: "Aman" });
```

---

## With Default Values

```js
function greet({ name = "Guest" } = {}) {
  console.log(name);
}
```

This prevents errors if function called without argument.

---

# 9️⃣ Rest Operator in Object Destructuring

Collect remaining properties.

```js
const user = {
  name: "Aman",
  age: 22,
  country: "India"
};

const { name, ...rest } = user;

console.log(name); // Aman
console.log(rest); 
```

Output:

```js
{ age: 22, country: "India" }
```

Very common in:

* React props
* Removing properties
* Creating new objects without certain keys

---

# 🔟 Combining Destructuring + Spread

Example: Removing a property immutably

```js
const user = {
  name: "Aman",
  password: "12345",
  age: 22
};

const { password, ...safeUser } = user;

console.log(safeUser);
```

Now `safeUser` has no password.

This pattern is used in backend sanitization.

---

# 1️⃣1️⃣ Computed Property Destructuring

If key is dynamic:

```js
const key = "name";

const user = {
  name: "Aman",
  age: 22
};

const { [key]: value } = user;

console.log(value); // Aman
```

Advanced but powerful.

---

# 1️⃣2️⃣ Destructuring with Arrays Inside Objects

```js
const user = {
  name: "Aman",
  skills: ["JS", "React"]
};

const {
  skills: [firstSkill]
} = user;

console.log(firstSkill); // JS
```

You can mix object + array destructuring.

---

# 1️⃣3️⃣ Common Mistakes

### ❌ Forgetting parentheses when reassigning

This fails:

```js
{ name } = user;
```

Correct:

```js
({ name } = user);
```

Because `{}` is interpreted as block otherwise.

---

### ❌ Destructuring undefined nested object

```js
const { address: { city } } = user;
```

If `address` is undefined → error.

Fix:

```js
const { address: { city } = {} } = user;
```

---

### ❌ Confusing with JSON

Destructuring works on objects, not JSON strings.

---

# 1️⃣4️⃣ Real-World Usage Examples

## React Props

```js
function Profile({ name, age }) {
  return <h1>{name}</h1>;
}
```

Very common pattern.

---

## API Response

```js
const response = {
  data: {
    user: {
      name: "Aman"
    }
  }
};

const {
  data: {
    user: { name }
  }
} = response;
```

Deep destructuring is common in backend work.

---

# 1️⃣5️⃣ Shallow Nature of Destructuring

Important:

```js
const user = {
  name: "Aman",
  address: { city: "Delhi" }
};

const { address } = user;
address.city = "Mumbai";

console.log(user.address.city); // Mumbai ❗
```

Destructuring does NOT deep clone.
It just extracts references.

---

# 🎯 What You MUST Master

If you understand:

* Basic destructuring
* Renaming
* Default values
* Nested destructuring
* Function parameter destructuring
* Rest operator
* Error prevention patterns

You are strong in modern JS.

---


# 🟢 5. Object References & Memory (Deep Mental Model)

This topic explains:

* How objects are stored in memory
* Why objects behave differently from primitives
* Why copying objects can cause bugs
* Why `===` behaves strangely with objects
* Shallow vs deep behavior (real understanding)

Let’s go step-by-step.

---

# 1️⃣ Memory Basics in JavaScript

JavaScript uses two main memory areas:

### 🟦 Stack

* Stores primitive values
* Stores references (addresses) to objects

### 🟥 Heap

* Stores actual objects and arrays

---

# 2️⃣ Primitive vs Object Memory Behavior

## 🟢 Primitive (Stored by Value)

```js
let a = 10;
let b = a;

b = 20;
console.log(a); // 10
```

What happens:

```
Stack:
a → 10
b → 10 (copy)

Then:
b → 20
```

Each variable has its own copy.

---

## 🔵 Object (Stored by Reference)

```js
let obj1 = { name: "Aman" };
let obj2 = obj1;

obj2.name = "Rahul";
console.log(obj1.name); // Rahul ❗
```

What happens:

```
Stack:
obj1 → 0x001
obj2 → 0x001

Heap:
0x001 → { name: "Aman" }
```

Both variables point to the same object in heap.

When you modify one, you modify the shared object.

---

# 3️⃣ Object Comparison (Very Important)

```js
const a = { x: 1 };
const b = { x: 1 };

console.log(a === b); // false
```

Why?

Because:

```
a → 0x001
b → 0x002
```

Different memory locations.

Even if contents same → references differ.

---

## But This Works:

```js
const a = { x: 1 };
const b = a;

console.log(a === b); // true
```

Because both point to same memory address.

---

# 4️⃣ Reassignment vs Mutation

This is extremely important.

## 🟢 Mutation (Changes existing object)

```js
const user = { name: "Aman" };
user.name = "Rahul";
```

You modified the same object.

---

## 🔵 Reassignment (Changes reference)

```js
let user = { name: "Aman" };
user = { name: "Rahul" };
```

Now:

Old object still exists in memory until garbage collected.

You created a new object and changed reference.

---

# 5️⃣ Function Arguments & References

Objects passed to functions are passed by reference value.

Meaning:

* The reference is copied
* Not the object itself

Example:

```js
function update(user) {
  user.name = "Rahul";
}

const person = { name: "Aman" };
update(person);

console.log(person.name); // Rahul
```

Because:

* `user` parameter points to same object.

---

## But Reassigning Inside Function Does NOT Affect Outside

```js
function update(user) {
  user = { name: "Rahul" };
}

const person = { name: "Aman" };
update(person);

console.log(person.name); // Aman
```

Because:

* Only local reference changed
* Original reference unchanged

This is a very common interview trap.

---

# 6️⃣ Shallow Copy Explained Properly

Example:

```js
const user = {
  name: "Aman",
  address: { city: "Delhi" }
};

const copy = { ...user };
```

Memory structure:

```
copy → new object
copy.address → same reference as user.address
```

So:

```js
copy.address.city = "Mumbai";
console.log(user.address.city); // Mumbai ❗
```

Because nested object still shared.

---

# 7️⃣ Deep Copy Concept

Deep copy means:

* New object
* New nested objects
* No shared references

Modern way:

```js
const deepCopy = structuredClone(user);
```

Now:

```
deepCopy.address !== user.address
```

Modifying one won’t affect other.

---

# 8️⃣ Garbage Collection (Basic Understanding)

JavaScript automatically removes objects from memory when:

* No variable references them anymore.

Example:

```js
let obj = { name: "Aman" };
obj = null;
```

Now:

* No references point to old object
* It becomes eligible for garbage collection

You don't manually free memory in JS.

---

# 9️⃣ Constant Objects (Important Concept)

```js
const user = { name: "Aman" };
user.name = "Rahul"; // ✅ allowed
```

Why?

Because:

* `const` prevents reassignment
* Not mutation

This fails:

```js
user = {}; ❌
```

Because reference cannot change.

---

# 🔟 Object.freeze() and Memory

```js
const user = { name: "Aman" };
Object.freeze(user);
```

Now:

* Mutation blocked
* Reference still same
* Nested objects still mutable (unless frozen too)

---

# 1️⃣1️⃣ Circular References

Objects can reference themselves.

```js
const obj = {};
obj.self = obj;
```

Now:

```
obj → {
   self → same obj
}
```

Important because:

* `JSON.stringify()` fails here
* Deep cloning becomes tricky

---

# 1️⃣2️⃣ Why React Cares About References

React checks changes using shallow comparison.

Example:

```js
setUser(prev => ({
  ...prev,
  age: prev.age + 1
}));
```

Why not:

```js
user.age = 23; ❌
```

Because:

* React needs new reference to detect change.

Reference change = React re-renders.

This is why immutability matters.

---

# 1️⃣3️⃣ Visual Mental Model Summary

Think of objects like:

* Variables hold **addresses**
* Heap stores **actual objects**
* Copying object variable copies **address**
* Mutating changes **shared object**
* Reassigning creates **new object**

---

# 1️⃣4️⃣ Common Bugs Due to Reference Misunderstanding

### ❌ Accidentally modifying original data

```js
const sorted = arr.sort();
```

`sort()` mutates original array.

---

### ❌ Unexpected shared state

```js
const config = defaultConfig;
config.theme = "dark";
```

You just modified defaultConfig.

---

# 🎯 What You MUST Truly Understand

If you deeply understand:

* Stack vs Heap concept
* Reference vs Value
* Mutation vs Reassignment
* Function parameter behavior
* Shallow vs Deep copy
* Why object comparison fails

Then your JavaScript mental model is strong.

---


# 🟢 6. Constructor Functions (Deep Dive)

---

# 1️⃣ What is a Constructor Function?

A constructor function is a **normal function** used to create multiple similar objects.

Before ES6 classes, this was the primary OOP pattern.

Basic example:

```js id="v0u4fj"
function User(name, age) {
  this.name = name;
  this.age = age;
}

const user1 = new User("Aman", 22);
const user2 = new User("Rahul", 25);
```

Now:

```js id="nox4wr"
console.log(user1.name); // Aman
console.log(user2.name); // Rahul
```

---

# 2️⃣ Why Use Constructor Functions?

Instead of:

```js id="1yecpz"
const user1 = { name: "Aman", age: 22 };
const user2 = { name: "Rahul", age: 25 };
```

You create a blueprint:

```js id="h74v4j"
function User(name, age) {
  this.name = name;
  this.age = age;
}
```

Now you can create unlimited users.

Think of constructor as a factory blueprint.

---

# 3️⃣ Why Capital Letter?

By convention:

```js id="e8l4ah"
function User() {}
```

Constructors start with uppercase.

This signals:

> "This function must be called with `new`."

---

# 4️⃣ What Does `new` Actually Do? (CRITICAL)

When you write:

```js id="28zbl1"
const user1 = new User("Aman", 22);
```

JavaScript internally does:

### Step 1:

Creates empty object

```js id="l5v0h7"
const obj = {};
```

### Step 2:

Sets prototype

```js id="wwf93q"
obj.__proto__ = User.prototype;
```

### Step 3:

Binds `this` to new object

```js id="y7n7re"
User.call(obj, "Aman", 22);
```

### Step 4:

Returns the object

So:

```js id="a0bd2m"
user1 → { name: "Aman", age: 22 }
```

This is the hidden magic of `new`.

---

# 5️⃣ Without `new` (Common Mistake)

```js id="6lmpht"
const user = User("Aman", 22);
```

Now:

* `this` becomes `undefined` (in strict mode)
* Or `window` (in non-strict mode)

This can break your program badly.

Always use `new`.

---

# 6️⃣ Adding Methods Inside Constructor

You can do:

```js id="m2db5v"
function User(name, age) {
  this.name = name;
  this.age = age;
  this.greet = function () {
    console.log("Hi, I am " + this.name);
  };
}
```

Works fine:

```js id="unw1pm"
const user1 = new User("Aman", 22);
user1.greet();
```

---

## ❌ Problem: Memory Waste

Each object gets its own copy of `greet()`.

If you create 10,000 users:

* 10,000 copies of same function in memory.

Bad design.

---

# 7️⃣ Correct Way: Use Prototype

Better approach:

```js id="lkhog3"
function User(name, age) {
  this.name = name;
  this.age = age;
}

User.prototype.greet = function () {
  console.log("Hi, I am " + this.name);
};
```

Now:

```js id="7lo41m"
const user1 = new User("Aman", 22);
const user2 = new User("Rahul", 25);
```

Both share same `greet()` method.

Memory efficient.

---

# 8️⃣ How Prototype Sharing Works

When you call:

```js id="t62slf"
user1.greet();
```

JS searches:

1. user1 object → not found
2. user1.**proto** → found
3. Executes it

This is prototype chain lookup (next topic).

---

# 9️⃣ Checking Instance

Use `instanceof`:

```js id="h7uyk6"
console.log(user1 instanceof User); // true
```

Checks if:

```id="32n91u"
User.prototype exists in user1's prototype chain
```

---

# 🔟 Constructor Returning Custom Object

If constructor returns object explicitly:

```js id="n14zlg"
function User(name) {
  this.name = name;
  return { custom: "object" };
}

const user = new User("Aman");
```

Now:

```js id="m7v0ci"
console.log(user); // { custom: "object" }
```

Because constructor returned its own object.

If it returns primitive:

```js id="2g9hmo"
return 5;
```

It gets ignored.

---

# 1️⃣1️⃣ Built-in Constructors

JavaScript itself uses constructor functions:

```js id="zk0lqp"
const arr = new Array();
const obj = new Object();
const date = new Date();
```

Modern practice avoids using `new Object()` or `new Array()`.

Use:

```js id="v61l7z"
[]
{}
```

Cleaner.

---

# 1️⃣2️⃣ Simulating Private Variables (Closure Trick)

Before classes had private fields:

```js id="5u8mld"
function User(name) {
  let secret = "hidden";

  this.name = name;

  this.getSecret = function () {
    return secret;
  };
}
```

Now:

```js id="b1slvu"
const user = new User("Aman");
console.log(user.secret); // undefined
console.log(user.getSecret()); // hidden
```

Uses closure for privacy.

---

# 1️⃣3️⃣ Constructor vs Factory Function

Constructor:

```js id="wtq9xa"
function User(name) {
  this.name = name;
}
```

Factory:

```js id="7bdlyz"
function createUser(name) {
  return {
    name
  };
}
```

Difference:

* Constructor needs `new`
* Factory returns object directly
* Factory is safer (no accidental missing `new`)

---

# 1️⃣4️⃣ Why Classes Were Introduced

Constructor functions were confusing because:

* `new` magic
* Prototype handling
* Manual inheritance setup

So ES6 introduced:

```js id="w6q7od"
class User {
  constructor(name) {
    this.name = name;
  }
}
```

But internally, classes still use constructor + prototype.

---


# 🟢 7. Prototypes & Prototype Chain (VERY IMPORTANT)

---

# 1️⃣ JavaScript is Prototype-Based (Not Class-Based)

Languages like:

* Java
* C++
* C#

Use classical class-based inheritance.

JavaScript uses **prototype-based inheritance**.

That means:

> Objects inherit directly from other objects.

Even when using `class`, it still uses prototypes underneath.

---

# 2️⃣ Every Object Has a Prototype

When you create an object:

```js
const user = { name: "Aman" };
```

Internally:

```text
user → has hidden link → Object.prototype
```

That hidden link is often shown as:

```js
user.__proto__
```

Better modern way:

```js
Object.getPrototypeOf(user);
```

---

# 3️⃣ What is a Prototype?

A prototype is simply **another object** that your object inherits from.

Example:

```js
const user = { name: "Aman" };

console.log(user.toString());
```

Wait — we never defined `toString()`.

Why does it work?

Because:

```text
user → Object.prototype → contains toString()
```

So JavaScript looks up the chain.

---

# 4️⃣ The Prototype Chain (How Lookup Works)

When you access:

```js
user.age
```

JavaScript checks:

1. Does `user` have `age`?
2. If not → check `user.__proto__`
3. If not → check its prototype’s prototype
4. Continue until `null`

This is called:

# 🔗 Prototype Chain

Visual:

```text
user
  ↓
User.prototype (if constructor used)
  ↓
Object.prototype
  ↓
null
```

---

# 5️⃣ Constructor Functions & Prototype Connection

Recall:

```js
function User(name) {
  this.name = name;
}

const user1 = new User("Aman");
```

Internally:

```text
user1.__proto__ === User.prototype
```

Verify:

```js
console.log(Object.getPrototypeOf(user1) === User.prototype); // true
```

That’s the critical link.

---

# 6️⃣ Why Use Prototype for Methods?

Bad approach:

```js
function User(name) {
  this.name = name;
  this.greet = function () {
    console.log("Hi");
  };
}
```

Each object gets its own copy.

Better:

```js
User.prototype.greet = function () {
  console.log("Hi " + this.name);
};
```

Now:

* All instances share one method.
* Memory efficient.
* Professional approach.

---

# 7️⃣ The `prototype` Property vs `__proto__`

This confuses many developers.

## 🔹 `prototype`

Exists on constructor functions.

```js
User.prototype
```

Used when creating new objects.

---

## 🔹 `__proto__`

Exists on object instances.

```js
user1.__proto__
```

Points to constructor’s prototype.

Connection:

```js
user1.__proto__ === User.prototype
```

---

# 8️⃣ Overriding Prototype Properties

Example:

```js
User.prototype.role = "user";

const user1 = new User("Aman");

console.log(user1.role); // "user"
```

If you add directly to instance:

```js
user1.role = "admin";
```

Now:

```js
console.log(user1.role); // "admin"
```

JavaScript always checks:

1. Instance
2. Then prototype

Instance property overrides prototype property.

---

# 9️⃣ Inheritance Between Constructors (Pre-ES6)

Parent:

```js
function Animal(name) {
  this.name = name;
}

Animal.prototype.speak = function () {
  console.log("Animal sound");
};
```

Child:

```js
function Dog(name) {
  Animal.call(this, name);
}
```

Now link prototypes:

```js
Dog.prototype = Object.create(Animal.prototype);
Dog.prototype.constructor = Dog;
```

Now:

```js
Dog.prototype.bark = function () {
  console.log("Woof!");
};
```

Usage:

```js
const dog = new Dog("Tommy");
dog.speak(); // inherited
dog.bark();
```

This is manual prototype inheritance.

---

# 🔟 How `instanceof` Works

```js
dog instanceof Dog // true
dog instanceof Animal // true
```

Why?

Because:

```text
Dog.prototype exists in dog’s prototype chain
Animal.prototype exists in dog’s prototype chain
```

`instanceof` checks the prototype chain.

---

# 1️⃣1️⃣ Prototype Chain Example (Deep Visualization)

```js
const arr = [1, 2, 3];
```

Chain looks like:

```text
arr
  ↓
Array.prototype
  ↓
Object.prototype
  ↓
null
```

That’s why:

```js
arr.push()   // from Array.prototype
arr.toString() // from Object.prototype
```

---

# 1️⃣2️⃣ Object.create()

Creates object with specific prototype.

```js
const animal = {
  speak() {
    console.log("Sound");
  }
};

const dog = Object.create(animal);
dog.speak();
```

Chain:

```text
dog
  ↓
animal
  ↓
Object.prototype
  ↓
null
```

Pure prototype-based inheritance.

---

# 1️⃣3️⃣ Everything in JS Is Connected

Even functions:

```js
function greet() {}
```

Chain:

```text
greet
  ↓
Function.prototype
  ↓
Object.prototype
  ↓
null
```

Functions are objects too.

---

# 1️⃣4️⃣ Common Mistakes

### ❌ Modifying built-in prototypes

```js
Array.prototype.custom = function() {};
```

Very dangerous in real projects.

---

### ❌ Forgetting to reset constructor after inheritance

After:

```js
Dog.prototype = Object.create(Animal.prototype);
```

You must do:

```js
Dog.prototype.constructor = Dog;
```

Otherwise constructor reference breaks.

---

# 1️⃣5️⃣ Classes Are Just Syntactic Sugar

```js
class User {
  constructor(name) {
    this.name = name;
  }

  greet() {
    console.log("Hi");
  }
}
```

Internally becomes:

```js
function User(name) {
  this.name = name;
}

User.prototype.greet = function() {};
```

Classes do NOT replace prototypes.
They simplify syntax.

---

# 🧠 Final Mental Model

When you access:

```js
obj.someProperty
```

JavaScript:

1. Looks inside `obj`
2. If not found → goes to `obj.__proto__`
3. Continues until `null`
4. If not found → returns `undefined`

That’s the prototype chain.

---

# 🎯 If You Truly Understand This, You’re Advanced

You should be comfortable with:

* What prototype is
* How `new` links objects
* Difference between `prototype` and `__proto__`
* How lookup works
* How inheritance works manually
* Why classes are syntactic sugar
* How `instanceof` works

---


# 🟢 8. Classes (ES6 Syntax) — Deep Dive

---

# 1️⃣ Basic Class Syntax

```js
class User {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  greet() {
    console.log("Hi, I am " + this.name);
  }
}

const user1 = new User("Aman", 22);
user1.greet();
```

This looks new, but internally it's doing:

* Creating constructor function
* Adding methods to `User.prototype`

---

# 2️⃣ What Happens Internally?

This:

```js
class User {
  constructor(name) {
    this.name = name;
  }

  greet() {
    console.log("Hi");
  }
}
```

Is roughly equivalent to:

```js
function User(name) {
  this.name = name;
}

User.prototype.greet = function () {
  console.log("Hi");
};
```

So classes are cleaner syntax, not a new inheritance model.

---

# 3️⃣ Constructor Method

Every class can have a special method:

```js
constructor()
```

Rules:

* Only one constructor allowed
* Automatically called when `new` is used
* Required if you want to initialize properties

Example:

```js
class Car {
  constructor(brand) {
    this.brand = brand;
  }
}
```

---

# 4️⃣ Methods in Classes

Inside class:

```js
class User {
  greet() {
    console.log("Hello");
  }
}
```

Important:

* Methods are added to `prototype`
* They are NOT stored inside each object
* Memory efficient

Verify:

```js
console.log(User.prototype);
```

You will see `greet` there.

---

# 5️⃣ Class Expressions

Classes can also be expressions.

```js
const User = class {
  constructor(name) {
    this.name = name;
  }
};
```

Rarely used but valid.

---

# 6️⃣ Static Methods

Static methods belong to the class itself, not instances.

```js
class MathHelper {
  static add(a, b) {
    return a + b;
  }
}

console.log(MathHelper.add(5, 3)); // 8
```

You cannot call:

```js
const obj = new MathHelper();
obj.add(); ❌
```

Static methods are often used for utilities.

---

# 7️⃣ Getters and Setters

Classes support getters and setters.

```js
class User {
  constructor(first, last) {
    this.first = first;
    this.last = last;
  }

  get fullName() {
    return this.first + " " + this.last;
  }

  set fullName(value) {
    const parts = value.split(" ");
    this.first = parts[0];
    this.last = parts[1];
  }
}

const user = new User("Aman", "Sharma");
console.log(user.fullName);

user.fullName = "Rahul Verma";
console.log(user.first);
```

They look like properties but behave like functions.

---

# 8️⃣ Inheritance with `extends`

Now we reach powerful part.

Parent class:

```js
class Animal {
  constructor(name) {
    this.name = name;
  }

  speak() {
    console.log("Animal sound");
  }
}
```

Child class:

```js
class Dog extends Animal {
  bark() {
    console.log("Woof!");
  }
}

const dog = new Dog("Tommy");
dog.speak(); // inherited
dog.bark();
```

---

# 9️⃣ Using `super()`

If child has constructor:

```js
class Dog extends Animal {
  constructor(name, breed) {
    super(name); // calls parent constructor
    this.breed = breed;
  }
}
```

Important rules:

* You MUST call `super()` before using `this`
* `super()` calls parent constructor

If not:

```js
constructor(name) {
  this.name = name; ❌ error
}
```

---

# 🔟 Overriding Methods

Child can override parent methods.

```js
class Dog extends Animal {
  speak() {
    console.log("Bark");
  }
}
```

If you want both:

```js
class Dog extends Animal {
  speak() {
    super.speak();
    console.log("Bark");
  }
}
```

---

# 1️⃣1️⃣ Private Fields (Modern Feature)

New syntax using `#`.

```js
class BankAccount {
  #balance = 0;

  deposit(amount) {
    this.#balance += amount;
  }

  getBalance() {
    return this.#balance;
  }
}

const account = new BankAccount();
account.deposit(100);
console.log(account.getBalance());
```

You cannot access:

```js
account.#balance ❌
```

True privacy enforced by JavaScript engine.

---

# 1️⃣2️⃣ Public Class Fields

Modern syntax:

```js
class User {
  role = "user";

  constructor(name) {
    this.name = name;
  }
}
```

This defines property directly on instance.

---

# 1️⃣3️⃣ Important Differences from Constructor Functions

### 1. Classes are not hoisted

```js
const user = new User(); ❌
class User {}
```

You must define class first.

---

### 2. Classes run in strict mode automatically

Inside class:

* `this` is never global
* Mistakes throw errors

---

### 3. Methods are non-enumerable

Unlike manually adding to object.

---

# 1️⃣4️⃣ Checking Instance

```js
const dog = new Dog("Tommy");

console.log(dog instanceof Dog);      // true
console.log(dog instanceof Animal);   // true
```

Still works using prototype chain.

---

# 1️⃣5️⃣ Under the Hood Chain

For:

```js
class Dog extends Animal {}
```

Chain becomes:

Instance level:

```
dog
 ↓
Dog.prototype
 ↓
Animal.prototype
 ↓
Object.prototype
 ↓
null
```

Constructor level:

```
Dog
 ↓
Animal
 ↓
Function.prototype
```

Two chains exist:

* Instance prototype chain
* Constructor inheritance chain

Advanced but important.

---

# 🎯 What You Must Understand About Classes

You should clearly know:

* Classes are syntactic sugar
* Methods go to prototype
* `constructor` initializes instance
* `extends` sets prototype chain
* `super()` calls parent constructor
* Static methods belong to class
* Private fields use `#`
* `instanceof` checks prototype chain

---

# 🔥 When to Use Classes?

Use classes when:

* Building structured models
* Creating reusable blueprints
* Working with frameworks (React, NestJS, Angular)
* Designing OOP systems

Avoid when:

* Simple object needed
* Functional style preferred

---


# 🟢 9. Advanced Object Concepts

We’ll cover:

1. Property Descriptors
2. `Object.defineProperty()`
3. Writable / Enumerable / Configurable
4. Object immutability patterns
5. Symbols as keys
6. Computed property names
7. Object iteration control
8. Reflect API (intro)
9. Proxy (intro to meta-programming)

---

# 1️⃣ Property Descriptors (The Hidden Layer)

Every property in JavaScript has hidden metadata.

When you create:

```js
const user = {
  name: "Aman"
};
```

It’s internally stored like:

```js
{
  value: "Aman",
  writable: true,
  enumerable: true,
  configurable: true
}
```

You can inspect it:

```js
Object.getOwnPropertyDescriptor(user, "name");
```

Output:

```js
{
  value: "Aman",
  writable: true,
  enumerable: true,
  configurable: true
}
```

These are called **Property Descriptors**.

---

# 2️⃣ Descriptor Properties Explained

### 🟢 value

Actual stored value.

---

### 🟢 writable

Can the value be changed?

```js
writable: false
```

Now:

```js
user.name = "Rahul"; // ignored (or error in strict mode)
```

---

### 🟢 enumerable

Controls whether property appears in:

* `Object.keys()`
* `for...in`
* `Object.entries()`

If:

```js
enumerable: false
```

Then property becomes hidden from iteration.

---

### 🟢 configurable

Controls whether:

* Property can be deleted
* Descriptor can be modified

If:

```js
configurable: false
```

Then:

```js
delete user.name; ❌
```

---

# 3️⃣ `Object.defineProperty()`

Lets you manually define descriptor behavior.

Example:

```js
const user = {};

Object.defineProperty(user, "id", {
  value: 123,
  writable: false,
  enumerable: false,
  configurable: false
});
```

Now:

* Cannot modify
* Not visible in `Object.keys`
* Cannot delete

---

## Real-world Use

Libraries use this to:

* Hide internal properties
* Protect critical data
* Create framework internals

---

# 4️⃣ Accessor Properties (Getter/Setter via Descriptors)

Instead of `value`, you can define:

* `get`
* `set`

Example:

```js
const user = {
  first: "Aman",
  last: "Sharma"
};

Object.defineProperty(user, "fullName", {
  get() {
    return this.first + " " + this.last;
  }
});
```

Now:

```js
console.log(user.fullName);
```

No actual `fullName` value stored — it's computed dynamically.

---

# 5️⃣ `Object.defineProperties()`

Define multiple properties at once.

```js
Object.defineProperties(user, {
  age: {
    value: 22,
    writable: true
  },
  country: {
    value: "India",
    writable: false
  }
});
```

---

# 6️⃣ Object Immutability Patterns

There are levels of immutability.

---

## 🔵 `Object.preventExtensions()`

Prevents adding new properties.

```js
Object.preventExtensions(user);
user.newProp = 1; // ❌
```

---

## 🟡 `Object.seal()`

* Cannot add
* Cannot delete
* Can modify existing

---

## 🔴 `Object.freeze()`

* Cannot add
* Cannot delete
* Cannot modify

But all are shallow.

---

## Deep Freeze Pattern

```js
function deepFreeze(obj) {
  Object.getOwnPropertyNames(obj).forEach(prop => {
    if (typeof obj[prop] === "object" && obj[prop] !== null) {
      deepFreeze(obj[prop]);
    }
  });

  return Object.freeze(obj);
}
```

Now nested objects also frozen.

Used in Redux-style architectures.

---

# 7️⃣ Symbols as Object Keys

Symbols create unique keys.

```js
const id = Symbol("id");

const user = {
  name: "Aman",
  [id]: 123
};
```

Why useful?

* Avoid name collisions
* Hidden internal properties
* Library-level architecture

Important:

```js
Object.keys(user); // doesn't include Symbol keys
```

To get symbols:

```js
Object.getOwnPropertySymbols(user);
```

---

# 8️⃣ Computed Property Names (Advanced Usage)

Dynamic keys:

```js
const key = "score";

const obj = {
  [key + "_2024"]: 95
};
```

Powerful for:

* Dynamic API mapping
* Config generation
* Key transformation logic

---

# 9️⃣ Controlling Object Iteration

Difference:

```js
Object.keys(obj)
Object.getOwnPropertyNames(obj)
Object.getOwnPropertySymbols(obj)
Reflect.ownKeys(obj)
```

### `Reflect.ownKeys()`

Returns:

* String keys
* Symbol keys
* Enumerable + non-enumerable

Most complete method.

---

# 🔟 Reflect API (Intro)

Reflect is modern alternative to Object methods.

Example:

```js
Reflect.get(obj, "name");
Reflect.set(obj, "name", "Rahul");
Reflect.has(obj, "name");
```

Why Reflect?

* Cleaner semantics
* Works perfectly with Proxy
* Returns boolean instead of throwing

Used heavily in advanced frameworks.

---

# 1️⃣1️⃣ Proxy (Meta-Programming)

Proxy allows you to intercept object operations.

Example:

```js
const user = {
  name: "Aman"
};

const proxy = new Proxy(user, {
  get(target, prop) {
    console.log("Accessed:", prop);
    return target[prop];
  }
});

proxy.name;
```

Output:

```
Accessed: name
```

Proxy can intercept:

* get
* set
* delete
* has
* apply
* etc.

Used in:

* Vue reactivity
* Modern frameworks
* Validation systems
* Security layers

---

# 1️⃣2️⃣ Internal Object Slots (Conceptual)

Objects have internal slots like:

* [[Prototype]]
* [[Extensible]]
* [[Get]]
* [[Set]]

You don’t access these directly.
Descriptors & Reflect expose controlled interfaces to them.

---

# 1️⃣3️⃣ Enumerability Deep Understanding

Why doesn’t this show in `for...in`?

Because built-in prototype methods are:

```js
enumerable: false
```

That’s why:

```js
for (let key in []) {
  console.log(key);
}
```

Does not print `push`, `pop`, etc.

---

# 1️⃣4️⃣ Performance Considerations

Important advanced insight:

* Adding properties dynamically changes object shape.
* Engines optimize objects based on stable structure.
* Changing structure frequently hurts performance.

Example of bad pattern:

```js
const obj = {};
obj.a = 1;
obj.b = 2;
delete obj.a;
```

Frequent shape changes reduce optimization.

---


# 1️⃣ What is JSON?

**JSON** stands for:

> JavaScript Object Notation

It is a **text format** used to store and transfer data.

Important:

> JSON is a string format.
> JavaScript objects are runtime data structures.

They look similar — but they are NOT the same.

---

# 2️⃣ JSON vs JavaScript Object (Critical Differences)

### ✅ JavaScript Object

```js
const user = {
  name: "Aman",
  age: 22,
  isAdmin: false
};
```

### ✅ JSON

```json
{
  "name": "Aman",
  "age": 22,
  "isAdmin": false
}
```

Looks similar — but strict rules apply in JSON.

---

# 3️⃣ JSON Rules (Very Important)

JSON:

* Keys MUST be in double quotes
* Strings MUST use double quotes
* No functions allowed
* No `undefined`
* No comments
* No trailing commas
* Only supports:

  * string
  * number
  * boolean
  * null
  * array
  * object

Invalid JSON example:

```json
{
  name: "Aman" ❌
}
```

Valid JSON:

```json
{
  "name": "Aman"
}
```

---

# 4️⃣ `JSON.stringify()` — Object → JSON String

Converts JavaScript object into JSON string.

```js
const user = {
  name: "Aman",
  age: 22
};

const jsonString = JSON.stringify(user);
console.log(jsonString);
```

Output:

```text
{"name":"Aman","age":22}
```

Now it's a string.

Check:

```js
typeof jsonString; // "string"
```

---

# 5️⃣ `JSON.parse()` — JSON String → Object

Converts JSON string back to object.

```js
const jsonString = '{"name":"Aman","age":22}';

const obj = JSON.parse(jsonString);
console.log(obj.name);
```

Now it's usable as normal object.

---

# 6️⃣ Why Do We Need JSON?

Because when sending data:

* Between frontend & backend
* Over HTTP
* To localStorage
* To database
* Across network

Data must be sent as string.

JSON is the universal format.

---

# 7️⃣ What `JSON.stringify()` Ignores

Very important interview topic.

Example:

```js
const user = {
  name: "Aman",
  age: undefined,
  greet() {
    console.log("Hi");
  }
};

console.log(JSON.stringify(user));
```

Output:

```text
{"name":"Aman"}
```

Removed:

* `undefined`
* functions
* Symbol properties

---

# 8️⃣ What Happens to Special Values?

### 🔹 `undefined`

Removed in objects.

In arrays:

```js
JSON.stringify([1, undefined, 3]);
```

Output:

```text
[1,null,3]
```

---

### 🔹 `NaN`, `Infinity`

Converted to:

```text
null
```

---

### 🔹 Dates

```js
const obj = { date: new Date() };
console.log(JSON.stringify(obj));
```

Converted to ISO string.

---

# 9️⃣ Circular Reference Problem

JSON cannot handle circular references.

Example:

```js
const obj = {};
obj.self = obj;

JSON.stringify(obj); // ❌ error
```

Error:

> Converting circular structure to JSON

Because JSON cannot represent cycles.

---

# 🔟 Pretty Formatting

You can format JSON:

```js
JSON.stringify(user, null, 2);
```

Parameters:

1. Object
2. Replacer
3. Space indentation

Example output:

```json
{
  "name": "Aman",
  "age": 22
}
```

Very useful for debugging.

---

# 1️⃣1️⃣ Replacer Function (Advanced)

You can control what gets serialized.

```js
JSON.stringify(user, (key, value) => {
  if (key === "password") return undefined;
  return value;
});
```

Used for:

* Hiding sensitive fields
* Transforming values
* Filtering data

---

# 1️⃣2️⃣ Reviver Function (Advanced Parsing)

`JSON.parse()` also accepts function.

```js
JSON.parse(jsonString, (key, value) => {
  if (key === "age") return value + 1;
  return value;
});
```

Used for:

* Data transformation
* Restoring Date objects
* Custom parsing logic

---

# 1️⃣3️⃣ Deep Copy Using JSON (Common Trick)

```js
const copy = JSON.parse(JSON.stringify(obj));
```

Works for simple objects.

But fails for:

* Dates
* Functions
* Undefined
* Symbols
* Maps
* Sets
* Circular references

Modern better solution:

```js
structuredClone(obj);
```

---

# 1️⃣4️⃣ JSON and localStorage

localStorage only stores strings.

```js
localStorage.setItem("user", JSON.stringify(user));
```

Retrieve:

```js
const user = JSON.parse(localStorage.getItem("user"));
```

Very common real-world use case.

---

# 1️⃣5️⃣ JSON vs Object Performance

* JSON.stringify is expensive for large objects
* Avoid unnecessary serialization
* Used carefully in performance-critical apps

---

# 1️⃣6️⃣ Security Considerations

⚠️ Never use `eval()` to parse JSON.

Wrong:

```js
eval('(' + jsonString + ')'); ❌
```

Always use:

```js
JSON.parse()
```

Because:

* Safe
* Prevents code injection

---

# 1️⃣7️⃣ JSON vs JavaScript Object Summary

| Feature                | JS Object | JSON |
| ---------------------- | --------- | ---- |
| Functions              | ✅         | ❌    |
| Undefined              | ✅         | ❌    |
| Comments               | ✅         | ❌    |
| Double quotes required | ❌         | ✅    |
| Executable             | ✅         | ❌    |
| Data transfer          | ❌         | ✅    |

---

# 1️⃣8️⃣ Real-World API Example

Backend response:

```json
{
  "success": true,
  "data": {
    "user": {
      "id": 1,
      "name": "Aman"
    }
  }
}
```

In frontend:

```js
fetch("/api")
  .then(res => res.json())
  .then(data => {
    console.log(data.data.user.name);
  });
```

`.json()` internally does `JSON.parse()`.

---

# 1️⃣9️⃣ Common Interview Questions

1. Difference between JSON and JS object?
2. What does JSON.stringify remove?
3. How to handle circular references?
4. How to deep copy object?
5. What happens to Date objects?
6. What are replacer and reviver functions?

---

# 🎯 What You Must Master

You should clearly understand:

* JSON is string format
* stringify vs parse
* What gets removed
* Circular reference limitation
* Deep copy limitations
* API usage patterns
* localStorage usage
* Replacer and reviver

---


# 1️⃣ What is OOP?

OOP is a programming paradigm based on:

> Modeling real-world entities as objects with state + behavior.

An object has:

* State → properties
* Behavior → methods

Example:

```js
class User {
  constructor(name) {
    this.name = name;   // state
  }

  greet() {             // behavior
    console.log("Hi " + this.name);
  }
}
```

---

# 2️⃣ The 4 Pillars of OOP

1. Encapsulation
2. Abstraction
3. Inheritance
4. Polymorphism

Let’s go deep.

---

# 🟢 1. Encapsulation

> Bundling data + methods together and restricting direct access.

In JavaScript, achieved via:

* Private fields (`#`)
* Closures
* Module pattern
* Controlled setters/getters

### Example (Private Fields)

```js
class BankAccount {
  #balance = 0;

  deposit(amount) {
    if (amount > 0) this.#balance += amount;
  }

  getBalance() {
    return this.#balance;
  }
}
```

Now:

```js
account.#balance ❌
```

That’s encapsulation.

---

# 🟢 2. Abstraction

> Hiding implementation details, exposing only necessary functionality.

User doesn’t care how it works internally.

Example:

```js
class Car {
  start() {
    this.#injectFuel();
    this.#igniteEngine();
  }

  #injectFuel() {}
  #igniteEngine() {}
}
```

User calls:

```js
car.start();
```

They don’t know internal complexity.

That’s abstraction.

---

# 🟢 3. Inheritance

> Child class inherits properties and methods from parent.

```js
class Animal {
  speak() {
    console.log("Animal sound");
  }
}

class Dog extends Animal {
  bark() {
    console.log("Woof");
  }
}
```

Dog gets `speak()` automatically.

This uses the prototype chain internally.

---

# 🟢 4. Polymorphism

> Same method name, different behavior.

Example:

```js
class Animal {
  speak() {
    console.log("Animal sound");
  }
}

class Dog extends Animal {
  speak() {
    console.log("Woof");
  }
}
```

Calling:

```js
animal.speak();
dog.speak();
```

Different outputs.

That’s runtime polymorphism.

---

# 3️⃣ Classical vs Prototypal OOP

Java, C++ → Classical OOP
JavaScript → Prototypal OOP

In JS:

* Objects inherit from objects
* Not classes inheriting classes (internally)
* Classes are syntax sugar

Prototype chain is the real inheritance mechanism.

---

# 4️⃣ Composition vs Inheritance (VERY IMPORTANT)

Modern JavaScript favors:

> Composition over inheritance

Instead of:

```js
class Dog extends Animal {}
```

We can do:

```js
const canBark = {
  bark() {
    console.log("Woof");
  }
};

const dog = {
  name: "Tommy",
  ...canBark
};
```

Why composition is better:

* More flexible
* Avoids deep inheritance trees
* Easier to maintain
* Less tightly coupled

Real-world frameworks prefer composition.

---

# 5️⃣ Example: Real OOP Design

Let’s design a simple system.

### Bad design

```js
class User {
  constructor(name) {
    this.name = name;
  }
}

class Admin extends User {
  deleteUser() {}
}

class SuperAdmin extends Admin {}
```

Deep inheritance = fragile system.

---

### Better design (composition)

```js
const canDeleteUsers = {
  deleteUser() {}
};

function createUser(name) {
  return {
    name
  };
}

function createAdmin(name) {
  return {
    ...createUser(name),
    ...canDeleteUsers
  };
}
```

More flexible.

---

# 6️⃣ OOP in Real JavaScript Apps

Used in:

* Backend services
* Node.js applications
* Game engines
* Enterprise software
* Framework internals

Example frameworks:

* Angular → heavy class-based
* NestJS → OOP-based architecture

Modern React → prefers functions + composition.

---

# 7️⃣ Common OOP Patterns in JS

### Factory Pattern

```js
function createUser(name) {
  return {
    name,
    greet() {
      console.log("Hi");
    }
  };
}
```

---

### Constructor Pattern

```js
function User(name) {
  this.name = name;
}
```

---

### Class Pattern

```js
class User {}
```

---

### Module Pattern

Encapsulation via closure:

```js
function createCounter() {
  let count = 0;

  return {
    increment() { count++; },
    getCount() { return count; }
  };
}
```

---

# 8️⃣ When NOT to Use OOP

Avoid OOP when:

* Writing small utilities
* Data transformations
* Functional pipelines
* Pure logic-heavy code

Functional programming is often cleaner for:

* Array transformations
* Async flows
* React components

---

# 9️⃣ Common OOP Mistakes in JS

1. Overusing inheritance
2. Deep class hierarchies
3. Ignoring composition
4. Mutating internal state everywhere
5. Not understanding `this` properly

---

# 🔟 Interview-Level Understanding

If asked:

> Does JavaScript support OOP?

Correct answer:

Yes. JavaScript supports object-oriented programming through:

* Prototypal inheritance
* Constructor functions
* ES6 classes
* Encapsulation via closures and private fields
* Polymorphism via method overriding

But it is not class-based like Java — it is prototype-based.

---

# 🎯 What You Should Now Understand

You should clearly know:

* What OOP means conceptually
* The 4 pillars
* How JS implements them
* Why classes are syntactic sugar
* Why composition is often better
* When to use OOP vs functional style

---


# 🟢 12. Objects in Real-World Scenarios

We’ll cover:

1. Modeling real-world entities
2. API response handling
3. State management
4. Configuration objects
5. Validation systems
6. Object patterns in backend
7. React & frontend usage
8. Database mapping
9. Common architectural patterns

---

# 1️⃣ Modeling Real-World Entities

Objects are used to represent business concepts.

Example: E-commerce User

```js
class User {
  constructor(id, name, email) {
    this.id = id;
    this.name = name;
    this.email = email;
    this.orders = [];
  }

  addOrder(order) {
    this.orders.push(order);
  }
}
```

Now your app models real business logic.

In backend frameworks like NestJS, classes are heavily used to model:

* Users
* Orders
* Products
* Services

---

# 2️⃣ Handling API Responses

Backend returns JSON:

```json
{
  "id": 1,
  "name": "Aman",
  "role": "admin"
}
```

Frontend converts to object:

```js
fetch("/api/user")
  .then(res => res.json())
  .then(data => {
    const user = new User(data.id, data.name, data.role);
  });
```

Why wrap API data in class?

* Add methods
* Add computed properties
* Keep logic organized

---

# 3️⃣ State Management (Very Common)

Objects store application state.

Example:

```js
const appState = {
  user: null,
  cart: [],
  isLoading: false
};
```

State changes:

```js
appState.user = { id: 1, name: "Aman" };
```

In libraries like Redux:

* State is a big object
* Updates must be immutable
* Deep copying becomes important

---

# 4️⃣ Configuration Objects Pattern

Very common real-world pattern.

Instead of multiple parameters:

```js
createUser("Aman", 22, "admin", true);
```

We pass config object:

```js
createUser({
  name: "Aman",
  age: 22,
  role: "admin",
  isActive: true
});
```

Why better?

* Order doesn't matter
* Optional properties easy
* Scalable
* Cleaner APIs

Used everywhere:

* Node.js libraries
* Database drivers
* UI frameworks

---

# 5️⃣ Validation Systems

Objects are validated before use.

Example:

```js
function validateUser(user) {
  if (!user.name) throw new Error("Name required");
  if (typeof user.age !== "number") throw new Error("Invalid age");
}
```

In production apps, validation schemas are objects too:

```js
const userSchema = {
  name: "string",
  age: "number",
  email: "string"
};
```

Libraries convert these schema objects into validation logic.

---

# 6️⃣ Backend Architecture (Service Layer)

Example structure:

```js
class UserService {
  constructor(userRepository) {
    this.userRepository = userRepository;
  }

  createUser(data) {
    return this.userRepository.save(data);
  }
}
```

Objects here represent:

* Services
* Controllers
* Repositories
* Models

Frameworks like Express.js often use objects to group logic:

```js
const userController = {
  create(req, res) {},
  update(req, res) {},
  delete(req, res) {}
};
```

---

# 7️⃣ Objects in Frontend (React Example)

In React, objects are everywhere:

### Component props

```js
<User name="Aman" age={22} />
```

Becomes:

```js
{
  name: "Aman",
  age: 22
}
```

### State

```js
const [user, setUser] = useState({
  name: "",
  age: 0
});
```

State is just an object.

Immutability becomes critical:

```js
setUser(prev => ({
  ...prev,
  name: "Rahul"
}));
```

---

# 8️⃣ Database Mapping (ORM Style)

Objects represent database records.

Example:

```js
class Product {
  constructor(data) {
    this.id = data.id;
    this.name = data.name;
    this.price = data.price;
  }

  applyDiscount(percent) {
    this.price -= this.price * percent;
  }
}
```

When data comes from DB → convert to object → attach behavior.

This pattern is called:

> Data Mapper Pattern

---

# 9️⃣ Logging & Monitoring Systems

Log entries are objects:

```js
const log = {
  level: "error",
  message: "Something failed",
  timestamp: new Date(),
  userId: 1
};
```

Then converted to JSON and sent to logging service.

Objects become structured data pipelines.

---

# 🔟 Middleware & Plugin Systems

Objects often define behavior contracts:

```js
const plugin = {
  name: "logger",
  init(app) {},
  destroy() {}
};
```

Framework reads object and executes hooks.

---

# 1️⃣1️⃣ API Request Objects

Instead of many arguments:

```js
sendRequest({
  url: "/api",
  method: "POST",
  headers: {},
  body: {}
});
```

Config object pattern again.

Used in:

* Fetch API
* Axios
* Node HTTP modules

---

# 1️⃣2️⃣ Security & Permissions Systems

Objects define role permissions:

```js
const roles = {
  admin: ["create", "delete", "update"],
  user: ["read"],
  guest: []
};
```

Application checks permissions dynamically.

---

# 1️⃣3️⃣ Caching Systems

Cache often stored as object:

```js
const cache = {};

function getData(key) {
  if (cache[key]) return cache[key];
}
```

Object used as fast key-value store.

---

# 1️⃣4️⃣ Performance Considerations in Real Apps

In large apps:

* Avoid deeply nested objects when possible
* Normalize state structure
* Avoid frequent object shape changes
* Use immutability patterns carefully

Example bad:

```js
state.user.profile.settings.theme.color.background
```

Hard to manage.

Better normalized structure.

---


# 🟢 13. Interview-Level Topics (Objects in JavaScript)

We’ll cover:

1. Most asked theory questions
2. Deep conceptual traps
3. Output-based questions
4. Edge cases interviewers love
5. Architecture-level discussion topics
6. Senior-level follow-up questions

---

# 1️⃣ Frequently Asked Core Questions

You must answer these confidently.

---

## ❓ Difference between Object.create() and new?

```js
function User(name) {
  this.name = name;
}

const u1 = new User("Aman");
const u2 = Object.create(User.prototype);
```

### Key Differences:

| `new`                  | `Object.create()`                |
| ---------------------- | -------------------------------- |
| Calls constructor      | Does NOT call constructor        |
| Sets prototype         | Sets prototype                   |
| Initializes properties | Doesn’t initialize automatically |

Correct explanation:

> `new` creates object, links prototype, binds `this`, and executes constructor.
> `Object.create()` only sets prototype.

---

## ❓ Difference between `__proto__` and `prototype`?

This question filters beginners from serious developers.

* `prototype` → property of constructor functions
* `__proto__` → internal reference of an object to its prototype

Example:

```js
function User() {}
const u = new User();

User.prototype  // exists
u.__proto__     // points to User.prototype
```

Better explanation:

> `prototype` is used to build inheritance.
> `__proto__` is how objects actually link internally.

---

## ❓ What is the prototype chain?

Correct answer:

> When a property is not found on an object, JavaScript looks up the chain via [[Prototype]] until null.

Mention:

```
obj → Constructor.prototype → Object.prototype → null
```

If you can explain lookup algorithm clearly, you pass.

---

# 2️⃣ Tricky Output Questions

These are very common.

---

## 🔥 Question 1

```js
function User() {}
User.prototype.age = 25;

const u1 = new User();
const u2 = new User();

u1.age = 30;

console.log(u2.age);
```

Answer:

```
25
```

Why?

Because `u1.age = 30` creates own property.
`u2` still reads from prototype.

---

## 🔥 Question 2

```js
const obj = { a: 1 };

const copy = obj;
copy.a = 5;

console.log(obj.a);
```

Answer:

```
5
```

Because objects are stored by reference.

---

## 🔥 Question 3

```js
const obj = {
  name: "Aman",
  greet() {
    console.log(this.name);
  }
};

const fn = obj.greet;
fn();
```

Answer:

```
undefined (or window/global in non-strict)
```

Because `this` is lost.

Follow-up solution:

```js
const fn = obj.greet.bind(obj);
```

---

# 3️⃣ Deep Concept Questions

---

## ❓ What is object immutability?

Correct explanation:

> An immutable object cannot have its properties added, removed, or modified.

Mention:

* `Object.freeze()`
* Shallow vs deep freeze
* Immutability important in React & Redux

---

## ❓ How does JavaScript handle memory for objects?

Answer should include:

* Objects stored in heap
* Variables store reference
* Garbage collector removes unreachable objects

That’s senior-level answer.

---

## ❓ How does `instanceof` work?

Correct explanation:

> It checks whether constructor.prototype exists anywhere in object's prototype chain.

Example:

```js
dog instanceof Animal
```

Internally:

```
Animal.prototype === dog.__proto__ ?
If not → keep climbing
```

---

# 4️⃣ JSON & Object Trap Questions

---

## ❓ What does JSON.stringify remove?

Answer:

* undefined
* functions
* symbols
* converts NaN/Infinity → null

If candidate says only “functions” → incomplete.

---

## ❓ Can JSON handle circular references?

Answer:

No. It throws error.

Senior follow-up:

* Use structuredClone
* Use custom serializer
* Or remove cycle manually

---

# 5️⃣ Property Descriptor Questions

---

## ❓ Difference between writable and configurable?

Correct explanation:

* writable → controls value modification
* configurable → controls deletion + descriptor change

If configurable = false:

* Cannot delete
* Cannot redefine descriptor

This is advanced-level answer.

---

# 6️⃣ Class-Based Questions

---

## ❓ Are ES6 classes hoisted?

Answer:

No. They are in temporal dead zone.

---

## ❓ Are class methods enumerable?

Answer:

No. They are non-enumerable.

---

## ❓ What happens if you don’t call super() in subclass constructor?

Answer:

ReferenceError before using `this`.

---

# 7️⃣ Architecture-Level Questions (Senior Interviews)

These are harder.

---

## ❓ When would you choose composition over inheritance?

Correct answer:

* When behavior needs to be reused flexibly
* To avoid deep hierarchy
* To reduce tight coupling
* To increase modularity

Mention:

> “Favor composition over inheritance.”

Instant senior impression.

---

## ❓ How would you design a permission system?

Expected approach:

* Roles object
* Permission mapping
* Maybe strategy pattern
* Avoid hardcoded if-else chains

---

## ❓ How would you implement private state before ES6 private fields?

Answer:

* Closures
* Module pattern
* IIFE

---

# 8️⃣ Output-Based Prototype Trap

Very famous question:

```js
function User() {}
User.prototype = { age: 25 };

const u1 = new User();

User.prototype.age = 30;

console.log(u1.age);
```

Answer:

```
30
```

Because `u1` references the same prototype object.

Now harder:

```js
function User() {}
const u1 = new User();

User.prototype = { age: 25 };

console.log(u1.age);
```

Answer:

```
undefined
```

Because prototype was replaced AFTER instance creation.

This question filters strong developers.

---


# 🟢 14. Bonus — High-Level Mastery of JavaScript Objects

We’ll cover:

1. How JS engines optimize objects
2. Hidden Classes & Inline Caching
3. Object Shape & Performance
4. Advanced Composition Patterns
5. Meta-Programming
6. Designing Scalable Object Systems
7. Anti-Patterns to Avoid
8. Mental Models of Senior Engineers

---

# 1️⃣ How JavaScript Engines Actually Optimize Objects

Engines like Google’s V8 (used in Node.js and Google Chrome) do something interesting.

Even though JS is dynamic…

Engines try to make objects behave like static class objects internally.

They create something called:

> Hidden Classes

---

# 2️⃣ Hidden Classes (Very Important)

When you create objects with the same structure:

```js
const user1 = { name: "Aman", age: 22 };
const user2 = { name: "Rahul", age: 25 };
```

Engine sees:

* Same properties
* Same order
* Same shape

So it internally creates a shared hidden class.

This makes property access extremely fast.

---

## 🚨 Performance Killer

Changing object structure dynamically:

```js
const obj = {};
obj.a = 1;
obj.b = 2;
delete obj.a;
```

Frequent structure changes → new hidden classes → de-optimization.

Senior engineers know:

> Keep object shape stable.

---

# 3️⃣ Property Order Matters

This creates different shapes:

```js
{ name: "Aman", age: 22 }
{ age: 22, name: "Aman" }
```

Even though logically same — engine sees different shape.

For large systems, this impacts performance.

---

# 4️⃣ Inline Caching

When you do:

```js
user.name
```

Engine remembers:

* Where `name` is located in memory
* Reuses optimized lookup

But if object shape changes often → inline cache breaks.

---

# 5️⃣ Immutability & Performance

Immutability is powerful:

```js
const newUser = { ...user, age: 23 };
```

But it creates new object.

Trade-offs:

| Mutable          | Immutable        |
| ---------------- | ---------------- |
| Faster updates   | Safer state      |
| Harder debugging | Predictable      |
| Side effects     | Functional style |

In systems like Redux, immutability ensures predictable updates.

Senior developers balance performance vs maintainability.

---

# 6️⃣ Advanced Composition Pattern (Functional Mixins)

Instead of classes:

```js
const withLogger = (obj) => ({
  ...obj,
  log() {
    console.log("Logging...");
  }
});
```

Usage:

```js
const user = withLogger({ name: "Aman" });
```

No inheritance.
No deep hierarchies.
Highly modular.

This is modern scalable design.

---

# 7️⃣ Dependency Injection via Objects

Instead of hardcoding:

```js
class PaymentService {
  constructor() {
    this.gateway = new Stripe();
  }
}
```

Better:

```js
class PaymentService {
  constructor(gateway) {
    this.gateway = gateway;
  }
}
```

Now object receives dependencies.

Used heavily in NestJS.

This improves:

* Testability
* Modularity
* Flexibility

---

# 8️⃣ Meta-Programming (Advanced)

Using:

* `Proxy`
* `Reflect`
* Property descriptors

You can intercept behavior:

```js
const proxy = new Proxy(obj, {
  get(target, prop) {
    console.log("Accessed:", prop);
    return Reflect.get(target, prop);
  }
});
```

This enables:

* Reactivity systems
* Access control
* Validation layers
* Debug tools

Frameworks like Vue.js use Proxy for reactivity.

---

# 9️⃣ Object Design for Large Systems

When designing object systems at scale:

Ask:

1. Who owns the state?
2. Who is allowed to mutate it?
3. Should state be private?
4. Should behavior live with data?
5. Is inheritance necessary?
6. Will this scale to 100k users?

This is architecture thinking.

---

# 🔟 Anti-Patterns in Object Design

❌ Deep inheritance chains
❌ Massive God objects
❌ Mutating shared objects globally
❌ Passing entire objects when only one field needed
❌ Dynamic shape mutation everywhere

Senior code = predictable, stable object structure.

---

# 1️⃣1️⃣ Functional vs OOP Balance

Modern JS systems often mix:

* Functional composition
* Object modeling
* Immutable state
* Class-based services

For example:

* React → functional
* Angular → class-heavy
* Express.js → object-based middleware

There is no “one right way.”

Senior engineers choose based on context.

---

# 1️⃣2️⃣ Thinking Like a Language Expert

High-level mastery means you understand:

* Objects are hash maps with prototype delegation
* Classes are syntax sugar
* Property lookup is dynamic
* Object identity matters
* References are powerful but dangerous
* Immutability improves reasoning
* Engine optimization depends on shape stability

---

# 1️⃣3️⃣ Mental Model of Objects (Final Form)

An object in JavaScript is:

> A dynamic key-value store
>
> * hidden metadata
> * prototype linkage
> * runtime-optimized structure

Once you see it this way, everything makes sense.

---

# 1️⃣4️⃣ The Ultimate Mastery Question

If someone asks:

“Explain JavaScript objects deeply.”

You can now talk about:

* Heap memory
* References
* Descriptors
* Prototypes
* Hidden classes
* Engine optimizations
* Immutability
* Design trade-offs
* Composition patterns

That’s mastery.

---
