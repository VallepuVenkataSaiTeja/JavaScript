# 3.6 Error Handling

## try / catch / finally
- Syntax:

```js
try {
  // code that may throw
} catch (err) {
  // handle error
} finally {
  // cleanup — always runs (even after return)
}
```

Examples:

```js
function read(json) {
  try {
    const value = JSON.parse(json);
    return value;
  } catch (err) {
    console.error('invalid json', err.message);
    throw err; // rethrow if we can't recover
  } finally {
    // cleanup or logging; always executes
    console.log('attempted parse');
  }
}
```

Note: `finally` runs even when `try`/`catch` returns.

## throw
- Use `throw` to raise errors: `throw new Error('message')` is preferred.
- JavaScript allows throwing any value (string, object), but `Error` instances provide `message` and `stack` which aid debugging.

```js
throw new Error('Something went wrong');
// avoid: throw 'oops';
```

## Common Error types
- `Error` — generic
- `SyntaxError` — parsing/JSON/`eval` syntax
- `TypeError` — invalid type operations
- `ReferenceError` — accessing undefined variables
- `RangeError` — numeric range issues
- `URIError` — encoding/decoding URI functions
- `AggregateError` — groups multiple errors (e.g., Promise.any)

Examples:

```js
try { JSON.parse('bad'); } catch (e) { console.log(e instanceof SyntaxError); }
const agg = new AggregateError([new Error('a'), new Error('b')], 'multiple');
console.log(agg.errors); // [Error('a'), Error('b')]
```

## Error properties
- `error.message` — human-friendly message
- `error.name` — constructor name (e.g., 'TypeError')
- `error.stack` — stack trace string (widely supported; use for debugging/logging)

```js
try { null.f(); } catch (err) {
  console.log(err.name); // 'TypeError'
  console.log(err.message);
  console.log(err.stack);
}
```

## Custom errors
- Create domain-specific errors by extending `Error`.
- Preserve stack trace and set `name`.
- ES2022 also supports the `cause` option for error chaining: `new Error('msg', { cause: inner })`.

```js
class MyError extends Error {
  constructor(message, options) {
    super(message, options);
    this.name = 'MyError';
    if (Error.captureStackTrace) Error.captureStackTrace(this, MyError);
  }
}

try {
  try { throw new Error('inner'); } catch (inner) {
    throw new MyError('outer', { cause: inner });
  }
} catch (e) {
  console.log(e.name); // 'MyError'
  console.log(e.cause); // inner Error (when supported)
}
```

## AggregateError
- Used to group multiple errors. Common when multiple async tasks fail.

```js
const errors = [new Error('x'), new Error('y')];
throw new AggregateError(errors, 'multiple failures');
```

## Async errors (Promises / async/await)
- With `async/await`, use `try/catch`:

```js
async function run() {
  try {
    const data = await fetchJSON();
    return data;
  } catch (err) {
    // handle or rethrow
    throw err;
  }
}
```

- For Promises directly, use `.catch()`:

```js
fetchJSON().then(data => {}).catch(err => console.error(err));
```

- Unhandled promise rejections should be avoided; attach `.catch()` or use top-level handlers in environments where available.

## Rethrowing and selective handling
- If you cannot fully handle an error, rethrow it to allow higher-level code to handle it.
- You can inspect error type or properties before deciding.

```js
try {
  doSomething();
} catch (err) {
  if (err instanceof KnownError) {
    // recover
  } else {
    throw err; // rethrow unknown errors
  }
}
```

## Best practices
- Throw `Error` instances (or subclasses) rather than raw values.
- Catch only what you can handle; avoid empty `catch {}` blocks that silently swallow errors.
- Use `finally` to release resources, clear timers, or close files/streams.
- Preserve original errors when wrapping (use `cause` or attach original as property) so stacks remain useful.
- Prefer explicit error checks over using exceptions for control flow where possible.
- When logging, include `error.stack` to aid debugging, but avoid leaking sensitive details to end-users.
- In async code, always attach error handlers (`.catch` or `try/catch`) to avoid unhandled rejections.
- Use error types to distinguish recoverable vs non-recoverable errors.

## Logging and monitoring
- Centralize error logging and add contextual metadata (request id, user id).
- Surface friendly error messages to users, but log full details (stack, inputs) for operators.

## Quick checklist
- Use `try/catch/finally` around risky code.
- Use `throw new Error(...)` or custom error classes.
- Handle expected errors; rethrow unexpected ones.
- Clean up in `finally`.
- For async, use `await`+`try/catch` or `.catch()`.

---
End of `3.6 Error Handling`.
