# 3.4 Higher-Order Functions and Callbacks

## First-class functions
- Functions are values in JavaScript: you can store them in variables, pass them as arguments, return them from other functions, and store them in data structures.

```js
const f = function(x) { return x * 2; };
const arr = [f, x => x + 1];
```

## Higher-order function (HOF)
- A HOF either takes one or more functions as arguments, returns a function, or both.
- Examples: `map`, `filter`, `reduce` (built-ins) and factories like `once()` or `memoize()`.

## Built-in HOFs
- `Array.prototype.map(fn)` — returns new array with `fn` applied to each item.
- `filter(fn)` — returns items where `fn(item)` is truthy.
- `reduce(fn, init)` — folds array to single value.
- `forEach(fn)` — runs `fn` for side effects.
- `sort(fn)` — sorts in-place with comparator.
- `find(fn)` — returns first matching item or `undefined`.
- `some(fn)` / `every(fn)` — boolean checks across elements.

Examples:

```js
const nums = [1,2,3,4];
const doubled = nums.map(n => n * 2);
const even = nums.filter(n => n % 2 === 0);
const sum = nums.reduce((acc, n) => acc + n, 0);
nums.forEach(n => console.log(n));
```

## Callback pattern
- A callback is a function passed to be executed later (event handlers, timers, async completion, or HOFs).

Examples:

```js
// event callback (browser)
button.addEventListener('click', e => console.log('clicked'));

// timer callback
setTimeout(() => console.log('later'), 1000);

// async callback (Node-style)
fs.readFile('file', (err, data) => { if (err) throw err; console.log(data); });
```

### Callback hell
- Deeply nested callbacks become hard to read and reason about.

```js
doA(arg, function(aErr, aRes) {
  if (aErr) return cb(aErr);
  doB(aRes, function(bErr, bRes) {
    if (bErr) return cb(bErr);
    doC(bRes, function(cErr, cRes) {
      // deeply nested
    });
  });
});
```

Solution: use Promises and `async/await` to flatten control flow.

```js
// Promise-based
async function run() {
  const a = await doA(arg);
  const b = await doB(a);
  const c = await doC(b);
}
```

## Custom HOFs / utility wrappers

### `once(fn)` — run a function only once

```js
function once(fn) {
  let called = false;
  let result;
  return function (...args) {
    if (!called) {
      called = true;
      result = fn.apply(this, args);
    }
    return result;
  };
}

const init = once(() => { console.log('init'); return 42; });
init(); // 'init'
init(); // no-op, returns cached 42
```

### `memoize(fn)` — cache results for pure functions

```js
function memoize(fn) {
  const cache = new Map();
  return function (arg) {
    if (cache.has(arg)) return cache.get(arg);
    const res = fn(arg);
    cache.set(arg, res);
    return res;
  };
}

const fib = memoize(n => n < 2 ? n : fib(n - 1) + fib(n - 2));
console.log(fib(20));
```

Note: choose cache key carefully for functions with multiple or non-primitive args.

### `debounce(fn, wait)` — delay until activity stops

```js
function debounce(fn, wait) {
  let t;
  return function (...args) {
    clearTimeout(t);
    t = setTimeout(() => fn.apply(this, args), wait);
  };
}

const onResize = debounce(() => { console.log('resized'); }, 200);
window.addEventListener('resize', onResize);
```

### `throttle(fn, limit)` — ensure at most one call per interval

```js
function throttle(fn, limit) {
  let last = 0;
  let pending;
  return function (...args) {
    const now = Date.now();
    const context = this;
    if (now - last >= limit) {
      last = now;
      fn.apply(context, args);
    } else if (!pending) {
      pending = setTimeout(() => {
        last = Date.now();
        pending = null;
        fn.apply(context, args);
      }, limit - (now - last));
    }
  };
}

const onScroll = throttle(() => { console.log('scrolled'); }, 100);
window.addEventListener('scroll', onScroll);
```

## Best practices
- Prefer higher-order built-ins (`map`, `filter`, `reduce`) for clearer, declarative code.
- Use `async/await` or Promises instead of deeply nested callbacks.
- Keep callbacks small and pure where possible; avoid side effects when composing functions.
- Be careful with `this` in callbacks — bind or use arrow functions when needed.
- For utilities like `memoize`, `debounce`, and `throttle`, consider edge cases: arguments identity, cancellation, leading/trailing options.

---
End of `3.4 Higher-Order Functions and Callbacks`.
