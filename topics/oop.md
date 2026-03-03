Perfect 👍
Now let’s deeply and clearly understand **OOP in JavaScript**, focusing on:

* ✅ Classes
* ✅ Inheritance
* ✅ Prototypes
* ✅ `this` keyword
* ✅ `super` keyword

We’ll go step-by-step from basics to internal behavior.

---

# 🔷 1️⃣ Classes in JavaScript

---

## 🔹 What is a Class?

A **class** is a blueprint for creating objects.

It defines:

* Properties (data)
* Methods (behavior)

---

## 🔹 Basic Class Syntax

```js
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  greet() {
    console.log(`Hi, I'm ${this.name}`);
  }
}

const p1 = new Person("John", 25);
p1.greet();
```

---

## 🔹 What Happens Internally?

When you write:

```js
const p1 = new Person("John", 25);
```

JavaScript:

1. Creates empty object `{}`
2. Sets prototype → `Person.prototype`
3. Binds `this` to new object
4. Executes constructor
5. Returns object

Important:

> Classes are syntactic sugar over prototype-based inheritance.

---

## 🔹 Class Features

### Instance Properties

```js
this.name = name;
```

Each object gets its own copy.

---

### Methods

```js
greet() {
  console.log("Hello");
}
```

Stored in `Person.prototype`.

All instances share it (memory efficient).

---

### Static Methods

Belong to class, not instance.

```js
class MathHelper {
  static add(a, b) {
    return a + b;
  }
}

MathHelper.add(2, 3); // 5
```

Cannot call via instance.

---

### Private Fields (Modern JS)

```js
class Bank {
  #balance;

  constructor(amount) {
    this.#balance = amount;
  }

  getBalance() {
    return this.#balance;
  }
}
```

`#balance` is truly private.

---

# 🔷 2️⃣ The `this` Keyword (Very Important)

---

## 🔹 What is `this`?

`this` refers to the **object that is calling the function**.

---

## 🔹 Inside Class Method

```js
class Person {
  constructor(name) {
    this.name = name;
  }

  greet() {
    console.log(this.name);
  }
}
```

Here:

* `this` refers to the current object.

---

## 🔹 `this` in Regular Functions

```js
function show() {
  console.log(this);
}

show();
```

In strict mode → `undefined`
In browser → `window`

---

## 🔹 `this` in Arrow Functions

Arrow functions do NOT have their own `this`.

```js
class Person {
  constructor(name) {
    this.name = name;
  }

  greet = () => {
    console.log(this.name);
  }
}
```

Arrow function inherits `this` from surrounding scope.

---

## 🔹 Losing `this` Context

```js
const greet = p1.greet;
greet(); // undefined or error
```

Because `this` is lost.

Fix with `.bind()`:

```js
const greet = p1.greet.bind(p1);
```

---

# 🔷 3️⃣ Prototypes (Core of JS OOP)

---

## 🔹 What is a Prototype?

Every JavaScript object has a hidden property:

```
[[Prototype]]
```

It points to another object.

---

## 🔹 Prototype Chain

```js
let arr = [];
```

Prototype chain:

```
arr → Array.prototype → Object.prototype → null
```

That’s how methods like `map()` work.

---

## 🔹 Example with Constructor Function

```js
function Person(name) {
  this.name = name;
}

Person.prototype.greet = function() {
  console.log("Hello " + this.name);
};

const p1 = new Person("John");
p1.greet();
```

Here:

* `greet()` is stored in prototype
* Shared by all instances

---

## 🔹 Prototype Lookup Process

When you call:

```js
p1.greet();
```

JS checks:

1. Does p1 have greet? ❌
2. Check Person.prototype? ✅
3. If not found → go up chain

This is called **prototype chaining**.

---

## 🔹 ES6 Classes Use Prototypes

```js
class Person {
  greet() {}
}
```

Is internally:

```js
Person.prototype.greet = function() {}
```

---

# 🔷 4️⃣ Inheritance

---

## 🔹 What is Inheritance?

One class can reuse properties and methods of another.

---

## 🔹 Using `extends`

```js
class Animal {
  speak() {
    console.log("Animal sound");
  }
}

class Dog extends Animal {
  bark() {
    console.log("Woof!");
  }
}

const d = new Dog();
d.speak(); // inherited
d.bark();
```

---

## 🔹 What Happens Internally?

`Dog.prototype` inherits from `Animal.prototype`.

Prototype chain becomes:

```
d → Dog.prototype → Animal.prototype → Object.prototype
```

---

# 🔷 5️⃣ The `super` Keyword

---

## 🔹 What is `super`?

Used to:

* Call parent constructor
* Call parent methods

---

## 🔹 Calling Parent Constructor

```js
class Animal {
  constructor(name) {
    this.name = name;
  }
}

class Dog extends Animal {
  constructor(name, breed) {
    super(name); // MUST call first
    this.breed = breed;
  }
}
```

Important:

> You must call `super()` before using `this`.

---

## 🔹 Calling Parent Method

```js
class Animal {
  speak() {
    console.log("Animal sound");
  }
}

class Dog extends Animal {
  speak() {
    super.speak();
    console.log("Woof!");
  }
}
```

Output:

```
Animal sound
Woof!
```

---

# 🔷 Full Example Combining Everything

```js
class Vehicle {
  constructor(brand) {
    this.brand = brand;
  }

  start() {
    console.log(`${this.brand} starting...`);
  }
}

class Car extends Vehicle {
  constructor(brand, model) {
    super(brand);
    this.model = model;
  }

  start() {
    super.start();
    console.log(`${this.model} ready to go!`);
  }
}

const myCar = new Car("Toyota", "Corolla");
myCar.start();
```

---

# 🔷 OOP Flow Diagram

```
Object
   ↑
Vehicle
   ↑
Car
   ↑
myCar
```

---

# 🔷 Important Interview Points

### Difference Between Class & Prototype?

Class is syntax sugar. Internally prototype-based.

---

### Why `super()` required?

Because child constructor must initialize parent part.

---

### How does `this` behave?

Depends on:

* How function is called
* Arrow vs normal function
* Bind/call/apply

---

### Memory Efficiency

Methods in prototype are shared.
Properties in constructor are per instance.

---

# 🔷 Common Mistakes

❌ Forgetting `new`
❌ Not calling `super()`
❌ Losing `this` context
❌ Confusing arrow function behavior

---

# 🔷 Final Summary

| Concept     | Meaning                  |
| ----------- | ------------------------ |
| Class       | Blueprint for objects    |
| Constructor | Initializes object       |
| Prototype   | Inheritance mechanism    |
| this        | Refers to calling object |
| extends     | Enables inheritance      |
| super       | Access parent class      |

---

Absolutely! Let’s dive **deeply into Prototypes and Prototype Chains in JavaScript**, which is **key to understanding object inheritance**. I’ll explain everything clearly with examples and diagrams.

---

# 🔹 1️⃣ What is a Prototype?

In JavaScript:

> **Every object has a hidden property called `[[Prototype]]`**
> which points to another object from which it can inherit properties and methods.

* This is the foundation of **JavaScript inheritance**.
* Methods like `.map()` and `.toString()` exist in **prototypes**, not in the objects themselves.

---

# 🔹 2️⃣ Prototype in Action

```js id="proto1"
const person = {
  name: "John",
  greet() {
    console.log("Hello " + this.name);
  }
};

person.greet(); // Hello John
```

Internally:

```id="proto2"
person → Object.prototype → null
```

`Object.prototype` contains standard methods like `toString()`, `hasOwnProperty()`.

---

# 🔹 3️⃣ Accessing Prototype

You can access the prototype using:

```js id="proto3"
// __proto__ (older)
console.log(person.__proto__);

// Object.getPrototypeOf()
console.log(Object.getPrototypeOf(person));
```

---

# 🔹 4️⃣ Prototype Chain

When you access a property:

```js id="proto4"
person.toString();
```

JS checks:

1. Does `person` have `toString()`? ❌
2. Check `person.__proto__` (Object.prototype) ✅ → found

This lookup process is called the **prototype chain**.

---

## Diagram of Prototype Chain

```text
myObj → MyConstructor.prototype → Object.prototype → null
```

* `myObj` → instance object
* `MyConstructor.prototype` → shared methods
* `Object.prototype` → default JS object methods

---

# 🔹 5️⃣ Constructor Function & Prototype

```js id="proto5"
function Person(name) {
  this.name = name;
}

Person.prototype.greet = function() {
  console.log("Hi " + this.name);
};

const p1 = new Person("Alice");
p1.greet(); // Hi Alice
```

* `greet()` is **not inside p1**.
* It lives in **Person.prototype**, shared by all instances → memory efficient.

```id="proto6"
p1.hasOwnProperty('greet'); // false
p1.__proto__ === Person.prototype; // true
```

---

# 🔹 6️⃣ Adding Methods Later

You can **dynamically add methods** to the prototype:

```js id="proto7"
Person.prototype.sayBye = function() {
  console.log("Bye " + this.name);
};

p1.sayBye(); // Bye Alice
```

All instances of Person automatically get it.

---

# 🔹 7️⃣ Inheritance via Prototype

Instead of `class` syntax, you can do **prototype-based inheritance**:

```js id="proto8"
function Animal(name) {
  this.name = name;
}

Animal.prototype.speak = function() {
  console.log(this.name + " makes a sound");
};

function Dog(name, breed) {
  Animal.call(this, name); // inherit properties
  this.breed = breed;
}

// Inherit methods
Dog.prototype = Object.create(Animal.prototype);
Dog.prototype.constructor = Dog;

Dog.prototype.bark = function() {
  console.log(this.name + " barks");
};

const dog = new Dog("Max", "Beagle");
dog.speak(); // Max makes a sound
dog.bark();  // Max barks
```

---

### Prototype Chain Diagram for Above:

```text
dog → Dog.prototype → Animal.prototype → Object.prototype → null
```

* JS checks **dog → Dog.prototype → Animal.prototype → Object.prototype** when accessing a property.

---

# 🔹 8️⃣ Key Points about Prototype Chain

1. All objects inherit from `Object.prototype` unless explicitly null.
2. Prototype chain ends with `null`.
3. Property/method lookup goes **up the chain**.
4. If two objects have the same method name, the **closest prototype is used**.

---

# 🔹 9️⃣ `hasOwnProperty()` vs Prototype

```js id="proto9"
console.log(p1.hasOwnProperty('name')); // true
console.log(p1.hasOwnProperty('greet')); // false, it's in prototype
```

* **Own properties** → created directly in object.
* **Inherited properties** → exist in prototype chain.

---

# 🔹 10️⃣ `Object.create()`

Creates a new object with a specified prototype.

```js id="proto10"
const animal = {
  speak() { console.log("Animal sound"); }
};

const dog = Object.create(animal);
dog.name = "Rex";
dog.speak(); // Animal sound
```

* `dog` doesn’t have `speak()` → prototype lookup finds it in `animal`.

---

# 🔹 11️⃣ Prototype in ES6 Classes

Classes use **prototype internally**:

```js id="proto11"
class Person {
  constructor(name) {
    this.name = name;
  }

  greet() {
    console.log("Hi " + this.name);
  }
}

const p = new Person("Alice");
console.log(p.__proto__ === Person.prototype); // true
```

* Methods defined in class → stored in prototype.
* Each instance has only **own properties**, not methods.

---

# 🔹 12️⃣ Real-World Analogy

Think of prototypes like **“inheritance folder”**:

* Object = your personal file folder
* Prototype = shared office folder
* Lookup goes from personal folder → shared folder → general company folder

---

# 🔹 13️⃣ Summary

* **Prototype** = object from which another object inherits properties
* **Prototype chain** = sequence of objects followed during property lookup
* **Constructor function** + `.prototype` → classic inheritance
* **ES6 class** → syntactic sugar over prototypes
* **`Object.create()`** → explicitly set prototype

---

Absolutely! Let’s dive deep into **Functional Programming (FP) in JavaScript**, covering **pure functions, immutability, and the core functional array methods: map, filter, reduce** with full explanations and examples.

---

# 🔹 1️⃣ What is Functional Programming?

Functional Programming (FP) is a programming paradigm that emphasizes:

* ✅ Functions as first-class citizens (functions can be passed, returned, stored)
* ✅ Immutability (data is not modified)
* ✅ Pure functions (no side effects, same output for same input)
* ✅ Function composition (combining simple functions into complex ones)

FP helps write **predictable, testable, and maintainable code**.

---

# 🔹 2️⃣ Pure Functions

### 📌 Definition:

A **pure function**:

1. Returns the same result for the same inputs
2. Does **not modify external state** (no side effects)

---

### ✅ Example of a Pure Function:

```js
function add(a, b) {
  return a + b;
}

console.log(add(2, 3)); // 5
console.log(add(2, 3)); // 5, always same output
```

---

### ❌ Example of an Impure Function:

```js
let total = 0;

function addToTotal(x) {
  total += x; // modifies external state
  return total;
}

addToTotal(5); // 5
addToTotal(3); // 8, different output for same input
```

> Impure functions are **harder to test** and debug.

---

# 🔹 3️⃣ Immutability

In FP, we **never modify existing data**.
Instead, we create **new copies**.

---

### ❌ Mutating Array Example:

```js
let arr = [1, 2, 3];
arr.push(4); // modifies original
console.log(arr); // [1,2,3,4]
```

---

### ✅ Immutable Array Example:

```js
let arr = [1, 2, 3];
let newArr = [...arr, 4]; // create new array
console.log(arr);    // [1,2,3]
console.log(newArr); // [1,2,3,4]
```

* Spread operator `...` is commonly used to maintain immutability.

---

# 🔹 4️⃣ First-Class Functions

In JavaScript, **functions are first-class citizens**:

* Can be stored in variables
* Can be passed as arguments
* Can be returned from functions

```js
const greet = function(name) {
  return `Hello ${name}`;
};

function sayHi(fn) {
  console.log(fn("Alice"));
}

sayHi(greet); // Hello Alice
```

---

# 🔹 5️⃣ Higher-Order Functions (HOF)

A **higher-order function**:

* Takes a function as argument
* Or returns a function

Example:

```js
function operate(a, b, operation) {
  return operation(a, b);
}

function add(x, y) { return x + y; }
function multiply(x, y) { return x * y; }

console.log(operate(5, 3, add));      // 8
console.log(operate(5, 3, multiply)); // 15
```

---

# 🔹 6️⃣ Functional Array Methods

FP shines with **immutable, declarative array operations**:

---

## 6.1 `map()`

Transforms every element in the array **without mutating**.

```js
const arr = [1, 2, 3];
const doubled = arr.map(x => x * 2);

console.log(arr);     // [1, 2, 3]  (original unchanged)
console.log(doubled); // [2, 4, 6]
```

* Returns a **new array**
* Pure, predictable function usage

---

## 6.2 `filter()`

Selects elements that satisfy a condition.

```js
const numbers = [1, 2, 3, 4, 5];
const even = numbers.filter(n => n % 2 === 0);

console.log(numbers); // [1,2,3,4,5]
console.log(even);    // [2,4]
```

* Also returns **new array**
* Original array untouched

---

## 6.3 `reduce()`

Combines all elements to a single value.

```js
const numbers = [1, 2, 3, 4];
const sum = numbers.reduce((acc, curr) => acc + curr, 0);

console.log(sum); // 10
```

* `acc` = accumulator (stores result)
* `curr` = current element
* `0` = initial value

---

### Reduce Example: Multiplying All Numbers

```js
const product = [2, 3, 4].reduce((acc, curr) => acc * curr, 1);
console.log(product); // 24
```

---

# 🔹 7️⃣ Function Composition

Combine multiple small functions into one:

```js
const double = x => x * 2;
const square = x => x * x;

const doubleThenSquare = x => square(double(x));

console.log(doubleThenSquare(3)); // 36
```

* FP encourages **small reusable functions**.

---

# 🔹 8️⃣ Pure FP Example: Chaining Map/Filter/Reduce

```js
const numbers = [1, 2, 3, 4, 5];

const result = numbers
  .filter(n => n % 2 === 1)  // keep odd numbers
  .map(n => n * n)           // square them
  .reduce((sum, n) => sum + n, 0); // sum squares

console.log(result); // 35 (1^2 + 3^2 + 5^2)
```

* **Readable**, declarative, immutable
* Avoids loops and mutations

---

# 🔹 9️⃣ FP vs Imperative Example

**Imperative (mutation-heavy)**

```js
let arr = [1,2,3,4,5];
let result = 0;

for(let i=0; i<arr.length; i++) {
  if(arr[i] % 2 === 1) {
    result += arr[i] ** 2;
  }
}

console.log(result); // 35
```

**Functional (declarative, pure)**

```js
const result = [1,2,3,4,5]
  .filter(n => n % 2 === 1)
  .map(n => n ** 2)
  .reduce((sum, n) => sum + n, 0);

console.log(result); // 35
```

> FP is **cleaner, safer, and easier to test**.

---

# 🔹 10️⃣ Key Principles of Functional Programming in JS

| Principle              | Meaning                         | Example              |
| ---------------------- | ------------------------------- | -------------------- |
| Pure Functions         | No side effects, same output    | `x => x*2`           |
| Immutability           | Don’t modify data               | `[...arr, 5]`        |
| First-Class Functions  | Functions can be passed/stored  | `const f = () => {}` |
| Higher-Order Functions | Functions take/return functions | `arr.map(fn)`        |
| Function Composition   | Combine functions               | `f(g(x))`            |

---

# 🔹 11️⃣ When to Use Functional Programming

* Transforming data (`map`, `filter`, `reduce`)
* State management (React/Redux)
* Predictable and testable code
* Avoiding side effects in large apps

---

✅ **Summary**:

Functional Programming in JavaScript focuses on:

* **Pure functions** → predictable output
* **Immutability** → do not modify original data
* **Higher-order functions** → pass/return functions
* **Array methods** → map, filter, reduce
* **Composition** → building complex behavior from simple functions

---

Absolutely! Let’s dive **deeply into Function Composition** in JavaScript, which is a **core concept in Functional Programming**. I’ll explain it step by step with examples, diagrams, and best practices.

---

# 🔹 1️⃣ What is Function Composition?

> **Function composition** is the process of **combining small, reusable functions** to build **larger, more complex logic**.

Instead of writing one big function, we write **many small functions** and “pipe” data through them.

---

## ✅ Example Conceptually

```js id="composition1"
// f(x) = x + 2
// g(x) = x * 3
// compose(f, g)(x) = f(g(x))
```

* Input → g → f → Output

For `x = 5`:

```js id="composition2"
g(5) = 5*3 = 15
f(15) = 15+2 = 17
```

---

# 🔹 2️⃣ Manual Function Composition

```js id="composition3"
const double = x => x * 2;
const square = x => x * x;

const doubleThenSquare = x => square(double(x));

console.log(doubleThenSquare(3)); // 36
```

* Step 1: `double(3)` → 6
* Step 2: `square(6)` → 36

> This is **manual composition** using nested calls.

---

# 🔹 3️⃣ Generic Compose Function

We can make a **helper function** to compose multiple functions:

```js id="composition4"
const compose = (...fns) => x =>
  fns.reduceRight((acc, fn) => fn(acc), x);

// Example
const add2 = x => x + 2;
const multiply3 = x => x * 3;

const composed = compose(add2, multiply3);
console.log(composed(5)); // 17 (multiply3 first, then add2)
```

* `reduceRight` → functions are applied **right to left**
* Clean, reusable, declarative

---

# 🔹 4️⃣ Pipe Function (Left-to-Right Composition)

Sometimes, **left-to-right** is more readable:

```js id="composition5"
const pipe = (...fns) => x =>
  fns.reduce((acc, fn) => fn(acc), x);

const composed = pipe(multiply3, add2);
console.log(composed(5)); // 17
```

* `pipe` is commonly used in FP libraries like **Ramda** or **Lodash/fp**
* Mirrors **data flow** → easier to read

---

# 🔹 5️⃣ Composing Array Transformations

FP shines with **map/filter/reduce** + composition.

```js id="composition6"
const numbers = [1, 2, 3, 4, 5];

// small reusable functions
const square = x => x * x;
const isOdd = x => x % 2 === 1;

// step 1: filter odd numbers
const filterOdd = arr => arr.filter(isOdd);

// step 2: square numbers
const mapSquare = arr => arr.map(square);

// step 3: sum all
const sum = arr => arr.reduce((acc, n) => acc + n, 0);

// compose all
const pipeline = pipe(filterOdd, mapSquare, sum);

console.log(pipeline(numbers)); // 35
```

* **Small pure functions**
* **Immutable**
* **Readable, testable**

---

# 🔹 6️⃣ Benefits of Function Composition

1. **Reusability** – small functions can be reused in multiple pipelines
2. **Testable** – each function can be unit tested independently
3. **Predictable** – pure functions → same input = same output
4. **Readable** – the pipeline reads like a sequence of operations
5. **Declarative** – describes **what** happens, not **how**

---

# 🔹 7️⃣ Compose vs Pipe

| Concept | Direction    | Example                        |
| ------- | ------------ | ------------------------------ |
| Compose | Right → Left | `compose(f, g)(x)` → `f(g(x))` |
| Pipe    | Left → Right | `pipe(f, g)(x)` → `g(f(x))`    |

* **Compose** is mathematically traditional
* **Pipe** is more readable in JS

---

# 🔹 8️⃣ Real-World Example: String Processing

```js id="composition7"
const trim = str => str.trim();
const toLower = str => str.toLowerCase();
const removeExclamation = str => str.replace(/!/g, "");

const cleanString = pipe(trim, toLower, removeExclamation);

console.log(cleanString("  HELLO WORLD!  ")); // "hello world"
```

* Each function does **one thing** → easy to understand
* Avoids **nested calls** → readable and maintainable

---

# 🔹 9️⃣ Key Principles for Composable Functions

1. **Pure** – No side effects
2. **Single Responsibility** – Each function does **one thing**
3. **Immutable** – Never mutate input
4. **Return a value** – Don’t just `console.log`

---

# 🔹 10️⃣ Advanced: Composing Async Functions (Promises)

```js id="composition8"
const fetchData = () => Promise.resolve(5);
const multiply2 = x => x * 2;
const add3 = x => x + 3;

fetchData()
  .then(multiply2)
  .then(add3)
  .then(console.log); // 13
```

* Functional pipelines work **with async code** using `then()`
* Libraries like **RxJS** extend this for reactive streams.

---

# 🔹 11️⃣ Summary

Function Composition allows us to:

* Build **complex behavior from small, reusable functions**
* Avoid **nested code** and **side effects**
* Make **readable, maintainable, testable** programs
* Combine with **map/filter/reduce** for powerful pipelines

---




