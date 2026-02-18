# Complete JavaScript Roadmap — Full In-Depth (Heavy)

JavaScript only. No frameworks. No other languages. From absolute beginner to advanced.

Everything in one file: **Roadmap** · **Interview Questions with Answers** · **Practice Problems** · **Projects**

---

# PART 1 — COMPLETE ROADMAP

Every topic. Every sub-topic. Checkboxes for tracking.

---

## Phase 1: Foundations

### 1.1 What is JavaScript

**Definition and purpose**
- [ ] Definition: high-level, dynamic, general-purpose programming language
- [ ] Original purpose: created in 1995 to make web pages interactive (Brendan Eich, Netscape, ~10 days)
- [ ] Modern role: full-stack apps, mobile apps, desktop apps, tooling, embedded — not "just for browsers"

**Where JavaScript is used (ecosystem)**
- [ ] Browsers (client-side): dropdown menus, form validation, animations, dashboards
- [ ] Servers: Node.js, Deno, Bun — backend, APIs, real-time
- [ ] Mobile apps: React Native — iOS/Android with one codebase
- [ ] Desktop apps: Electron — VS Code, Slack, Discord, Notion
- [ ] Build tools: Webpack, Vite, Babel, ESLint
- [ ] Embedded / IoT: microcontrollers, smart devices (light mention)

**Core characteristics**
- [ ] Dynamic typing: types checked at runtime, not before; same variable can hold any type
- [ ] Garbage-collected: memory managed automatically; no manual allocate/free
- [ ] Multi-paradigm: procedural (step-by-step), object-oriented (objects + classes), functional (functions as values)

**JavaScript vs ECMAScript**
- [ ] ECMAScript = the specification (the blueprint / rulebook)
- [ ] JavaScript = an implementation of that spec (the house built from the blueprint)
- [ ] Multiple engines implement the same spec → code works across browsers
- [ ] "ES6", "ES2024" = editions of the ECMAScript standard
- [ ] Why this distinction matters: explains compatibility, new features, tooling

**How the language evolves**
- [ ] ECMA-262: the official spec document (syntax, semantics, built-ins)
- [ ] TC39: committee (Technical Committee 39) that proposes and standardizes features
- [ ] Proposal stages: Stage 0 (idea) → Stage 1 (proposal) → Stage 2 (draft) → Stage 3 (candidate) → Stage 4 (finished → in spec)
- [ ] Takeaway: JavaScript is actively evolving; new features every year

**Where JavaScript runs: engines and runtimes**
- [ ] **Engines** read and execute JS code:
  - [ ] V8 (Chrome, Edge, Node.js, Deno, Bun)
  - [ ] SpiderMonkey (Firefox)
  - [ ] JavaScriptCore (Safari)
- [ ] **Runtime** = engine + environment + APIs
  - [ ] Browser runtime: engine + DOM, fetch, timers, events
  - [ ] Node.js runtime: V8 + file system, network, process
- [ ] Engine executes code; runtime provides environment and capabilities
- [ ] Same JS language → different APIs per runtime (e.g. `document` in browser, `process` in Node)

**How JavaScript executes code**
- [ ] Pipeline: parsing → compilation → execution
- [ ] Parsing: read source, check syntax, build AST (Abstract Syntax Tree); syntax error = stop here
- [ ] Compilation: turn AST into bytecode/machine code; JIT (Just-In-Time) = compile during execution for speed
- [ ] Execution: run instructions; create variables, call functions, produce output
- [ ] Key: JavaScript is NOT purely interpreted; modern engines use JIT compilation

**Concurrency model**
- [ ] Single-threaded: one call stack; only one piece of code runs at a time
- [ ] Call stack: tracks currently running function; push on call, pop on return
- [ ] Event loop (intro only — deep dive in Phase 4):
  - [ ] Call stack: where code executes
  - [ ] Task queue (macrotask): setTimeout, setInterval callbacks
  - [ ] Microtask queue: Promise callbacks, queueMicrotask
  - [ ] Event loop: checks "is call stack empty?" → moves next task from queue to stack
- [ ] Single-threaded but not single-tasking: concurrency through scheduling, not parallelism

**Optional: brief history**
- [ ] Created 1995, Brendan Eich, Netscape, ~10 days
- [ ] Standardized as ECMAScript to prevent browser fragmentation
- [ ] Exploded: Node.js (2009), modern frameworks, massive ecosystem

---

### 1.2 Running Your First JavaScript

**Ways to run JavaScript**
- [ ] `<script>` tag: inline (`<script>code</script>`) and external files (`<script src="app.js"></script>`)
- [ ] Inline JS: for small tests/learning only; not for production (mixes HTML + JS)
- [ ] External files: cleaner, cacheable, reusable — the default for real apps
- [ ] Script placement: browsers parse HTML top → bottom; `<script>` in `<head>` without defer blocks page
- [ ] The classic bug: script in `<head>` accessing DOM element that doesn't exist yet → error
- [ ] Golden rule: **use `defer` for external scripts by default**
- [ ] `defer`: downloads in parallel, executes after HTML parsed, preserves script order — best default
- [ ] `async`: downloads in parallel, executes immediately when ready, order NOT guaranteed — for independent scripts (analytics, ads)
- [ ] Mental model: `defer` = safe default; `async` = special case for independent scripts

**Browser console**
- [ ] How to open: F12 / Ctrl+Shift+I (Windows/Linux), Cmd+Option+I (Mac) → Console tab
- [ ] Running snippets: type JS directly, press Enter, see result
- [ ] `console.log()` — primary way to see what the program is doing
- [ ] When confused → log it (even senior devs do this daily)
- [ ] Reading console errors: red messages tell you what went wrong, where, and sometimes why
- [ ] Errors are normal; good developers read them, great developers learn from them
- [ ] Golden habit: **"If JavaScript isn't working, open the console first"**

**First real program**
- [ ] Create `index.html` with `<script defer src="app.js"></script>`
- [ ] Create `app.js` with `console.log("My first JavaScript program!");`
- [ ] Open in browser → open console → see message
- [ ] What happened: HTML loaded → script downloaded → engine parsed and executed → output in console

**Syntax basics**
- [ ] Statements: single instructions; engine executes top → bottom
- [ ] One statement per line for readability
- [ ] Semicolons and ASI (Automatic Semicolon Insertion): engine sometimes inserts semicolons; can cause bugs (e.g. `return` on its own line)
- [ ] Beginner rule: **always write semicolons** — remove ambiguity

**Comments**
- [ ] Single-line: `// comment`
- [ ] Multi-line: `/* comment */`
- [ ] Golden rule: explain **why**, not **what** — code should be self-explanatory
- [ ] Don't overcomment; use comments when they add clarity, not noise

**Inline event handlers (awareness only)**
- [ ] e.g. `<button onclick="alert('Hi')">` — still works but outdated
- [ ] Mixes structure (HTML) with behavior (JS)
- [ ] Modern approach: `addEventListener()` in JS files — learn it later
- [ ] Know it exists; don't build habits around it

---

### 1.3 Variables

**What is a variable**
- [ ] Named container for storing values
- [ ] Why: reuse data, avoid repetition, improve readability

**Declaring variables**
- [ ] Three keywords: `var`, `let`, `const`
- [ ] Modern best practice: prefer `const` by default, use `let` when reassignment needed, avoid `var`

**`let` (teach first)**
- [ ] Block scope: only accessible within `{ }` where declared
- [ ] Can be reassigned: `let x = 1; x = 2;` ✓
- [ ] Cannot be redeclared in same scope: `let x = 1; let x = 2;` ✗ → SyntaxError
- [ ] Temporal Dead Zone: cannot access before declaration → ReferenceError

**`const`**
- [ ] Block scope (same as let)
- [ ] Must be initialized at declaration: `const x;` ✗
- [ ] Cannot be reassigned: `const x = 1; x = 2;` ✗ → TypeError
- [ ] **Assignment vs mutation**: `const obj = {}; obj.name = "Alex";` ✓ — the binding is constant, not the value
- [ ] `const` does NOT mean immutable for objects/arrays
- [ ] Habit: prefer `const` by default — signals "this won't change"

**Reassignment vs redeclaration**
- [ ] Reassignment: changing the value (`x = 2`)
- [ ] Redeclaration: declaring same name again (`let x = 1; let x = 2;`)
- [ ] `let`: allows reassignment, blocks redeclaration in same scope
- [ ] `const`: blocks both reassignment and redeclaration
- [ ] `var`: allows both — which is why it causes bugs

**Understanding `var` (legacy awareness)**
- [ ] Function scope (not block scope): `if (true) { var x = 1; }` → `x` leaks outside the block
- [ ] Redeclaration allowed: no error for `var x = 1; var x = 2;`
- [ ] Hoisting: `var` declarations are moved to top of function; initialized with `undefined`
- [ ] Why avoided: unpredictable scope, accidental overwrites, confusing bugs
- [ ] Frame it: know it, recognize it in old code, but don't use it

**Hoisting (beginner level)**
- [ ] JavaScript processes declarations before execution
- [ ] `var` → hoisted and initialized with `undefined` (can access before declaration, gets `undefined`)
- [ ] `let` / `const` → hoisted but NOT initialized → Temporal Dead Zone → ReferenceError if accessed before declaration
- [ ] Function declarations → fully hoisted (can call before the line they appear on)
- [ ] Function expressions → NOT hoisted (variable is hoisted per its keyword, but the function assignment isn't)
- [ ] Rule: declare before use; don't rely on hoisting

**Temporal Dead Zone (TDZ)**
- [ ] The period between entering a scope and the actual declaration of `let`/`const`
- [ ] Accessing variable in TDZ → ReferenceError
- [ ] Encourages safer, more predictable code
- [ ] Only applies to `let`/`const`, not `var`

**Uninitialized variables**
- [ ] Declared but not assigned → value is `undefined` (for `let` and `var`)
- [ ] Accessing completely undeclared variable → ReferenceError
- [ ] Why this matters: `undefined` is a valid value; ReferenceError means the variable doesn't exist

**Naming rules**
- [ ] Allowed characters: letters, digits, `_`, `$`
- [ ] Cannot start with a digit: `1name` ✗
- [ ] Case-sensitive: `name` ≠ `Name` ≠ `NAME`
- [ ] Reserved words cannot be used: `let`, `const`, `class`, `return`, etc.

**Naming conventions**
- [ ] camelCase for variables and functions: `firstName`, `getUserData`
- [ ] UPPER_SNAKE_CASE for true constants: `MAX_SIZE`, `API_URL`
- [ ] Descriptive names: `userAge` not `x`; `isLoggedIn` not `flag`
- [ ] Avoid vague names: `data`, `temp`, `value`, `stuff`
- [ ] Code is read more than written — names are documentation

**Variable scope (mental model)**
- [ ] Global scope: accessible everywhere; avoid polluting
- [ ] Block scope: `let`/`const` inside `{ }` — only accessible within that block
- [ ] Function scope: `var` inside function — accessible anywhere in that function
- [ ] Minimize global variables — reduces bugs and naming collisions

**Shadowing (optional, light)**
- [ ] Inner scope variable with same name as outer scope variable
- [ ] Inner scope uses its own; outer is unaffected
- [ ] Can cause confusion — use distinct names when possible

**Dynamic typing**
- [ ] Variables can hold values of any type
- [ ] Type can change at runtime: `let x = 10; x = "hello"; x = true;`
- [ ] Flexibility: fast to write; risk: unexpected type bugs

**Best practices**
- [ ] Declare close to where used
- [ ] Prefer `const`, use `let` when needed, avoid `var`
- [ ] One declaration per line
- [ ] Don't reuse variable names for different purposes

---

### 1.4 Primitive Data Types

**What is a data type**
- [ ] Classification of values that determines what operations are allowed
- [ ] Why it matters: `"5" + 2` vs `5 + 2` produce different results because of types
- [ ] JavaScript is dynamically typed: types checked at runtime
- [ ] Key insight: **variables don't have types — values do**

**Primitive vs non-primitive (seed)**
- [ ] Primitive = single, immutable value; stored and copied **by value**
- [ ] Non-primitive (objects) = stored and copied **by reference** (deep dive later)
- [ ] Don't go deep yet — just plant the seed

**The 7 primitive types**
- [ ] string, number, boolean, undefined, null, symbol, bigint
- [ ] You will use string, number, boolean **daily** — reduces anxiety

**string**
- [ ] Literals: single quotes `'hello'`, double quotes `"hello"`, backticks `` `hello` ``
- [ ] Template literals (backticks): `${expression}` for interpolation; multi-line strings
- [ ] Escape sequences: `\n` (newline), `\\` (backslash), `\"` (quote), `\t` (tab)
- [ ] `.length` property: number of characters (technically UTF-16 code units)
- [ ] Strings are **immutable**: `str[0] = "X"` does nothing; you create a new string instead
- [ ] String methods: covered in Phase 2 (don't overload here)

**number**
- [ ] JavaScript has **one** numeric type (no separate int/float like other languages)
- [ ] Includes integers and decimals: `42`, `3.14`, `-7`
- [ ] Special values:
  - [ ] `NaN` (Not a Number): result of failed numeric operation (e.g. `"abc" * 2`); `typeof NaN === "number"`; `NaN !== NaN`
  - [ ] `Infinity` and `-Infinity`: result of division by zero or overflow
- [ ] NaN propagation: any operation with NaN returns NaN
- [ ] No IEEE 754 deep dive yet; just know `0.1 + 0.2 !== 0.3` (floating-point quirk)

**boolean**
- [ ] Two values: `true` and `false`
- [ ] Used for decisions (if/else, loops, conditions)
- [ ] Comparison operators return booleans: `5 > 3` → `true`

**undefined**
- [ ] Default value for uninitialized variables: `let x; console.log(x);` → `undefined`
- [ ] Also: missing function parameters, functions that don't return, missing object properties
- [ ] Means: "value not assigned yet" — set by the system

**null**
- [ ] Intentional absence of value — set explicitly by developers
- [ ] `let user = null;` means "no user right now"
- [ ] **null vs undefined**: undefined = system says "nothing here yet"; null = developer says "intentionally empty"
- [ ] Simple rule: undefined → system; null → developer

**symbol (light coverage)**
- [ ] Created with `Symbol()` or `Symbol("description")`
- [ ] Every symbol is **unique**: `Symbol("a") !== Symbol("a")`
- [ ] Mainly used as unique object property keys (no accidental name collisions)
- [ ] Rare in beginner code — awareness is enough
- [ ] Well-known symbols exist (Symbol.iterator, etc.) — covered in Phase 6

**bigint (light coverage)**
- [ ] For very large integers beyond Number.MAX_SAFE_INTEGER
- [ ] Created with `123n` literal or `BigInt(123)`
- [ ] Cannot mix directly with Number in operations: `1n + 2` → TypeError
- [ ] No decimals allowed
- [ ] Awareness is enough for now

**`typeof` operator**
- [ ] Returns a string indicating the type of a value
- [ ] Common results:
  - [ ] `typeof "hello"` → `"string"`
  - [ ] `typeof 42` → `"number"`
  - [ ] `typeof true` → `"boolean"`
  - [ ] `typeof undefined` → `"undefined"`
  - [ ] `typeof Symbol()` → `"symbol"`
  - [ ] `typeof 123n` → `"bigint"`
  - [ ] `typeof {}` → `"object"`
  - [ ] `typeof function(){}` → `"function"`
- [ ] **typeof null quirk**: `typeof null` → `"object"` — historical bug from 1995; cannot be fixed

**Immutability**
- [ ] Primitive values cannot be changed after creation
- [ ] Reassignment creates a **new** value: `let x = "hello"; x = "world";` — the string "hello" wasn't modified; `x` now points to a new string
- [ ] Mental model: you don't modify a primitive — you replace it

**Copy by value**
- [ ] Assigning a primitive copies the actual value: `let a = 5; let b = a;` → `b` is an independent copy
- [ ] Changing `b` does NOT affect `a`
- [ ] Contrast: objects copy by reference (later) — this is a major source of bugs

---

### 1.5 Type Coercion and Equality

**What is type coercion**
- [ ] Automatic or manual conversion from one type to another
- [ ] **Implicit** (automatic): JavaScript converts types behind the scenes
- [ ] **Explicit** (manual): developer converts intentionally with `Number()`, `String()`, `Boolean()`
- [ ] Framing: JavaScript tries to help — sometimes too much

**Implicit coercion — strings**
- [ ] `+` with a string converts the other to string: `"5" + 2` → `"52"` (string concatenation)
- [ ] `+` is BOTH addition AND concatenation — major beginner trap
- [ ] Other operators (`-`, `*`, `/`, `%`) convert strings to numbers: `"5" - 2` → `3`
- [ ] Empty string to number: `"" - 0` → `0`

**Implicit coercion — booleans**
- [ ] In conditionals (`if`, `while`, ternary), values are converted to boolean
- [ ] This is where truthy/falsy matters

**Truthy and falsy**
- [ ] **Falsy values** (memorize — there are only 6):
  - [ ] `false`
  - [ ] `0` (and `-0`)
  - [ ] `""` (empty string)
  - [ ] `null`
  - [ ] `undefined`
  - [ ] `NaN`
- [ ] **Everything else is truthy**: `"hello"`, `42`, `[]`, `{}`, `" "` (space), `"0"`, `"false"`, etc.
- [ ] Don't list many truthy examples — just say "everything else"

**Loose equality (`==`, `!=`)**
- [ ] Performs type coercion before comparing
- [ ] Compares values after attempting to make both the same type
- [ ] Surprising results:
  - [ ] `"5" == 5` → `true` (string coerced to number)
  - [ ] `false == 0` → `true` (boolean coerced to number)
  - [ ] `null == undefined` → `true` (special case in spec)
  - [ ] `"" == 0` → `true`
  - [ ] `[] == false` → `true`
- [ ] Mental model: `==` tries to make both sides the same type, then compares
- [ ] Don't memorize the full algorithm — understand that it's unpredictable

**Strict equality (`===`, `!==`)**
- [ ] NO coercion: same type AND same value required
- [ ] `"5" === 5` → `false` (different types)
- [ ] `0 === false` → `false` (different types)
- [ ] `null === undefined` → `false` (different types)
- [ ] Predictable, safe, easy to reason about
- [ ] **Golden rule: use `===` by default — make it a reflex**

**`Object.is()` (light)**
- [ ] Same-value equality (like `===` but handles two edge cases)
- [ ] `NaN === NaN` → `false`; but `Object.is(NaN, NaN)` → `true`
- [ ] `+0 === -0` → `true`; but `Object.is(+0, -0)` → `false`
- [ ] Rarely used in beginner code — awareness only

**Explicit coercion**
- [ ] `Number("25")` → `25`; `Number("abc")` → `NaN`; `Number(true)` → `1`; `Number(null)` → `0`
- [ ] `String(42)` → `"42"`; `String(null)` → `"null"`
- [ ] `Boolean(0)` → `false`; `Boolean("hello")` → `true`
- [ ] Developers should control conversions — don't rely on implicit magic

---

### 1.6 Operators

**Arithmetic**
- [ ] `+` addition (or string concatenation), `-` subtraction, `*` multiplication, `/` division
- [ ] `%` remainder (modulo), `**` exponentiation (e.g. `2 ** 3` → `8`)
- [ ] `++` increment, `--` decrement; prefix (`++x` increments then returns) vs postfix (`x++` returns then increments)
- [ ] Unary `+` converts to number: `+"5"` → `5`; unary `-` negates

**Assignment**
- [ ] `=` assign
- [ ] Compound: `+=`, `-=`, `*=`, `/=`, `%=`, `**=`
- [ ] `x += 5` is `x = x + 5`

**Comparison**
- [ ] `>`, `<`, `>=`, `<=` — numeric or string comparison (alphabetical for strings)
- [ ] `==`, `===`, `!=`, `!==` — see coercion section above

**Logical**
- [ ] `&&` (AND): returns first falsy value, or last value if all truthy; short-circuits
- [ ] `||` (OR): returns first truthy value, or last value if all falsy; short-circuits
- [ ] `!` (NOT): inverts boolean; `!!value` for explicit boolean conversion
- [ ] Short-circuit evaluation: right side may not execute

**Nullish coalescing `??`**
- [ ] Returns right side ONLY if left is `null` or `undefined`
- [ ] `0 ?? "default"` → `0` (because 0 is not null/undefined)
- [ ] `null ?? "default"` → `"default"`
- [ ] Different from `||`: `0 || "default"` → `"default"` (because 0 is falsy)
- [ ] Use `??` when 0, "", false are valid values

**Optional chaining `?.`**
- [ ] Safe property access: `obj?.prop?.nested` → `undefined` instead of TypeError
- [ ] Works for methods: `obj?.method?.()` — won't call if method is undefined
- [ ] Works for brackets: `obj?.["key"]`

**Ternary**
- [ ] `condition ? valueIfTrue : valueIfFalse`
- [ ] Shorthand for simple if/else; avoid nesting (becomes unreadable)

**Other operators**
- [ ] Comma `,`: evaluates left to right, returns rightmost value
- [ ] `in`: `"key" in obj` → true/false (checks if property exists in object or prototype)
- [ ] `instanceof`: `obj instanceof Constructor` (checks prototype chain)
- [ ] `delete`: `delete obj.key` (removes property; doesn't work on variables)
- [ ] `void`: `void expression` → returns `undefined`
- [ ] Logical assignment: `x &&= y` (assign if truthy), `x ||= y` (assign if falsy), `x ??= y` (assign if null/undefined)
- [ ] Spread `...`: expands iterables (arrays, strings) in array/object literals and function calls
- [ ] Rest `...`: collects remaining items in destructuring or function parameters

---

### 1.7 Control Flow

**Conditional**
- [ ] `if (condition) { }` — runs block if condition is truthy
- [ ] `else if (condition) { }` — additional checks
- [ ] `else { }` — fallback if all conditions false
- [ ] `switch (expr) { case val: ... break; default: ... }` — multiple value matches; don't forget `break`

**Loops**
- [ ] `for (init; condition; update) { }` — classic counting loop
- [ ] `while (condition) { }` — loop while condition true; check first
- [ ] `do { } while (condition);` — execute at least once, then check
- [ ] `for...in` — iterate over enumerable property **keys** of object (includes prototype chain; order not guaranteed for numeric keys)
- [ ] `for...of` — iterate over iterable **values** (arrays, strings, Map, Set, etc.); does NOT work on plain objects

**Control**
- [ ] `break` — exit loop entirely
- [ ] `continue` — skip to next iteration
- [ ] Labels: `outer: for (...)` + `break outer;` — rare but useful for nested loops
- [ ] Choosing the right loop: `for` for counting, `for...of` for iterables, `for...in` for object keys, `while` for unknown iterations

---

### 1.8 Functions (Basics)

**Function declaration**
- [ ] `function name(params) { return value; }`
- [ ] Hoisted: can be called before the line it appears on
- [ ] Creates a named function

**Function expression**
- [ ] `const fn = function(params) { };` — assigned to variable
- [ ] NOT hoisted: cannot call before the assignment line
- [ ] Can be anonymous or named

**Parameters and arguments**
- [ ] Parameters: names in function definition
- [ ] Arguments: values passed at call time
- [ ] Missing arguments → `undefined`; extra arguments → ignored (but accessible via `arguments`)
- [ ] Arity: number of declared parameters (`fn.length`)

**Return**
- [ ] `return value;` — sends value back to caller and exits function
- [ ] Functions without `return` (or with `return;`) return `undefined`
- [ ] Only one return value (use object/array to return multiple)

**Scope**
- [ ] Global scope: variables declared outside any function/block
- [ ] Function scope: variables declared inside function (with `var`, `let`, or `const`)
- [ ] Block scope: `let`/`const` inside `{ }` (if, for, etc.)
- [ ] Lexical scope: function accesses variables from where it was **defined**, not where it's called
- [ ] Nested functions: inner function can access outer function's variables (closure intro)

**Shadowing**
- [ ] Inner variable with same name as outer → inner scope uses its own, outer unaffected

---

## Phase 2: Core Data Structures and Built-ins

### 2.1 Arrays

- [ ] Array is an object; indices are string property keys ("0", "1", ...)
- [ ] **Creating**: `[]`, `new Array(len)`, `new Array(a, b, c)`, `Array.from(iterable, mapFn?)`, `Array.of(1, 2, 3)`
- [ ] **Length**: `.length` (writable — can truncate or extend); sparse arrays (holes)
- [ ] **Indexing**: `arr[0]`, `arr[arr.length - 1]`; out-of-bounds → `undefined`
- [ ] **Mutating methods** (change original): `push`, `pop`, `shift`, `unshift`, `splice`, `sort`, `reverse`, `fill`, `copyWithin`
- [ ] **Non-mutating methods** (return new): `slice`, `concat`, `join`, `indexOf`, `lastIndexOf`, `includes`
- [ ] **Iteration methods**: `forEach`, `map`, `filter`, `reduce`, `reduceRight`, `find`, `findIndex`, `findLast`, `findLastIndex`, `some`, `every`, `flat`, `flatMap`
- [ ] **sort(compareFn)**: default sorts as strings; pass comparator for numbers: `(a, b) => a - b`; stable sort
- [ ] **Spread**: `[...arr]` for shallow copy, concatenation
- [ ] **Destructuring**: `const [a, b, ...rest] = arr`; default values `[a = 1]`; swap `[a, b] = [b, a]`
- [ ] **Multidimensional**: nested arrays; flatten with `flat(depth)` or `flat(Infinity)`
- [ ] **Array.isArray()** vs `typeof` (typeof returns "object" for arrays)
- [ ] **Array-like objects**: `arguments`, `NodeList`; convert with `Array.from()` or `[...arrayLike]`

### 2.2 Objects

- [ ] Collection of key-value pairs; keys are strings or Symbols
- [ ] **Literal**: `{ key: value, "key": value, [computed]: value }`
- [ ] **Property shorthand**: `{ name }` → `{ name: name }`
- [ ] **Method shorthand**: `{ greet() {} }` → `{ greet: function() {} }`
- [ ] **Access**: dot `obj.key` vs bracket `obj["key"]` (bracket for dynamic keys, special chars)
- [ ] **Adding/updating**: `obj.key = value`; **deleting**: `delete obj.key`
- [ ] **Checking**: `"key" in obj` (includes prototype), `obj.hasOwnProperty("key")`, `Object.hasOwn(obj, "key")` (ES2022)
- [ ] **Iteration**: `for...in` (enumerable + prototype), `Object.keys(obj)`, `Object.values(obj)`, `Object.entries(obj)` (own enumerable only)
- [ ] **Static methods**: `Object.assign(target, ...sources)`, `Object.create(proto)`, `Object.freeze()`, `Object.seal()`, `Object.defineProperty()`, `Object.getOwnPropertyDescriptor()`, `Object.fromEntries()`
- [ ] **Destructuring**: `const { a, b: renamed, c = defaultVal, ...rest } = obj`; nested destructuring
- [ ] **Shallow copy**: spread `{...obj}`, `Object.assign({}, obj)`; **deep copy**: `structuredClone(obj)` or recursive
- [ ] **Optional chaining**: `obj?.prop?.nested`, `obj?.method?.()`
- [ ] **Property descriptors**: `configurable`, `enumerable`, `writable`, `value`; getters/setters with `get`/`set`
- [ ] **Prototype**: every object has internal `[[Prototype]]`; `Object.getPrototypeOf(obj)` — deep dive in Phase 5

### 2.3 Strings (Full)

- [ ] Auto-boxing: `"hello".toUpperCase()` — primitive temporarily wrapped in String object
- [ ] `.length` — UTF-16 code units (not always = characters for emojis/surrogate pairs)
- [ ] Access: `str[0]`, `str.charAt(0)`; strings are **immutable**
- [ ] **Search**: `indexOf`, `lastIndexOf`, `includes`, `startsWith`, `endsWith`, `search(regex)`, `match(regex)`, `matchAll(regex)`
- [ ] **Extract**: `slice(start, end)`, `substring(start, end)` (no negative), `substr` (legacy)
- [ ] **Transform**: `toUpperCase()`, `toLowerCase()`, `trim()`, `trimStart()`, `trimEnd()`, `repeat(n)`, `padStart(len, char)`, `padEnd(len, char)`
- [ ] **Replace**: `replace(pattern, replacement)`, `replaceAll(pattern, replacement)`; replacement patterns `$&`, `$1`
- [ ] **Split**: `split(separator, limit)` → array
- [ ] **Template literals**: `` `Hello ${expression}` ``; multi-line; nesting
- [ ] **Tagged templates**: `` tag`strings ${expr}` `` — function receives string segments and values
- [ ] **Unicode**: `\uXXXX`, `\u{X}`; `String.fromCodePoint`, `codePointAt`; iterate code points with `for...of`

### 2.4 Numbers and Math

- [ ] IEEE 754 double-precision; safe range `Number.MIN_SAFE_INTEGER` to `Number.MAX_SAFE_INTEGER`
- [ ] Parsing: `Number(val)`, `parseInt(str, radix)`, `parseFloat(str)` — always specify radix for parseInt
- [ ] Checking: `isNaN()` vs `Number.isNaN()` (strict); `Number.isFinite()`, `Number.isInteger()`, `Number.isSafeInteger()`
- [ ] Conversion: `toString(radix)`, `toFixed(digits)`, `toExponential()`, `toPrecision()`
- [ ] **Math**: `abs`, `sign`, `ceil`, `floor`, `round`, `trunc`, `min`, `max`, `sqrt`, `cbrt`, `pow`, `random`, `log`, `log10`
- [ ] Floating-point gotcha: `0.1 + 0.2 !== 0.3`; rounding strategies (`toFixed`, multiply-then-divide)
- [ ] **BigInt**: `123n`, `BigInt(123)`; no decimals; explicit conversion to mix with Number

### 2.5 Dates

- [ ] `new Date()`, `new Date(timestamp)`, `new Date(year, month, ...)`, `new Date(string)`
- [ ] Months are 0-indexed (January = 0)
- [ ] Getters/setters: `getFullYear`, `getMonth`, `getDate`, `getDay`, `getHours`, `getMinutes`, `getSeconds`, `getMilliseconds`, `getTime`; UTC variants
- [ ] Timestamps: ms since Unix epoch; `Date.now()`, `getTime()`
- [ ] Formatting: `toISOString()`, `toLocaleString()`, `toLocaleDateString()`
- [ ] Manipulation: no built-in add/subtract; use timestamp math
- [ ] Time zones: UTC vs local; limitations of built-in Date

### 2.6 JSON

- [ ] `JSON.stringify(value, replacer?, space?)` — object/array → JSON string; replacer filters/transforms
- [ ] `JSON.parse(string, reviver?)` — JSON string → object; reviver transforms values
- [ ] Supported: object, array, string, number, boolean, null; NOT function, undefined, Symbol, BigInt
- [ ] Dates serialize as ISO string; restore in reviver
- [ ] Circular references → TypeError; `toJSON()` method for custom serialization

### 2.7 RegExp

- [ ] Creating: `/pattern/flags`, `new RegExp(pattern, flags)` (for dynamic patterns)
- [ ] Flags: `g` (global), `i` (case-insensitive), `m` (multiline), `s` (dotAll), `u` (unicode), `y` (sticky), `v` (ES2024 unicode sets)
- [ ] Patterns: character classes `[abc]`, `\d`, `\w`, `\s`; quantifiers `*`, `+`, `?`, `{n,m}`; anchors `^`, `$`, `\b`; alternation `|`; groups `()`; non-capturing `(?:)`; lookahead `(?=)`, `(?!)`; named groups `(?<name>)`; backreferences `\1`
- [ ] Methods: `test(str)` → boolean; `exec(str)` → match array or null (with `lastIndex` for g/y)
- [ ] String methods with regex: `match`, `matchAll`, `search`, `replace`, `replaceAll`, `split`

### 2.8 Map and Set

- [ ] **Map**: any key type (not just strings); insertion order; `new Map()`, `new Map([[k,v]])`
  - [ ] API: `set`, `get`, `has`, `delete`, `clear`, `size`; `keys()`, `values()`, `entries()`, `forEach`
- [ ] **Set**: unique values; insertion order; `new Set()`, `new Set([1,2,3])`
  - [ ] API: `add`, `has`, `delete`, `clear`, `size`; `keys()`, `values()`, `entries()`, `forEach`
  - [ ] ES2024: `union`, `intersection`, `difference`, `symmetricDifference`, `isSubsetOf`, `isSupersetOf`
- [ ] **WeakMap**: keys must be objects; weak reference (GC); no iteration, no size
- [ ] **WeakSet**: values must be objects; weak reference; no iteration
- [ ] When to use: Map over Object when keys aren't strings or need insertion order; Set for unique collections

---

## Phase 3: Functions (Deep Dive)

### 3.1 Closures
- [ ] Closure: function that "remembers" variables from its lexical scope (where it was defined), even after the outer function returns
- [ ] How: inner function retains a reference to the outer function's variable environment
- [ ] Practical uses: private state (counter), factory functions, partial application, module pattern
- [ ] Classic mistake: `var` in loop with `setTimeout` — all callbacks share same `i`; fix with `let` (block scope) or IIFE
- [ ] Memory: closures keep references alive → be aware of unintended retention of large objects

### 3.2 Execution Context and `this`
- [ ] `this`: determined by HOW a function is called (call site), not where it's defined
- [ ] **Default binding**: standalone function call → `this` is global object (non-strict) or `undefined` (strict)
- [ ] **Implicit binding**: `obj.method()` → `this` is `obj`; lost if you extract: `const fn = obj.method; fn();`
- [ ] **Explicit binding**: `fn.call(thisArg, arg1, arg2)`, `fn.apply(thisArg, [args])`, `fn.bind(thisArg)` — bind returns new function
- [ ] **new binding**: `new Constructor()` → `this` is new empty object; constructor sets properties on it
- [ ] **Precedence**: new > explicit (call/apply/bind) > implicit (obj.method) > default
- [ ] **Arrow functions**: NO own `this`; inherit `this` from enclosing lexical scope; cannot be changed with call/apply/bind
- [ ] Arrow pitfalls: don't use as object methods (no `this`), can't use as constructors (no `new`), no `arguments` object

### 3.3 Function Forms and Parameters
- [ ] **Arrow functions**: `(x) => x * 2`, `(x, y) => { return x + y; }`; concise body (implicit return) vs block body
- [ ] **Default parameters**: `function fn(a = 1, b = 2) {}`; evaluated at call time; later defaults can use earlier params
- [ ] **Rest parameters**: `function fn(...args) {}`; `args` is a real array; must be last parameter
- [ ] **`arguments` object** (non-arrow): array-like (not a real array); `arguments.length`; convert: `Array.from(arguments)` or `[...arguments]`
- [ ] **Function `.length`**: number of parameters before first default or rest
- [ ] **Function `.name`**: inferred from assignment; useful for debugging

### 3.4 Higher-Order Functions and Callbacks
- [ ] **First-class functions**: functions are values; can be stored, passed, returned
- [ ] **Higher-order function**: takes function as argument AND/OR returns a function
- [ ] **Built-in HOFs**: `map`, `filter`, `reduce`, `forEach`, `sort`, `find`, `some`, `every`
- [ ] **Callback pattern**: pass function to be called later (e.g. event handler, timer, async operation)
- [ ] **Callback hell**: deeply nested callbacks → hard to read → solved by Promises and async/await
- [ ] **Custom HOFs**: `once()` (run function once), `debounce()`, `throttle()`, `memoize()`

### 3.5 IIFE and Module Pattern
- [ ] **IIFE**: `(function() { })()` — immediately invoked; creates private scope
- [ ] **Module pattern**: IIFE returning an object with public methods; private variables stay inside
- [ ] **Revealing module**: return object mapping names to inner functions
- [ ] Historical purpose: before ES modules, this was the way to encapsulate code and avoid globals

### 3.6 Error Handling
- [ ] **try/catch/finally**: `try { } catch (err) { } finally { }` — finally always runs
- [ ] **throw**: `throw new Error("message")` — throw any value, but prefer Error instances
- [ ] **Error types**: `Error`, `SyntaxError`, `TypeError`, `ReferenceError`, `RangeError`, `URIError`, `AggregateError`
- [ ] **Error properties**: `message`, `name`, `stack` (non-standard but universal)
- [ ] **Custom errors**: `class MyError extends Error { constructor(msg) { super(msg); this.name = "MyError"; } }`
- [ ] **Best practices**: catch specific errors; don't swallow errors (empty catch); clean up in finally; rethrow if you can't handle

---

## Phase 4: Asynchronous JavaScript

### 4.1 Event Loop and Concurrency
- [ ] **Call stack**: one thread; runs sync code; stack of execution contexts
- [ ] **Task queue (macrotask)**: `setTimeout`, `setInterval`, I/O, UI events → callbacks placed here
- [ ] **Microtask queue**: Promise `.then/.catch/.finally`, `queueMicrotask()`, `MutationObserver` → higher priority
- [ ] **Order**: sync code → all microtasks → one macrotask → all microtasks → next macrotask → repeat
- [ ] **setTimeout(fn, delay)**: minimum delay (not exact); returns timer ID; `clearTimeout(id)`
- [ ] **setInterval(fn, delay)**: repeating; `clearInterval(id)`
- [ ] **requestAnimationFrame(callback)**: for animations; fires before next repaint (~60fps)
- [ ] **queueMicrotask(fn)**: schedule microtask directly
- [ ] No true parallelism in JS (single thread); concurrency = scheduling via event loop

### 4.2 Promises
- [ ] **Promise**: object representing eventual completion or failure
- [ ] **States**: pending → fulfilled (resolved with value) or rejected (with reason); immutable once settled
- [ ] **Creating**: `new Promise((resolve, reject) => { })` — resolve/reject called once
- [ ] **Consuming**: `.then(onFulfilled, onRejected)`, `.catch(onRejected)`, `.finally(onSettled)`
- [ ] **Chaining**: return value from `.then` becomes next Promise's value; return Promise to chain async ops
- [ ] **Error propagation**: rejection flows through chain until caught by `.catch`
- [ ] **Promise.resolve(val)** / **Promise.reject(reason)**: create already settled Promises
- [ ] **Promise.all([...])**: all fulfill → array of values; one reject → first rejection
- [ ] **Promise.allSettled([...])**: wait for all; array of `{status, value/reason}`
- [ ] **Promise.race([...])**: first to settle (fulfill or reject)
- [ ] **Promise.any([...])**: first to fulfill; all reject → AggregateError
- [ ] **Promisifying**: wrap callback API in `new Promise`

### 4.3 Async/Await
- [ ] **async function**: always returns Promise; return value wrapped in Promise.resolve; throw → Promise.reject
- [ ] **await**: pause until Promise settles; returns fulfilled value; throws on rejection
- [ ] **Sequential**: `const a = await fetchA(); const b = await fetchB();` — B waits for A
- [ ] **Parallel**: `const [a, b] = await Promise.all([fetchA(), fetchB()]);`
- [ ] **Error handling**: try/catch around await; or `.catch()` on the returned Promise
- [ ] **Top-level await**: in ES modules only
- [ ] **Patterns**: retry loop, timeout with `Promise.race`, sequential async in for loop

### 4.4 Fetch
- [ ] `fetch(url, options?)` → Promise<Response>; does NOT throw on 4xx/5xx (only network error)
- [ ] **Options**: method, headers, body (string, FormData, JSON.stringify), mode, credentials
- [ ] **Response**: `response.ok`, `.status`, `.headers`; body methods: `.json()`, `.text()`, `.blob()`, `.arrayBuffer()` (consumed once)
- [ ] **Error handling**: check `response.ok`; throw on failure
- [ ] **AbortController**: `const ctrl = new AbortController(); fetch(url, {signal: ctrl.signal}); ctrl.abort();`
- [ ] **CORS**: same-origin policy; preflight for non-simple requests; `credentials: "include"` for cookies

---

## Phase 5: OOP (Prototypes and Classes)

### 5.1 Prototypes
- [ ] Every object has internal `[[Prototype]]`; access with `Object.getPrototypeOf(obj)` (not `__proto__`)
- [ ] **Prototype chain**: property lookup goes object → prototype → prototype's prototype → ... → `null`
- [ ] **Constructor.prototype**: the prototype of all instances created with `new Constructor()`
- [ ] **Own vs inherited**: `Object.hasOwn(obj, key)` (own only); `in` operator (includes prototype)
- [ ] **Object.create(proto)**: create object with specified prototype; no constructor call
- [ ] **new keyword**: creates new object → sets prototype → calls constructor with `this` = new object → returns object
- [ ] **instanceof**: checks if Constructor.prototype is anywhere in the prototype chain

### 5.2 Classes
- [ ] `class Name { constructor() {} method() {} }` — syntactic sugar over constructor + prototype
- [ ] NOT hoisted like function declarations
- [ ] **constructor**: initializes instance; `super()` required in subclass before using `this`
- [ ] **Instance methods**: defined on prototype (shared)
- [ ] **Static methods/fields**: `static method() {}`; on the class itself, not instances
- [ ] **Instance fields**: `field = value` in class body
- [ ] **Private**: `#field`, `#method()` — only accessible inside class body; true encapsulation
- [ ] **extends**: `class Child extends Parent` — sets up prototype chain; `super` calls parent
- [ ] **Getters/setters**: `get name() {}`, `set name(v) {}` — computed properties
- [ ] **Composition vs inheritance**: prefer "has-a" over "is-a" when possible; avoid deep hierarchies

### 5.3 Built-in Constructors
- [ ] Array, Date, RegExp, Error, Map, Set — all are constructors
- [ ] Subclassing: `class MyArray extends Array` — works with Symbol.species for derived instances

---

## Phase 6: Iteration, Iterators, Generators

### 6.1 Iterables and Iterators
- [ ] **Iterable**: object with `[Symbol.iterator]()` method that returns an iterator
- [ ] **Iterator**: object with `next()` method returning `{ value, done }`
- [ ] **Built-in iterables**: Array, String, Map, Set, arguments, NodeList, TypedArray; Object is NOT iterable
- [ ] **Consumers**: `for...of`, spread `...`, `Array.from()`, destructuring, `yield*`
- [ ] **Custom iterable**: implement `[Symbol.iterator]()` returning `{ next() { return {value, done}; } }`

### 6.2 Generators
- [ ] `function* gen() { yield 1; yield 2; }` — returns generator object (iterator)
- [ ] `yield`: pauses execution; `gen.next()` resumes; `next(value)` passes value into generator
- [ ] `yield*`: delegate to another iterable/generator
- [ ] **Lazy sequences**: infinite generators; compute on demand
- [ ] `return(value)`: sets done=true; `throw(error)`: inject exception

### 6.3 Async Iteration
- [ ] `async function* gen() { yield await fetch(...); }` — async generator
- [ ] `for await (const item of asyncIterable) { }` — consume async iterables
- [ ] Use cases: streaming data, paginated APIs, real-time feeds

---

## Phase 7: Modules and Strict Mode

### 7.1 ES Modules
- [ ] `<script type="module">` — deferred by default; module scope (not global); strict mode automatic
- [ ] **Named export**: `export const x = 1;`, `export { a, b };`, `export { a as alias };`
- [ ] **Default export**: `export default expression;` — one per module
- [ ] **Import**: `import { a } from './mod.js'`, `import def from './mod.js'`, `import * as ns from './mod.js'`
- [ ] **Dynamic import**: `const mod = await import('./mod.js');` — for code-splitting, conditional loading
- [ ] **Top-level await**: allowed in modules; blocks module evaluation
- [ ] **Circular dependencies**: imports are live bindings; may be `undefined` until module executes

### 7.2 Strict Mode
- [ ] `"use strict";` at top of file or function
- [ ] Changes: undeclared variable assignment throws; no duplicate params; `this` is `undefined` in plain calls; no `with`; `delete` on non-configurable throws; reserved word restrictions
- [ ] ES modules are strict by default

### 7.3 globalThis
- [ ] Cross-environment global: `globalThis` works in browser (`window`), Node (`global`), workers (`self`)
- [ ] Avoid adding custom properties to global object

---

## Phase 8: Proxy, Reflect, Symbols

### 8.1 Proxy
- [ ] `new Proxy(target, handler)` — intercept operations on target
- [ ] **Key traps**: `get(target, prop, receiver)`, `set(target, prop, value, receiver)`, `has(target, prop)`, `deleteProperty`, `ownKeys`, `apply` (for functions), `construct` (for new)
- [ ] **Use cases**: validation, default values, logging, observable objects, virtual properties
- [ ] **Revocable**: `Proxy.revocable()` — can disable proxy later

### 8.2 Reflect
- [ ] Methods mirror Proxy traps; provide default behavior for operations
- [ ] `Reflect.get`, `Reflect.set`, `Reflect.has`, `Reflect.deleteProperty`, `Reflect.ownKeys`, `Reflect.apply`, `Reflect.construct`
- [ ] Use inside Proxy traps: perform default action + custom logic

### 8.3 Symbols (Deep)
- [ ] **Well-known symbols**: `Symbol.iterator`, `Symbol.asyncIterator`, `Symbol.toPrimitive`, `Symbol.toStringTag`, `Symbol.hasInstance`, `Symbol.species`, `Symbol.isConcatSpreadable`
- [ ] `Symbol.toPrimitive`: control how object converts to number/string
- [ ] `Symbol.toStringTag`: customize `Object.prototype.toString` result

---

## Phase 9: JavaScript in the Browser

### 9.1 DOM
- [ ] Document tree: Document → Element → Text nodes
- [ ] **Selecting**: `getElementById`, `querySelector`, `querySelectorAll` (static), `getElementsByClassName` (live)
- [ ] **Traversal**: parentNode, children, firstElementChild, nextElementSibling, etc.
- [ ] **Creating**: `createElement`, `createTextNode`, `createDocumentFragment`, `cloneNode`
- [ ] **Inserting**: `append`, `prepend`, `before`, `after`, `replaceWith`, `remove()`
- [ ] **Attributes**: `getAttribute`, `setAttribute`, `dataset` (data-* attributes)
- [ ] **Classes**: `classList.add/remove/toggle/contains`
- [ ] **Content**: `textContent` (safe), `innerHTML` (XSS risk), `innerText`
- [ ] **Styles**: `element.style.property`, `getComputedStyle(el)`
- [ ] **Events**: `addEventListener(type, handler, options)`, `removeEventListener`; `event.target`, `event.currentTarget`, `preventDefault()`, `stopPropagation()`
- [ ] **Event phases**: capturing → target → bubbling
- [ ] **Event delegation**: single listener on parent; check `event.target`
- [ ] **Common events**: click, submit, input, change, keydown, keyup, load, DOMContentLoaded
- [ ] **Custom events**: `new CustomEvent("name", {detail: data})`, `dispatchEvent`

### 9.2 BOM
- [ ] `window`: global; `innerWidth/Height`, `scrollX/Y`, `open`, `close`, `alert/confirm/prompt`
- [ ] `location`: `href`, `pathname`, `search`, `hash`; `assign()`, `replace()`, `reload()`
- [ ] `history`: `back()`, `forward()`, `pushState`, `replaceState`
- [ ] `navigator`: `userAgent`, `language`, `geolocation`
- [ ] `requestAnimationFrame`, `cancelAnimationFrame`

### 9.3 Storage
- [ ] `localStorage`: `setItem`, `getItem`, `removeItem`, `clear`; string only; persistent; same origin
- [ ] `sessionStorage`: same API; cleared on tab close
- [ ] Cookies: `document.cookie`; HttpOnly, Secure, SameSite
- [ ] IndexedDB: async key-value store for larger data (concept)

### 9.4 Web APIs
- [ ] URL / URLSearchParams, Blob / File / FileReader, FormData
- [ ] IntersectionObserver, ResizeObserver, MutationObserver
- [ ] Page Visibility, Clipboard, Geolocation
- [ ] Web Workers (concept): separate thread; postMessage; no DOM
- [ ] requestIdleCallback

---

## Phase 10: Advanced

### 10.1 Performance
- [ ] Minimize reflows: batch DOM reads/writes; avoid layout thrashing
- [ ] Debounce (delay until pause) and throttle (limit rate)
- [ ] Memory leaks: detached DOM, closures holding references, forgotten listeners
- [ ] requestAnimationFrame for animations
- [ ] Chrome DevTools: Performance tab, Memory tab

### 10.2 Security
- [ ] XSS: never insert user input with innerHTML; use textContent or sanitize
- [ ] CORS: same-origin policy; Access-Control headers
- [ ] CSP: Content-Security-Policy for script sources
- [ ] eval: avoid; same risks as XSS with untrusted input

### 10.3 Recursion
- [ ] Function calling itself; base case + recursive case
- [ ] Stack overflow for deep recursion
- [ ] TCO (tail call optimization): in spec but limited support; trampoline pattern as alternative

### 10.4 Typed Arrays
- [ ] ArrayBuffer: raw binary data; DataView and typed arrays (Uint8Array, Float32Array, etc.)
- [ ] Use: binary protocols, file parsing, WebGL

### 10.5 Intl
- [ ] `Intl.NumberFormat`: currency, percent, locale
- [ ] `Intl.DateTimeFormat`: dates by locale
- [ ] `Intl.RelativeTimeFormat`: "3 days ago"
- [ ] `Intl.Collator`, `Intl.ListFormat`, `Intl.Segmenter`

### 10.6 Modern Features (ES2020–ES2024)
- [ ] `?.`, `??`, `??=`, `||=`, `&&=`
- [ ] `Array.at()`, `Object.hasOwn()`, `structuredClone()`
- [ ] `String.replaceAll()`, `String.matchAll()`
- [ ] `Promise.allSettled`, `Promise.any`, `Promise.withResolvers` (ES2024)
- [ ] `Object.groupBy`, `Map.groupBy` (ES2024)
- [ ] `Array.fromAsync` (ES2024)
- [ ] Set methods: `union`, `intersection`, `difference` (ES2024)
- [ ] Numeric separators: `1_000_000`

### 10.7 Reading the Spec
- [ ] ECMA-262: how to look up a feature
- [ ] MDN: compatibility tables, examples
- [ ] TC39 proposals: stages, GitHub
- [ ] Can I use / Node.js compatibility

---

# PART 2 — INTERVIEW QUESTIONS WITH ANSWERS (90+)

Every question includes the expected answer and what interviewers look for.

---

## Foundations & Types (1–15)

**1. What is the difference between `var`, `let`, and `const`?**
- [ ] `var`: function scope, hoisted (initialized `undefined`), redeclarable
- [ ] `let`: block scope, hoisted (TDZ), NOT redeclarable, reassignable
- [ ] `const`: block scope, hoisted (TDZ), NOT redeclarable, NOT reassignable (but objects/arrays are still mutable)
- [ ] Best: `const` by default, `let` when reassignment needed, avoid `var`

**2. What is the Temporal Dead Zone?**
- [ ] The period between entering a scope and the `let`/`const` declaration
- [ ] Accessing the variable during TDZ → ReferenceError
- [ ] `var` has no TDZ (hoisted with `undefined` instead)

**3. What are the 7 primitive types?**
- [ ] string, number, boolean, undefined, null, symbol, bigint
- [ ] Bonus: primitives are immutable and copied by value

**4. What is `typeof null` and why?**
- [ ] Returns `"object"` — a bug from the original JS implementation in 1995
- [ ] Cannot be fixed because it would break existing websites

**5. Name all falsy values.**
- [ ] `false`, `0`, `""` (empty string), `null`, `undefined`, `NaN`
- [ ] Everything else is truthy (including `[]`, `{}`, `"0"`, `"false"`)

**6. Difference between `==` and `===`?**
- [ ] `==` performs type coercion then compares (unpredictable)
- [ ] `===` compares type AND value without coercion (predictable)
- [ ] Always use `===` by default

**7. What is type coercion? Give an example.**
- [ ] Automatic conversion between types
- [ ] `"5" + 2` → `"52"` (number coerced to string because `+` concatenates)
- [ ] `"5" - 2` → `3` (string coerced to number because `-` is only numeric)

**8. What is NaN? How do you check for it?**
- [ ] "Not a Number" — result of failed numeric operations (e.g. `"abc" * 2`)
- [ ] `typeof NaN` → `"number"` (ironic)
- [ ] `NaN === NaN` → `false` (NaN is not equal to anything, including itself)
- [ ] Check with `Number.isNaN(val)` (strict) not `isNaN(val)` (coerces first)

**9. undefined vs null?**
- [ ] `undefined`: system-assigned; uninitialized variables, missing params, missing properties
- [ ] `null`: developer-assigned; intentional absence of value
- [ ] Simple rule: undefined → system; null → developer

**10. What are Symbols and why use them?**
- [ ] Unique, immutable primitive: `Symbol("desc")` — every call creates a unique symbol
- [ ] Use case: unique property keys (no accidental collisions)
- [ ] Well-known symbols customize language behavior (Symbol.iterator, Symbol.toPrimitive)

**11. Are primitives mutable or immutable?**
- [ ] Immutable — cannot be changed after creation
- [ ] `let s = "hello"; s[0] = "H";` → no effect; strings aren't modified
- [ ] Reassignment (`s = "Hello"`) creates a new value, doesn't modify the old one

**12. What does "copy by value" mean for primitives?**
- [ ] `let a = 5; let b = a;` → `b` is an independent copy
- [ ] Changing `b` does NOT affect `a`
- [ ] Objects behave differently (copy by reference)

**13. What is `Object.is()` and when would you use it?**
- [ ] Same-value equality: like `===` but handles two edge cases
- [ ] `Object.is(NaN, NaN)` → `true` (unlike `===`)
- [ ] `Object.is(+0, -0)` → `false` (unlike `===`)

**14. What is BigInt?**
- [ ] For integers larger than `Number.MAX_SAFE_INTEGER` (2^53 - 1)
- [ ] Created with `123n` or `BigInt(123)`
- [ ] Cannot mix with Number without explicit conversion: `1n + 2` → TypeError

**15. What is dynamic typing?**
- [ ] Variables can hold any type; type determined at runtime
- [ ] `let x = 10; x = "hello";` — valid; type changed from number to string
- [ ] Flexibility: fast development; risk: type-related bugs

---

## Functions, Scope & Closures (16–30)

**16. What is a closure?**
- [ ] A function that retains access to its lexical scope (outer variables) even after the outer function has returned
- [ ] Example: counter factory that keeps private count
- [ ] Use cases: data privacy, factory functions, callbacks, partial application

**17. Classic loop + setTimeout — what is the output?**
```js
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 0);
}
```
- [ ] Output: `3, 3, 3` — because `var` is function-scoped; all callbacks share the same `i`; by the time they run, `i` is 3
- [ ] Fix with `let`: `for (let i = ...)` — block scope creates new `i` for each iteration
- [ ] Fix with IIFE: `(function(j) { setTimeout(..., 0); })(i);`

**18. Explain the 4 rules for `this`.**
- [ ] **Default**: standalone call → `window` (non-strict) or `undefined` (strict)
- [ ] **Implicit**: `obj.method()` → `this` is `obj`
- [ ] **Explicit**: `call/apply/bind` → `this` is specified argument
- [ ] **new**: `new Fn()` → `this` is new empty object
- [ ] Precedence: new > explicit > implicit > default

**19. What does `bind` return? How is it different from `call`/`apply`?**
- [ ] `call(thisArg, a, b)`: invokes immediately with given `this` and args
- [ ] `apply(thisArg, [a, b])`: same as call but args as array
- [ ] `bind(thisArg, a)`: returns NEW function with `this` permanently bound; does NOT invoke

**20. Why don't arrow functions have their own `this`?**
- [ ] Arrow functions inherit `this` from enclosing lexical scope
- [ ] Designed for callbacks where you want parent's `this`
- [ ] Do NOT use for object methods that need their own `this`
- [ ] Cannot use as constructors (no `new`); no `arguments` object

**21. What is an IIFE?**
- [ ] Immediately Invoked Function Expression: `(function() { })();`
- [ ] Creates private scope; variables don't leak to global
- [ ] Historical: main encapsulation technique before ES modules

**22. What is a higher-order function?**
- [ ] Takes a function as argument AND/OR returns a function
- [ ] Built-in examples: `map`, `filter`, `reduce`, `sort`, `forEach`
- [ ] Custom: `function once(fn) { let called = false; return function(...args) { if (!called) { called = true; return fn(...args); } }; }`

**23. Function declaration vs expression?**
- [ ] Declaration: `function foo() {}` — hoisted (callable before its line)
- [ ] Expression: `const foo = function() {};` — NOT hoisted (TypeError if called before)
- [ ] Named expression: `const foo = function bar() {};` — `bar` only available inside the function (useful for recursion)

**24. What is the `arguments` object?**
- [ ] Array-like object available in non-arrow functions; contains all passed arguments
- [ ] Convert to array: `Array.from(arguments)` or `[...arguments]`
- [ ] Arrow functions do NOT have `arguments`; use rest parameters instead

**25. Default parameters and rest parameters?**
- [ ] Default: `function fn(a = 1, b = 2) {}` — used if argument is `undefined`
- [ ] Rest: `function fn(...args) {}` — collects remaining arguments into real array; must be last parameter
- [ ] Cannot have rest before another parameter: `(...args, last)` ✗

**26. What is hoisting?**
- [ ] JS moves declarations to top of scope before execution
- [ ] `var`: declaration hoisted, initialized `undefined`; `let`/`const`: declaration hoisted, NOT initialized (TDZ)
- [ ] Function declarations: fully hoisted; function expressions: follow variable rules

**27. What is scope chain?**
- [ ] When a variable isn't found in current scope, JS looks in the outer scope, then outer-outer, up to global
- [ ] Determined by where code is WRITTEN (lexical/static scoping), not where it's called
- [ ] Closures work because inner functions retain their scope chain

**28. What is lexical scope?**
- [ ] Scope determined by position in source code (where function is defined)
- [ ] Inner function can access outer function's variables; outer cannot access inner's
- [ ] This is why closures work

**29. try/catch/finally — how does it work?**
- [ ] `try`: code that might throw; `catch(err)`: handle error; `finally`: always runs (cleanup)
- [ ] `finally` runs even if try/catch has `return`
- [ ] Only catches runtime errors; syntax errors stop parsing before execution

**30. How do you create custom errors?**
- [ ] `class ValidationError extends Error { constructor(msg) { super(msg); this.name = "ValidationError"; } }`
- [ ] Use `instanceof` to catch specific types: `catch(e) { if (e instanceof ValidationError) ... }`

---

## Objects, Arrays & Data Structures (31–45)

**31. How does `reduce` work?**
- [ ] `array.reduce((accumulator, current, index, arr) => newAccumulator, initialValue)`
- [ ] Iterates through array, building up a single result
- [ ] Without initial value: first element is initial accumulator (can be risky with empty arrays)

**32. Implement `map` using `reduce`.**
```js
function myMap(arr, fn) {
  return arr.reduce((acc, val, i) => { acc.push(fn(val, i, arr)); return acc; }, []);
}
```

**33. `slice` vs `splice`?**
- [ ] `slice(start, end)`: returns new array; does NOT mutate; end is exclusive
- [ ] `splice(start, deleteCount, ...items)`: modifies original array; returns deleted items

**34. How to remove duplicates from an array?**
- [ ] `[...new Set(arr)]` — simplest
- [ ] `arr.filter((val, i) => arr.indexOf(val) === i)` — manual
- [ ] For objects: need custom comparison (e.g. by id)

**35. Shallow vs deep copy?**
- [ ] Shallow: copies top-level; nested objects still share references. Methods: `{...obj}`, `Object.assign({}, obj)`, `[...arr]`
- [ ] Deep: copies everything recursively. Methods: `structuredClone(obj)` (modern), `JSON.parse(JSON.stringify(obj))` (loses functions, dates, undefined), recursive manual copy
- [ ] `structuredClone` handles circular references; JSON method does not

**36. `Map` vs plain object?**
- [ ] Map: any key type (objects, functions); guaranteed insertion order; `.size` property; better for frequent add/delete
- [ ] Object: keys are strings/Symbols; simpler syntax; JSON-compatible; has prototype (can conflict)

**37. `WeakMap` vs `Map`?**
- [ ] WeakMap keys must be objects; weak references (GC can collect if no other reference)
- [ ] No iteration (`forEach`, `keys`, `values`, `entries` don't exist); no `.size`
- [ ] Use case: private data, caching without preventing garbage collection

**38. What is destructuring?**
- [ ] Extract values from arrays/objects into variables
- [ ] Array: `const [a, b, ...rest] = [1, 2, 3, 4];`
- [ ] Object: `const { name, age: years, country = "US" } = person;`
- [ ] Nested: `const { address: { city } } = person;`

**39. What is the spread operator?**
- [ ] `...` expands iterables: `[...arr]` (copy), `{...obj}` (copy), `fn(...args)` (spread args)
- [ ] Shallow copy only
- [ ] In objects: later properties overwrite earlier (`{...a, ...b}`)

**40. What are property descriptors?**
- [ ] Every property has: `value`, `writable`, `enumerable`, `configurable` (or `get`/`set` for accessors)
- [ ] `Object.defineProperty(obj, "key", { writable: false })` — make read-only
- [ ] `Object.freeze(obj)` — all properties non-writable and non-configurable (shallow)

**41. Array-like vs array?**
- [ ] Array-like: has `length` and indexed elements but not Array methods (`arguments`, `NodeList`)
- [ ] Convert: `Array.from(arrayLike)` or `[...arrayLike]`

**42. `for...in` vs `for...of`?**
- [ ] `for...in`: iterates over enumerable property **keys** (including prototype); for objects
- [ ] `for...of`: iterates over iterable **values**; for arrays, strings, Map, Set; NOT plain objects

**43. `Object.keys` vs `Object.entries` vs `for...in`?**
- [ ] `Object.keys(obj)`: own enumerable string keys (array)
- [ ] `Object.entries(obj)`: own enumerable [key, value] pairs
- [ ] `for...in`: own + inherited enumerable keys (need `hasOwnProperty` to filter)

**44. What is optional chaining?**
- [ ] `obj?.prop` returns `undefined` if `obj` is null/undefined instead of throwing
- [ ] Works for methods: `obj?.method?.()`, brackets: `obj?.["key"]`
- [ ] Short-circuits: rest of chain is not evaluated

**45. What is nullish coalescing `??`?**
- [ ] Returns right side only when left is `null` or `undefined`
- [ ] `0 ?? "default"` → `0` (0 is NOT null/undefined)
- [ ] `0 || "default"` → `"default"` (0 is falsy)
- [ ] Use `??` when 0, "", false are valid values

---

## Asynchronous (46–60)

**46. Explain the event loop.**
- [ ] JS is single-threaded with one call stack
- [ ] Async callbacks go to task queue (macrotask) or microtask queue
- [ ] Event loop: "Is call stack empty?" → run all microtasks → run one macrotask → repeat
- [ ] Microtasks: Promise callbacks, queueMicrotask; Macrotasks: setTimeout, setInterval, I/O

**47. What is the output?**
```js
console.log(1);
setTimeout(() => console.log(2), 0);
Promise.resolve().then(() => console.log(3));
console.log(4);
```
- [ ] Output: `1, 4, 3, 2`
- [ ] Sync first (1, 4) → microtask (Promise → 3) → macrotask (setTimeout → 2)

**48. What are the states of a Promise?**
- [ ] pending → fulfilled (with value) or rejected (with reason)
- [ ] Once settled, state is immutable
- [ ] `.then` handles fulfillment; `.catch` handles rejection; `.finally` runs either way

**49. `Promise.all` vs `Promise.allSettled`?**
- [ ] `.all`: resolves when ALL resolve; rejects immediately if ANY rejects (fail-fast)
- [ ] `.allSettled`: waits for ALL to settle; returns `[{status:"fulfilled",value}, {status:"rejected",reason}]`
- [ ] Use `.all` when you need everything; `.allSettled` when you want all results regardless of failures

**50. How does async/await work?**
- [ ] `async` function always returns a Promise
- [ ] `await` pauses execution until Promise settles; returns value on fulfill; throws on reject
- [ ] Syntactic sugar over Promises + `.then` chains

**51. How to run async operations in parallel?**
- [ ] `const [a, b] = await Promise.all([fetchA(), fetchB()]);`
- [ ] NOT: `const a = await fetchA(); const b = await fetchB();` — that's sequential

**52. Error handling in async/await?**
- [ ] `try { const data = await fetch(...); } catch (err) { handle(err); }`
- [ ] Or: `asyncFn().catch(err => handle(err));`
- [ ] Unhandled rejections become unhandledrejection events

**53. What is AbortController?**
- [ ] `const ctrl = new AbortController();` — creates signal
- [ ] Pass to fetch: `fetch(url, { signal: ctrl.signal })`
- [ ] `ctrl.abort()` cancels the fetch; throws AbortError

**54. setTimeout vs setInterval vs requestAnimationFrame?**
- [ ] `setTimeout`: run once after delay; `setInterval`: run repeatedly; both have minimum delay (~4ms in browsers)
- [ ] `requestAnimationFrame`: fires before next repaint (~16ms / 60fps); best for animations; pauses in background tabs

**55. Microtasks vs macrotasks?**
- [ ] Microtasks: Promise.then/catch/finally, queueMicrotask — run BEFORE next macrotask; ALL microtasks drain before proceeding
- [ ] Macrotasks: setTimeout, setInterval, I/O, UI events — run one at a time between microtask drains

**56. What is callback hell?**
- [ ] Deeply nested callbacks making code hard to read/maintain
- [ ] Solved by: Promises (chaining), async/await (flat structure), named functions

**57. How do you promisify a callback-based function?**
```js
function delay(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}
```

**58. What does `fetch` NOT throw on?**
- [ ] 4xx and 5xx HTTP errors — `fetch` only rejects on network failure
- [ ] Must check `response.ok` or `response.status` manually

**59. What is CORS?**
- [ ] Cross-Origin Resource Sharing: browser blocks requests to different origins by default
- [ ] Server must send `Access-Control-Allow-Origin` header to permit
- [ ] Preflight (OPTIONS) request for non-simple methods/headers

**60. What is `Promise.any`?**
- [ ] Resolves with first fulfilled Promise; ignores rejections
- [ ] If ALL reject → `AggregateError` containing all rejection reasons

---

## OOP, Prototypes, Classes (61–70)

**61. What is the prototype chain?**
- [ ] Every object has `[[Prototype]]`; property lookup: own → prototype → prototype's prototype → null
- [ ] `Object.getPrototypeOf(obj)` to inspect; `Object.create(proto)` to set

**62. How does `new` work step by step?**
- [ ] 1. Creates new empty object
- [ ] 2. Sets its `[[Prototype]]` to Constructor.prototype
- [ ] 3. Calls constructor with `this` = new object
- [ ] 4. Returns the object (unless constructor explicitly returns a different object)

**63. `__proto__` vs `.prototype`?**
- [ ] `__proto__`: the actual prototype of an instance (legacy; use `Object.getPrototypeOf`)
- [ ] `.prototype`: property on constructor functions; becomes `__proto__` of instances created with `new`

**64. How are classes syntactic sugar?**
- [ ] `class Foo { method() {} }` is equivalent to `function Foo() {} Foo.prototype.method = function() {};`
- [ ] Classes add: cleaner syntax, `extends`/`super`, static, private fields (#), but same prototype mechanism underneath

**65. What is `super`?**
- [ ] In constructor: `super()` calls parent constructor (required before using `this` in subclass)
- [ ] In methods: `super.method()` calls parent's method

**66. Private fields `#`?**
- [ ] `#field` — only accessible inside the class body; true encapsulation
- [ ] Accessing from outside → SyntaxError
- [ ] Different from convention (`_field` which is still public)

**67. Static methods?**
- [ ] `static method() {}` — belongs to class, not instances
- [ ] Called as `ClassName.method()`, NOT `instance.method()`
- [ ] Use for utility/factory functions

**68. `instanceof` — how does it work?**
- [ ] Checks if `Constructor.prototype` exists in object's prototype chain
- [ ] Can be "fooled" by changing prototypes after creation
- [ ] `Symbol.hasInstance` can customize behavior

**69. Composition vs inheritance?**
- [ ] Inheritance: "is-a" (Dog extends Animal); creates tight coupling; deep hierarchies are fragile
- [ ] Composition: "has-a" (Dog has walkBehavior); combine small, focused pieces; more flexible
- [ ] Prefer composition when possible; use inheritance for clear "is-a" relationships

**70. Getters and setters?**
- [ ] `get prop() { return this._prop; }`, `set prop(val) { this._prop = val; }`
- [ ] Look like property access but run a function
- [ ] Use for validation, computed properties, lazy initialization

---

## Modules, Generators, Advanced (71–90)

**71. `export default` vs named export?**
- [ ] Default: one per module; import with any name: `import whatever from './mod.js'`
- [ ] Named: multiple per module; import with exact name or alias: `import { name as alias } from './mod.js'`
- [ ] Can have both in one module

**72. Dynamic `import()`?**
- [ ] `const mod = await import('./module.js');` — returns Promise<Module>
- [ ] Use for: code-splitting, conditional loading, lazy loading

**73. What does `"use strict"` change?**
- [ ] Assigning to undeclared variable throws (no accidental globals)
- [ ] `this` in standalone function is `undefined` (not window)
- [ ] Duplicate parameter names throw
- [ ] `delete` on non-configurable throws; `with` statement forbidden

**74. What is a generator?**
- [ ] `function* gen() { yield 1; yield 2; }` — pauses at each `yield`
- [ ] `gen.next()` → `{value: 1, done: false}`, `gen.next()` → `{value: 2, done: false}`, `gen.next()` → `{value: undefined, done: true}`
- [ ] Use: lazy sequences, infinite iterators, async flow control

**75. What is `Symbol.iterator`?**
- [ ] Well-known symbol that makes an object iterable
- [ ] Must return iterator with `next()` method returning `{value, done}`
- [ ] Used by `for...of`, spread, destructuring, `Array.from`

**76. What is a Proxy?**
- [ ] `new Proxy(target, { get(t, p) {}, set(t, p, v) {} })` — intercepts operations
- [ ] Use cases: validation (reject bad values), default values, logging, reactivity

**77. What is Reflect?**
- [ ] Built-in object with methods that match Proxy traps
- [ ] Use inside traps: `Reflect.get(target, prop)` to perform default behavior + add custom logic

**78. Implement debounce.**
```js
function debounce(fn, delay) {
  let timer;
  return function(...args) {
    clearTimeout(timer);
    timer = setTimeout(() => fn.apply(this, args), delay);
  };
}
```

**79. Implement throttle.**
```js
function throttle(fn, limit) {
  let lastCall = 0;
  return function(...args) {
    const now = Date.now();
    if (now - lastCall >= limit) {
      lastCall = now;
      fn.apply(this, args);
    }
  };
}
```

**80. What is a memory leak in JS? Example?**
- [ ] Memory that should be freed but isn't because references still exist
- [ ] Examples: detached DOM nodes with event listeners; closures holding large objects; forgotten setInterval; global variables

**81. `this` in setTimeout callback — what happens?**
- [ ] Regular function: `this` is `window` (non-strict) or `undefined` (strict) — NOT the object
- [ ] Fix: arrow function (inherits `this`), `.bind(this)`, or store `const self = this;`

**82. Deep clone without libraries?**
- [ ] `structuredClone(obj)` — handles circular references, dates, maps, sets (modern)
- [ ] `JSON.parse(JSON.stringify(obj))` — loses functions, undefined, dates (become strings), no circular refs
- [ ] Manual recursive: check type, handle arrays/objects/dates separately

**83. `JSON.stringify` — what types are NOT supported?**
- [ ] Functions: omitted; `undefined`: omitted; `Symbol`: omitted; `BigInt`: throws
- [ ] `NaN`/`Infinity`: become `null`; `Date`: becomes ISO string
- [ ] Custom: implement `toJSON()` method on object

**84. `Object.hasOwn` vs `hasOwnProperty`?**
- [ ] `Object.hasOwn(obj, key)` — static method; works even if object doesn't inherit from Object.prototype
- [ ] `obj.hasOwnProperty(key)` — can be overridden; fails if `Object.create(null)`

**85. How to prevent XSS?**
- [ ] Never use `innerHTML` with user input; use `textContent` instead
- [ ] Sanitize/escape HTML entities before inserting
- [ ] Use Content-Security-Policy headers; avoid `eval()`

**86. Write a simple iterable.**
```js
const range = {
  from: 1, to: 5,
  [Symbol.iterator]() {
    let current = this.from;
    return {
      next: () => current <= this.to
        ? { value: current++, done: false }
        : { done: true }
    };
  }
};
for (const n of range) console.log(n); // 1, 2, 3, 4, 5
```

**87–90: Behavioral**
- [ ] 87. Describe debugging a tricky bug: scope/this/async issue → isolate with console.log → use breakpoints → identify root cause
- [ ] 88. Staying updated: JavaScript Weekly, TC39 proposals, MDN, conference talks
- [ ] 89. Explain closure to a junior: "A function that remembers the variables around it, even after the outer function is done"
- [ ] 90. One feature you'd add to JS: (open-ended; shows engagement with the language)

---

# PART 3 — PRACTICE PROBLEMS (Detailed)

## Phase 1: Foundations

**Easy**
- [ ] **Type Logger**: Create variables `name`, `age`, `isStudent`, `city`; log `typeof` each. Expected: practice typeof.
- [ ] **null vs undefined**: Declare `let a;` and `let b = null;` Log both. Explain the difference.
- [ ] **Immutable Check**: `let s = "hello"; s[0] = "H"; console.log(s);` → still "hello". Why? Strings are immutable.
- [ ] **Predict typeof**: `typeof "Hi"`, `typeof 42`, `typeof true`, `typeof undefined`, `typeof null`, `typeof NaN`. Guess before running.
- [ ] **Copy by value**: `let a = 10; let b = a; b = 20; console.log(a);` → 10. Why? Primitives copy by value.

**Medium**
- [ ] **NaN Generator**: Write 3 expressions that produce NaN. Examples: `"abc" * 2`, `parseInt("xyz")`, `0/0`, `undefined + 1`.
- [ ] **Truthy/Falsy Check**: Which enter `if` block? `"hello"`, `0`, `[]`, `null`, `100`, `""`, `"0"`, `NaN`, `{}`. Write code to test.
- [ ] **Coercion Predict**: Predict: `"5"+2`, `"5"-2`, `0==false`, `0===false`, `null==undefined`, `null===undefined`, `Boolean("")`, `Boolean("0")`.
- [ ] **Fix the Bug**: `if (userInput == 0)` — user types "0" (string); this is risky. Why? Fix with `===`.
- [ ] **Explicit Convert**: Convert `"25"` to number, `42` to string, `0` to boolean, `""` to boolean. Use `Number()`, `String()`, `Boolean()`.

**Hard**
- [ ] **Profile Card**: Store name, age, country, isEmployed. Log formatted: `"Hello, my name is Alex. I am 25. Employed: true."` Use template literals.
- [ ] **Data Reporter**: Create one variable of each primitive type (all 7). Log value and typeof for each. Proves you know them all.
- [ ] **Login Validator**: Store `enteredPassword` and `savedPassword`. Compare with `==` and `===`. Show when they differ and why.

---

## Phase 2: Data Structures

**Easy**
- [ ] **Sum Array**: `[1,2,3,4,5]` → sum with reduce. Then with for loop. Compare.
- [ ] **Remove Duplicates**: `[1,2,2,3,3,4]` → `[1,2,3,4]`. Use Set. Then use filter+indexOf.
- [ ] **Flatten**: `[[1,2],[3,[4,5]]]` → `[1,2,3,4,5]`. Use `flat(Infinity)`. Then recursive.
- [ ] **Destructure Object**: `const {name, age: years, country = "US"} = person;` — practice rename + default.
- [ ] **Merge Objects**: `{...a, ...b}` — what happens when keys overlap?

**Medium**
- [ ] **Implement map with reduce**: `function myMap(arr, fn) { return arr.reduce((acc, v, i) => [...acc, fn(v, i)], []); }`
- [ ] **Implement filter with reduce**: Same pattern but only push if predicate true.
- [ ] **Group By**: Given `[{type:"a",val:1},{type:"b",val:2},{type:"a",val:3}]` → `{a:[...], b:[...]}`. Use reduce or Object.groupBy.
- [ ] **Deep Clone**: Clone `{a:1, b:{c:2}}` so changing clone.b.c doesn't affect original. Use structuredClone or recursive.
- [ ] **Reverse String**: 3 ways: split+reverse+join, for loop, reduce.
- [ ] **Capitalize Words**: `"hello world"` → `"Hello World"`. Split, map, join.
- [ ] **Count Occurrences**: `[1,2,2,3,3,3]` → `{1:1, 2:2, 3:3}`. Use reduce.

**Hard**
- [ ] **Implement flat(depth)**: Recursive; handle depth parameter; return new array.
- [ ] **Debounce**: `function debounce(fn, delay)` — clear previous timeout, set new one. Test with input field.
- [ ] **Throttle**: `function throttle(fn, limit)` — only execute once per limit ms. Test with scroll.
- [ ] **Curry**: `function curry(fn)` — `curry(add)(1)(2)(3)` → 6. Handle arbitrary arity.
- [ ] **Compose/Pipe**: `compose(f, g, h)(x)` → `f(g(h(x)))`. Pipe is reverse order.

---

## Phase 3: Functions & Closures

**Easy**
- [ ] **Counter**: Closure that returns `{increment, decrement, getCount}` with private count.
- [ ] **Factory**: `createPerson(name, age)` returning `{name, age, greet() {}}`.
- [ ] **Fix Loop**: `for (var i=0; i<3; i++) setTimeout(()=>console.log(i), 0)` → outputs 3,3,3. Fix it.
- [ ] **call/apply/bind**: Object `user` with `greet`. Call greet with different `this` using all three.

**Medium**
- [ ] **Once**: `function once(fn)` — returned function only executes fn the first time; subsequent calls return first result.
- [ ] **Memoize**: `function memoize(fn)` — cache results by arguments; return cached if same args.
- [ ] **Partial Application**: `function partial(fn, ...presetArgs)` — return function that fills remaining args.
- [ ] **Event Emitter**: `class EventEmitter` with `on(event, handler)`, `emit(event, ...data)`, `off(event, handler)`.

**Hard**
- [ ] **Implement Promise (basic)**: Support `new MyPromise((resolve, reject) => {})`, `.then(onFulfilled)`, `.catch(onRejected)`, chaining.
- [ ] **Recursive Flatten**: `flatten([1,[2,[3,[4]]]])` → `[1,2,3,4]` without using `.flat()`.
- [ ] **Trampoline**: Convert recursive factorial to trampolined version to avoid stack overflow.

---

## Phase 4: Async

**Easy**
- [ ] **Fetch JSON**: `fetch('https://jsonplaceholder.typicode.com/posts/1').then(r=>r.json()).then(console.log)`. Then rewrite with async/await.
- [ ] **Sequential Fetch**: Fetch post 1, then use its userId to fetch user. Sequential with await.
- [ ] **Parallel Fetch**: Fetch posts 1, 2, 3 simultaneously with `Promise.all`.

**Medium**
- [ ] **Retry**: `async function fetchWithRetry(url, retries = 3)` — retry on failure up to N times.
- [ ] **Timeout**: Race fetch against a timeout: `Promise.race([fetch(url), delay(5000).then(() => { throw new Error("Timeout") })])`.
- [ ] **Promisify**: `function delay(ms) { return new Promise(resolve => setTimeout(resolve, ms)); }`
- [ ] **Async Map**: `async function asyncMap(arr, asyncFn)` — run asyncFn on each item, return array of results.

**Hard**
- [ ] **Promise Pool**: `async function pool(tasks, limit)` — run at most `limit` tasks concurrently; when one finishes, start next.
- [ ] **Implement Promise.allSettled**: Manually track fulfilled/rejected for each promise.
- [ ] **Cancellable Chain**: Fetch → transform → save; cancel at any point with AbortController.

---

## Phase 5+: OOP, Generators, DOM, Advanced

**Easy**
- [ ] **Class with Getter/Setter**: `class User` with `#name`; get/set validates name length.
- [ ] **Generator Fibonacci**: `function* fib() { let a=0, b=1; while(true) { yield a; [a,b]=[b,a+b]; } }`
- [ ] **DOM Toggle**: Button that toggles a class on an element using `classList.toggle`.
- [ ] **Event Listener**: Add click listener to button; show message.

**Medium**
- [ ] **Custom Iterable**: Object with `[Symbol.iterator]` that yields a range of numbers.
- [ ] **Proxy Validation**: `new Proxy(user, { set(t, p, v) { if (p === "age" && typeof v !== "number") throw TypeError(); ... } })`.
- [ ] **Event Delegation**: Single listener on `<ul>` that handles clicks on any `<li>`.
- [ ] **localStorage Wrapper**: `class Storage { get(key) {} set(key, val) {} remove(key) {} }` with JSON parse/stringify.

**Hard**
- [ ] **Observable**: `class Observable { subscribe(observer) {} }` with `next`, `error`, `complete`.
- [ ] **SPA Router**: Listen for `hashchange`; render different content based on `location.hash`.
- [ ] **Virtual Scroll**: Only render visible items in a long list; calculate positions based on scroll offset.
- [ ] **Implement `bind`**: `Function.prototype.myBind = function(ctx, ...args) { ... }`.

---

# PART 4 — PROJECT TO-DO LIST (Detailed)

## Beginner Projects (After Phase 1–2)

- [ ] **Console Profile Card**: Store name, age, country, isEmployed; log formatted message with template literals. Skills: variables, types, console.log, template literals.
- [ ] **Type Inspector**: Create variables of all 7 primitive types; display value + type in console. Skills: primitives, typeof.
- [ ] **Simple Calculator**: Two numbers + operator; return result. Handle division by zero, invalid input. Skills: operators, conditionals, type checking.
- [ ] **Greeting Generator**: Input name → output personalized greeting with time-based message (morning/afternoon/evening). Skills: Date, conditionals, strings.
- [ ] **Array Toolkit**: Functions for sum, average, max, min, removeDuplicates, flatten. All in one file. Skills: array methods, reduce.
- [ ] **Object CRUD**: Create person object; add/update/delete properties; display as formatted string. Skills: objects, destructuring, template literals.
- [ ] **String Utilities**: Functions: reverse, capitalize, countVowels, truncate, slugify. Skills: string methods, split, join, regex.

## Intermediate Projects (After Phase 3–5)

- [ ] **Todo App (Console → DOM)**: Start in console (add, toggle, delete, list). Then build DOM version with localStorage. Skills: arrays, objects, closures, DOM, events, localStorage.
- [ ] **Timer / Stopwatch**: Start, pause, reset, lap times. Display updating time. Skills: setInterval, DOM updates, state management.
- [ ] **Form Validator**: Required fields, email format, min/max length, password match, real-time error display. Skills: regex, events, DOM manipulation.
- [ ] **Image Gallery**: Thumbnails grid → click for lightbox → prev/next/close. Keyboard navigation (arrow keys, Esc). Skills: DOM, events, event delegation, CSS interaction.
- [ ] **Fetch & Display**: Pick a public API (weather, posts, users); fetch data; display cards; search/filter. Skills: fetch, async/await, DOM, error handling.
- [ ] **Event Emitter Library**: `class EventEmitter { on(event, fn) {} off(event, fn) {} emit(event, ...data) {} once(event, fn) {} }`. Write tests. Skills: closures, callbacks, classes, Map/Set.
- [ ] **Class-Based Game**: Tic-tac-toe or simple quiz: Player class, Game class, Board class. DOM rendering. Skills: classes, inheritance, DOM, events.

## Advanced Projects (After Phase 6–9)

- [ ] **Debounce/Throttle Visualizer**: Input field + scroll area. Show when debounced/throttled functions fire vs raw events. Skills: closures, timing, DOM, visualization.
- [ ] **Infinite Scroll Feed**: Fetch paginated data (JSONPlaceholder); IntersectionObserver triggers next page; loading states. Skills: async/await, observers, DOM, performance.
- [ ] **Vanilla SPA**: Hash-based or history-based routing; multiple "pages" rendered from JS; shared layout. Skills: history API, event listeners, module pattern, DOM.
- [ ] **Drag & Drop List**: Reorder items via drag and drop; persist order in localStorage. Skills: native DnD API, events, DOM, storage.
- [ ] **Notes App**: Create, edit, delete, search, tag notes; localStorage persistence; markdown preview (optional). Skills: CRUD, DOM, storage, string manipulation.
- [ ] **Async Data Layer**: Fetch with retry, timeout, caching, request deduplication. Reusable utility module. Skills: Promises, async patterns, closures, modules.
- [ ] **Custom Iterable API Client**: Paginated API as async iterable; `for await (const page of apiClient)`. Skills: async generators, Symbol.asyncIterator, fetch.
- [ ] **Proxy-Based Form**: Form object with Proxy traps for validation, change tracking, dirty state. Skills: Proxy, Reflect, DOM.

## Capstone / Portfolio Projects

- [ ] **Full Todo SPA**: Routing, localStorage, filter (all/active/completed), animations, keyboard shortcuts. Production quality. Skills: everything from Phase 1–9.
- [ ] **Weather Dashboard**: Multiple cities; current + forecast; geolocation; responsive. Skills: fetch, async, DOM, geolocation, error handling.
- [ ] **Expense Tracker**: Add expenses; categories; date range filter; totals and breakdowns; chart (optional). Skills: arrays, objects, reduce, DOM, storage, dates.
- [ ] **Quiz Application**: Fetch questions from API; timer per question; score tracking; review answers. Skills: async, DOM, state, timers.
- [ ] **REST Client UI**: CRUD interface for JSONPlaceholder (or similar): list, create, edit, delete with confirmation. Skills: fetch, async, DOM, forms.
- [ ] **Pomodoro Timer**: Work/break sessions; customizable durations; notification on completion; session history. Skills: timers, Notification API, DOM, storage.
- [ ] **Markdown Previewer**: Textarea input → live rendered preview (parse basic markdown: headers, bold, italic, lists, code). Skills: regex, string parsing, DOM, innerHTML (safe since user's own input).
- [ ] **Open Source Contribution**: Find a JS project on GitHub; fix a bug or add a small feature; submit PR. Skills: real-world codebase navigation, git, collaboration.

---

# PART 5 — QUICK REFERENCE

| Phase | Focus | Key concepts |
|-------|-------|-------------|
| 1 | Foundations | Syntax, variables, types, coercion, operators, control flow, functions |
| 2 | Data Structures | Array, Object, String, Number, Math, Date, JSON, RegExp, Map, Set |
| 3 | Functions Deep | Closures, this, arrow, default/rest, callbacks, IIFE, errors |
| 4 | Async | Event loop, Promises, async/await, fetch |
| 5 | OOP | Prototypes, classes, extends, super, private, composition |
| 6 | Iteration | Symbol.iterator, generators, async generators, for await |
| 7 | Modules | import/export, dynamic import, strict mode, globalThis |
| 8 | Meta | Proxy, Reflect, well-known Symbols |
| 9 | Browser | DOM, BOM, events, delegation, storage, Web APIs |
| 10 | Advanced | Performance, security, recursion, Typed Arrays, Intl, modern features |

---

# Resources

- **Spec**: [ECMA-262](https://tc39.es/ecma262/)
- **Docs**: [MDN JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
- **Proposals**: [TC39 GitHub](https://github.com/tc39/proposals)
- **Books**: *You Don't Know JS* (YDKJS), *Eloquent JavaScript*, *JavaScript: The Good Parts*
- **Practice**: Codewars, LeetCode (JS), freeCodeCamp — all in pure JavaScript
- **Stay updated**: [JavaScript Weekly](https://javascriptweekly.com/), TC39 meeting notes

---

*Track progress with checkboxes. Refer to js.md for beginner-friendly explanations of each topic. Build projects, solve problems, answer interview questions out loud.*
