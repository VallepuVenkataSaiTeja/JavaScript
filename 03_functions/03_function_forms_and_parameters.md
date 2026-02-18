# 3.3 Function Forms and Parameters

## Arrow functions
- Syntax: concise body: `(x) => x * 2` (implicit return), block body: `(x, y) => { return x + y; }`.
- Concise body returns the expression value implicitly; block body requires an explicit `return`.
- Arrow functions have lexical `this`, no `arguments`, and cannot be used as constructors.

Examples:

```js
const dbl = x => x * 2;
const add = (a, b) => { return a + b; };

console.log(dbl(3)); // 6
console.log(add(2, 4)); // 6
```

Gotchas:
- Parentheses are required for zero or multiple params: `() => 1`, `(a, b) => a + b`.
- Returning an object literal requires parentheses: `() => ({ a: 1 })`.

## Default parameters
- Provide defaults in the signature: `function fn(a = 1, b = 2) {}`.
- Defaults are evaluated at call time; later defaults can reference earlier parameters.

```js
function greet(name = 'Guest', suffix = name === 'Guest' ? '' : '!') {
  return `Hello ${name}${suffix}`;
}

console.log(greet()); // 'Hello Guest'
console.log(greet('Alice')); // 'Hello Alice!'
```

Note: default values create their own scope for evaluating default expressions.

## Rest parameters
- Syntax: `function fn(...args) {}`. `args` is a real Array containing remaining arguments.
- Must be the last parameter in the parameter list.

```js
function sum(...nums) {
  return nums.reduce((s, n) => s + n, 0);
}

console.log(sum(1,2,3)); // 6
```

Rest vs `arguments`:
- Rest is a real Array; `arguments` is array-like.

## `arguments` object (non-arrow)
- Every non-arrow function has an `arguments` object (array-like) with the passed values and `.length`.
- Not available in arrow functions.

```js
function f() {
  console.log(arguments[0]);
  console.log(arguments.length);
  const arr = Array.from(arguments);
  console.log(arr);
}

f('a', 'b'); // 'a', 2, ['a','b']
```

To convert: `Array.from(arguments)` or `[...arguments]` (spread) inside non-arrow functions.

## Function `.length`
- The `.length` property of a function equals the number of parameters before the first one with a default value or the rest parameter.

```js
function a(x, y) {}
function b(x = 1, y) {}
function c(x, ...rest) {}

console.log(a.length); // 2
console.log(b.length); // 0 (first param has default)
console.log(c.length); // 1 (rest doesn't count)
```

## Function `.name`
- Functions infer a `.name` from their declaration or assignment, useful for debugging and stack traces.

```js
const f = function() {};
const g = function named() {};
function h() {}

console.log(f.name); // 'f'
console.log(g.name); // 'named'
console.log(h.name); // 'h'
```

Notes and best practices
- Prefer rest parameters and default parameters over `arguments` for clarity and better semantics.
- Use arrow functions for short callbacks and when you want lexical `this`.
- Avoid mixing `arguments` and rest parameters; rest is the modern approach.
- Remember `.length` is helpful when writing utilities that introspect functions.

---
End of `3.3 Function Forms and Parameters`.
