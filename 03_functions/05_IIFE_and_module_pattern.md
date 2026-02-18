# 3.5 IIFE and Module Pattern

## IIFE (Immediately Invoked Function Expression)
- Syntax: `(function() { /* code */ })()` — define and immediately execute a function to create a private scope.
- Purpose: avoid polluting the global scope and create private variables before block scoping (`let`/`const`) and ES modules existed.

Example:

```js
(function () {
  const secret = 'shh';
  console.log('IIFE ran');
})();

// `secret` is not visible here
```

You can also pass injected values (globals, dependencies) to keep the internals decoupled:

```js
(function (window, document) {
  // use window/document without referencing globals directly
})(this, this.document);
```

## Module pattern (IIFE returning an API)
- The module pattern uses an IIFE that returns an object exposing only the public API while keeping internal state private.

```js
const Counter = (function () {
  let count = 0; // private
  function inc() { count += 1; return count; }
  function get() { return count; }
  return { inc, get }; // public API
})();

console.log(Counter.get()); // 0
Counter.inc();
console.log(Counter.get()); // 1
```

Benefits:
- Encapsulation: internal variables are inaccessible except via the returned API.
- Clear public surface: only returned properties are part of the module's interface.

## Revealing module pattern
- A variant where you define internal functions/variables and explicitly map them to the returned object, improving clarity about which internals are exposed.

```js
const MyModule = (function () {
  let _value = 0;
  function _privateInc() { _value++; }
  function publicInc() { _privateInc(); }
  function publicGet() { return _value; }
  return {
    inc: publicInc,
    get: publicGet
  };
})();

MyModule.inc();
console.log(MyModule.get());
```

## Historical purpose and portability
- Before ES modules (`import`/`export`) and modern bundlers, IIFEs and the module pattern were the common way to:
  - Encapsulate code and create private state.
  - Avoid adding variables to the global object.
  - Create singletons and initialize module state immediately.

Developers also used UMD (Universal Module Definition) wrappers around IIFEs to support multiple environments (AMD, CommonJS, global).

## When to use today
- Use native ES modules for modularity and static analysis when you can (preferred).
- IIFEs are still useful for one-off initialization code, immediately-scoped logic in scripts, or when you need to isolate code without changing module config.

## Quick comparison
- IIFE/module pattern: encapsulation at runtime using closures.
- ES modules: language-level modules with static imports/exports, better tooling, and clearer semantics.

---
End of `3.5 IIFE and Module Pattern`.
