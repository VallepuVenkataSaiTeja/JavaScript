# 3.2 Execution Context and `this`

## Summary
- `this` is determined by *how* a function is called (the call site), not where it was defined.
- There are several binding rules: Default, Implicit, Explicit, and `new` binding. Arrow functions inherit `this` lexically.

## Default binding
- Standalone function call (non-method): `this` is the global object (in non-strict mode) or `undefined` (in strict mode).

Example (non-strict):

```js
function fn() {
  return this; // global object (window in browsers)
}
console.log(fn());
```

Example (strict):

```js
'use strict';
function fn2() {
  return this; // undefined
}
console.log(fn2());
```

## Implicit binding (method call)
- When you call `obj.method()`, `this` inside `method` is `obj` (the object to the left of the dot).

```js
const o = {
  value: 42,
  get() { return this.value; }
};
console.log(o.get()); // 42  (this -> o)
```

Lost implicit binding (common pitfall): extracting a method loses its object binding:

```js
const f = o.get;
console.log(f()); // undefined or error depending on strict mode
```

Fixes: bind the function or call via the object: `o.get()` or `f = o.get.bind(o)`.

## Explicit binding (`call`, `apply`, `bind`)
- You can explicitly set `this` using `fn.call(thisArg, ...)`, `fn.apply(thisArg, argsArray)`, or `fn.bind(thisArg)`.
- `bind` returns a new function with the bound `this` (and optionally leading args).

```js
function show() { return this.name; }
const x = { name: 'X' };
console.log(show.call(x)); // 'X'

const bound = show.bind(x);
console.log(bound()); // 'X'
```

## `new` binding (constructor call)
- Calling a function with `new` creates a fresh object and sets `this` to that object. The constructor typically initializes properties on `this` and implicitly returns `this` (unless it returns an object explicitly).

```js
function Person(name) { this.name = name; }
const p = new Person('Alice');
console.log(p.name); // 'Alice'
```

## Precedence of bindings
- When multiple rules could apply, the precedence is:
  1. `new` binding (highest)
  2. Explicit binding (`call`/`apply`/`bind`)
  3. Implicit binding (`obj.method()`)
  4. Default binding (lowest)

Example showing `new` vs `bind`:

```js
function Thing(name) { this.name = name; }
const Bound = Thing.bind({ name: 'X' });
const t = new Bound('Bob');
console.log(t.name); // 'Bob' — `new` wins; the bound `this` is ignored for constructor calls
```

Example showing explicit binding overriding implicit:

```js
const a = { name: 'A', show() { return this.name; } };
const b = { name: 'B' };
console.log(a.show.call(b)); // 'B'  (explicit call overrides implicit)
```

## Arrow functions and lexical `this`
- Arrow functions do not have their own `this`. Instead they inherit `this` from the surrounding (lexical) scope at the time they are defined.
- Because of lexical `this`, `call`/`apply`/`bind` cannot change an arrow function's `this`.

Example:

```js
const obj = {
  id: 1,
  regular() { return this.id; },
  arrow: () => this && this.id
};
console.log(obj.regular()); // 1
console.log(obj.arrow());   // undefined (arrow `this` is outer scope — here likely global/undefined)
```

Practical use of arrow lexical `this` (common pattern):

```js
function Timer() {
  this.seconds = 0;
  setInterval(() => { // arrow keeps `this` from Timer
    this.seconds++;
  }, 1000);
}
const t = new Timer();
```

## Arrow pitfalls
- Do NOT use arrow functions as object methods when you rely on `this` being the object.
- Arrow functions cannot be used as constructors (`new` will throw).
- Arrow functions do not have their own `arguments` object.

## Additional gotchas and recommendations
- When passing methods as callbacks, explicitly bind or wrap to preserve `this`:

```js
class Counter {
  constructor() { this.count = 0; }
  inc() { this.count++; }
}

const c = new Counter();
setTimeout(c.inc, 100); // wrong — `this` lost
setTimeout(c.inc.bind(c), 100); // correct
```

- Prefer `const self = this` or arrow functions when you need lexical `this` inside nested functions (or simply use arrow functions in modern code).

- Use strict mode if you want default binding to be `undefined` rather than the global object; this helps catch accidental global access.

## Quick reference
- Default: standalone call → global / `undefined` (strict)
- Implicit: `obj.method()` → `obj`
- Explicit: `fn.call/apply/bind(thisArg)` → `thisArg`
- `new`: `new Fn()` → newly created object
- Arrow: lexical `this` (inherited), cannot be overridden

---
End of `3.2 Execution Context and this`.
