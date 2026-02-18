# 3.1 Closures

## What is a closure?
- A closure is a function that "remembers" variables from its lexical scope (the environment where it was defined), even after the outer function has finished executing.
- In other words, an inner function retains access to variables declared in its outer function.

## How closures work (conceptually)
- When a function is defined, JavaScript records a link to its surrounding lexical environment (the variables and their bindings).
- If the inner function is returned or passed outside the outer function, that environment is kept alive so the inner function can access those variables later.
- The inner function holds references to the variable *bindings*, not just copies of their values. If the binding changes, the inner function sees the latest value.

## Simple example: counter factory

```js
function makeCounter() {
  let count = 0; // private variable
  return function () {
    count += 1;
    return count;
  };
}

const c = makeCounter();
console.log(c()); // 1
console.log(c()); // 2

// `count` remains accessible to the returned function even though
// `makeCounter` has finished executing.
```

Explanation:
- `makeCounter` creates a local variable `count` and returns an inner function.
- That inner function closes over `count`, forming a closure. Calls to `c()` update that captured `count`.

## Inner function retains variable environment (demonstration)

```js
function outer() {
  let x = 10;
  return function inner() {
    return x;
  };
}

const fn = outer();
// although outer() returned, `x` still exists because `fn` references it
console.log(fn()); // 10
```

If the outer scope had multiple variables, the inner function keeps references to all variables that it uses.

## Practical uses

- Private state / data hiding (like the `count` example).
- Factory functions (create specialized functions with preserved configuration).
- Partial application / currying (pre-fill arguments via closures).
- Module pattern (returning API with private state without exposing internals).
- Event handlers and callbacks that need access to surrounding data.

### Example: factory with configuration

```js
function makeGreeter(greeting) {
  return function(name) {
    return `${greeting}, ${name}!`;
  };
}

const greetHi = makeGreeter('Hi');
console.log(greetHi('Alice')); // "Hi, Alice!"
```

### Example: partial application

```js
function multiply(a) {
  return function(b) {
    return a * b;
  };
}

const double = multiply(2);
console.log(double(5)); // 10
```

### Example: module pattern (API with private state)

```js
const Counter = (function () {
  let value = 0; // private
  return {
    inc() { value += 1; return value; },
    dec() { value -= 1; return value; },
    get() { return value; }
  };
})();

console.log(Counter.get()); // 0
Counter.inc();
console.log(Counter.get()); // 1

// `value` is inaccessible from outside the module except via the returned API.
```

## Classic mistake: `var` in loops with asynchronous callbacks

Problem:

```js
for (var i = 0; i < 3; i++) {
  setTimeout(function () {
    console.log(i);
  }, 10);
}
// prints: 3, 3, 3  (because `var i` is function-scoped; all callbacks share same `i`)
```

Why this happens:
- `var` is function-scoped; the loop doesn't create a new binding per iteration. The callbacks capture the single `i` binding, which after the loop ends is 3.

Fixes:

1) Use `let` (block-scoped, creates a fresh binding each iteration)

```js
for (let i = 0; i < 3; i++) {
  setTimeout(function () {
    console.log(i);
  }, 10);
}
// prints: 0, 1, 2
```

2) Use an IIFE to capture the value (old school)

```js
for (var i = 0; i < 3; i++) {
  (function (j) {
    setTimeout(function () {
      console.log(j);
    }, 10);
  })(i);
}
// prints: 0, 1, 2
```

3) Use `.forEach` which provides a fresh callback argument

```js
[0,1,2].forEach(function(i) {
  setTimeout(function () { console.log(i); }, 10);
});
// prints: 0, 1, 2
```

## Memory implications of closures

- Because closures keep references to their outer environment, the captured variables cannot be garbage-collected while the closure is reachable. This can lead to retaining memory longer than intended.
- If a closure accidentally captures a large object or array, that memory will remain live as long as the closure is reachable.

Example (potential leak):

```js
function createHandler() {
  const big = new Array(1_000_000).fill('*');
  return function handler() {
    // `big` is still referenced, so the large array remains in memory
    console.log('handler called');
  };
}

const h = createHandler();
// if `h` lives a long time, `big` stays in memory as well
```

Mitigations / best practices:

- Avoid capturing large data structures unnecessarily. Only keep the variables you need inside the closure.
- Null out references when no longer needed: set large variables to `null` if they must be created but can be released.

```js
function createHandler() {
  let big = new Array(1_000_000).fill('*');
  function handler() {
    console.log('handler called');
  }
  // release large memory if not needed later
  big = null;
  return handler;
}
```

- For long-lived caches or maps keyed by objects, consider `WeakMap` to allow garbage collection when keys become unreachable.
- Be mindful in long-running apps (servers, single-page apps): closures attached to DOM event listeners or timers can keep DOM or data alive—remove listeners or clear timers when no longer needed.

## Common patterns that rely on closures

- Memoization caches
- Function decorators and wrappers
- Event handler factories
- Currying / partial application

Example: memoize via closure

```js
function memoize(fn) {
  const cache = new Map();
  return function (arg) {
    if (cache.has(arg)) return cache.get(arg);
    const result = fn(arg);
    cache.set(arg, result);
    return result;
  };
}

const slow = (n) => { /* expensive */ return n * n; };
const fast = memoize(slow);

console.log(fast(10));
```

## Summary / key takeaways

- A closure = a function + the lexical environment it remembers.
- Closures enable private state, factories, partial application, and module-like encapsulation.
- Watch out for scoping gotchas with `var` in loops—prefer `let` or per-iteration bindings.
- Closures keep references alive; avoid capturing unnecessary large objects and clean up listeners/timers to prevent leaks.

---
End of `3.1 Closures`.
