# 2.4 Numbers and Math

## What is a Number?

In JavaScript, **numbers** are a primitive data type representing both integers and floating-point values. JavaScript uses the **IEEE 754 double-precision 64-bit format**, which means all numbers are stored as floating-point internally, even integers.

```javascript
const integer = 42;
const float = 3.14;
const scientific = 1.23e5; // 123000
const negative = -10;

console.log(typeof 42);      // "number"
console.log(typeof 3.14);    // "number"
console.log(42 === 42.0);    // true — they're the same
```

---

## 1. IEEE 754 and the Safe Integer Range

### IEEE 754 Double-Precision Format

JavaScript stores all numbers as 64-bit floating-point values:
- **1 bit**: sign
- **11 bits**: exponent
- **52 bits**: mantissa (fractional part)

This means JavaScript can precisely represent integers only up to $2^{53} - 1$.

### Safe Integer Range

```javascript
// Maximum safe integer
console.log(Number.MAX_SAFE_INTEGER);  // 9007199254740991 (2^53 - 1)

// Minimum safe integer
console.log(Number.MIN_SAFE_INTEGER);  // -9007199254740991

// Safe range for precise integer operations
const maxSafe = 9007199254740991;
const tooLarge = 9007199254740992;
const evenLarger = 9007199254740993;

console.log(tooLarge === evenLarger); // true — precision lost!
console.log(tooLarge);                // 9007199254740992
console.log(evenLarger);              // 9007199254740992 — same value!

// Practical impact
const accountBalance = 9007199254740991; // Max safe amount
const deposit = 2;
console.log(accountBalance + deposit); // 9007199254740992 — incorrect!
```

### Special Number Values

```javascript
// Infinity
console.log(Number.POSITIVE_INFINITY); // Infinity
console.log(Number.NEGATIVE_INFINITY); // -Infinity
console.log(1 / 0);                    // Infinity
console.log(-1 / 0);                   // -Infinity
console.log(Infinity + 1);             // Infinity
console.log(Infinity - Infinity);      // NaN

// NaN (Not-a-Number)
console.log(Number.NaN);               // NaN
console.log(0 / 0);                    // NaN
console.log(Math.sqrt(-1));            // NaN
console.log(NaN === NaN);              // false (special case!)
```

---

## 2. Parsing Numbers

### `Number(value)`
Converts value to number or returns `NaN`:

```javascript
// From strings
console.log(Number('42'));             // 42
console.log(Number('3.14'));           // 3.14
console.log(Number('1e5'));            // 100000
console.log(Number('0xFF'));           // 255 (hex)
console.log(Number('0b101'));          // 5 (binary)
console.log(Number('0o77'));           // 63 (octal)

// Whitespace is trimmed
console.log(Number('  42  '));         // 42

// Invalid strings return NaN
console.log(Number('hello'));          // NaN
console.log(Number('12abc'));          // NaN

// From other types
console.log(Number(true));             // 1
console.log(Number(false));            // 0
console.log(Number(null));             // 0
console.log(Number(undefined));        // NaN

// Empty string is special
console.log(Number(''));               // 0

// Booleans
console.log(Number(true));             // 1
console.log(Number(false));            // 0
```

### `parseInt(string, radix)`
**Always specify radix!** Parses first valid integer from string:

```javascript
// Without radix (DANGEROUS in old code)
console.log(parseInt('10'));           // 10
console.log(parseInt('010'));          // 10 (not 8 in modern JS, but was octal!)

// With radix (ALWAYS recommend)
console.log(parseInt('10', 10));       // 10 (decimal)
console.log(parseInt('10', 2));        // 2 (binary)
console.log(parseInt('10', 8));        // 8 (octal)
console.log(parseInt('10', 16));       // 16 (hexadecimal)

// Parsing until invalid character
console.log(parseInt('42abc', 10));    // 42 — stops at first non-digit
console.log(parseInt('abc42', 10));    // NaN — starts with invalid

// Hex parsing
console.log(parseInt('FF', 16));       // 255
console.log(parseInt('0xFF', 16));     // 255
console.log(parseInt('FF'));           // NaN — no radix defaults to 10!

// Floating-point strings
console.log(parseInt('3.14', 10));     // 3 — decimal point stops parsing
console.log(parseFloat('3.14'));       // 3.14 — better for floats

// Radix range (2-36)
console.log(parseInt('Z', 36));        // 35
console.log(parseInt('10', 1));        // NaN — radix too small
console.log(parseInt('10', 37));       // NaN — radix too large

// Whitespace is trimmed
console.log(parseInt('  42  ', 10));   // 42
```

### `parseFloat(string)`
Parses floating-point number from string:

```javascript
// Decimal numbers
console.log(parseFloat('3.14'));       // 3.14
console.log(parseFloat('3.14abc'));    // 3.14 — stops at first invalid

// Scientific notation
console.log(parseFloat('1.23e5'));     // 123000
console.log(parseFloat('1.23e-5'));    // 0.0000123

// Leading whitespace is trimmed
console.log(parseFloat('  3.14  '));   // 3.14

// Only first valid number
console.log(parseFloat('3.14 2.71'));  // 3.14

// Invalid returns NaN
console.log(parseFloat('abc'));        // NaN
console.log(parseFloat(''));           // NaN

// Difference from Number()
console.log(Number('3.14abc'));        // NaN
console.log(parseFloat('3.14abc'));    // 3.14
```

---

## 3. Checking Number Types

### `isNaN(value)` vs `Number.isNaN(value)`

⚠️ **Gotcha**: `isNaN()` does type coercion, `Number.isNaN()` is strict

```javascript
// Global isNaN() — does coercion
console.log(isNaN(NaN));               // true
console.log(isNaN('hello'));           // true — converts to NaN
console.log(isNaN('42'));              // false — converts to 42
console.log(isNaN(undefined));         // true — converts to NaN
console.log(isNaN(null));              // false — null converts to 0!
console.log(isNaN(true));              // false — true converts to 1

// Number.isNaN() — strict, no coercion
console.log(Number.isNaN(NaN));        // true
console.log(Number.isNaN('hello'));    // false — not NaN type
console.log(Number.isNaN('42'));       // false
console.log(Number.isNaN(undefined));  // false
console.log(Number.isNaN(null));       // false

// Which to use?
// ✅ Use Number.isNaN() for strict checking
// ❌ Avoid global isNaN() — too many false positives
```

### `Number.isFinite(value)`
Returns true only for finite numbers (not `Infinity`, not `NaN`):

```javascript
console.log(Number.isFinite(42));      // true
console.log(Number.isFinite(3.14));    // true
console.log(Number.isFinite(Infinity)); // false
console.log(Number.isFinite(-Infinity)); // false
console.log(Number.isFinite(NaN));     // false

// Global isFinite() does coercion
console.log(isFinite('42'));           // true — converts to 42
console.log(isFinite('hello'));        // false
console.log(Number.isFinite('42'));    // false — strict, no conversion

// Practical use
function process(value) {
  if (!Number.isFinite(value)) {
    throw new Error('Must be a finite number');
  }
  return value * 2;
}

console.log(process(21));              // 42
// process(Infinity); // Error
// process(NaN); // Error
```

### `Number.isInteger(value)`
Returns true if value is a number and has no fractional part:

```javascript
console.log(Number.isInteger(42));     // true
console.log(Number.isInteger(42.0));   // true — 42.0 is integer
console.log(Number.isInteger(42.5));   // false
console.log(Number.isInteger(3.14));   // false
console.log(Number.isInteger(Infinity)); // false
console.log(Number.isInteger(NaN));    // false

// Type checking matters
console.log(Number.isInteger('42'));   // false — string, not number
console.log(Number.isInteger(true));   // false
console.log(Number.isInteger(null));   // false

// Practical use
function arrayIndex(i) {
  if (!Number.isInteger(i) || i < 0) {
    throw new Error('Index must be non-negative integer');
  }
  return i;
}

console.log(arrayIndex(5));            // 5
// arrayIndex(5.5); // Error
// arrayIndex(-1); // Error
```

### `Number.isSafeInteger(value)`
Returns true if value is within safe integer range:

```javascript
const safe = 42;
const unsafe = 9007199254740992;

console.log(Number.isSafeInteger(42)); // true
console.log(Number.isSafeInteger(Number.MAX_SAFE_INTEGER)); // true
console.log(Number.isSafeInteger(Number.MIN_SAFE_INTEGER)); // true
console.log(Number.isSafeInteger(unsafe)); // false

// Precision is lost beyond safe range
const max = Number.MAX_SAFE_INTEGER;
console.log(Number.isSafeInteger(max)); // true
console.log(Number.isSafeInteger(max + 1)); // false
console.log(Number.isSafeInteger(max + 2)); // false
console.log((max + 1) === (max + 2)); // true — both same!

// Practical use
function bankTransaction(amount) {
  if (!Number.isSafeInteger(amount)) {
    throw new Error('Amount must be safe integer (cents)');
  }
  // Process transaction
}
```

---

## 4. Number Conversion and Formatting

### `toString(radix)`
Converts number to string in different bases:

```javascript
// Decimal (radix 10, default)
const num = 255;
console.log(num.toString());           // '255'
console.log(num.toString(10));         // '255'

// Binary (radix 2)
console.log(num.toString(2));          // '11111111'

// Octal (radix 8)
console.log(num.toString(8));          // '377'

// Hexadecimal (radix 16)
console.log(num.toString(16));         // 'ff'

// Other bases
console.log(num.toString(36));         // '73' (base-36, max)
console.log(100.toString(3));          // '10201' (base-3)

// Edge cases
console.log((1).toString());           // '1' — need parentheses for literals
console.log(1.toString());             // Error — dot interpreted as decimal
console.log((1.5).toString(2));        // Error — can't convert decimals

// Practical: color conversions
const red = 255;
const green = 128;
const blue = 64;
const hex = '#' + red.toString(16).padStart(2, '0') +
                  green.toString(16).padStart(2, '0') +
                  blue.toString(16).padStart(2, '0');
console.log(hex); // '#ff8040'
```

### `toFixed(digits)`
Formats number with fixed decimal places (rounds):

```javascript
const num = 3.14159;

console.log(num.toFixed());            // '3' — default 0 decimals
console.log(num.toFixed(0));           // '3'
console.log(num.toFixed(2));           // '3.14'
console.log(num.toFixed(5));           // '3.14159'
console.log(num.toFixed(10));          // '3.1415900000' — pads with zeros

// Returns string!
const result = num.toFixed(2);
console.log(typeof result);            // "string"
console.log(result + 1);               // '3.141' (string concatenation)

// Rounding behavior
console.log((1.005).toFixed(2));       // '1.00' or '1.01'? (banker's rounding)
console.log((1.015).toFixed(2));       // '1.01' or '1.02'?

// Practical: currency formatting
const price = 19.9;
console.log('$' + price.toFixed(2));   // '$19.90'

const total = 123.456;
console.log('€' + total.toFixed(2));   // '€123.46'
```

### `toExponential(digits)`
Returns string in exponential (scientific) notation:

```javascript
const num = 123456;

console.log(num.toExponential());      // '1.23456e+5'
console.log(num.toExponential(0));     // '1e+5'
console.log(num.toExponential(2));     // '1.23e+5'
console.log(num.toExponential(5));     // '1.23456e+5'

// With decimals
const decimal = 0.00123;
console.log(decimal.toExponential());  // '1.23e-3'
console.log(decimal.toExponential(2)); // '1.23e-3'

// Practical: scientific calculations
const lightSpeed = 299792458; // m/s
console.log(lightSpeed.toExponential(2)); // '2.99e+8'
```

### `toPrecision(digits)`
Returns string with specified total digits (significant figures):

```javascript
const num = 123.456;

console.log(num.toPrecision());        // '123.456'
console.log(num.toPrecision(1));       // '1e+2' — 1 significant digit
console.log(num.toPrecision(3));       // '123' — 3 significant digits
console.log(num.toPrecision(5));       // '123.46' — 5 significant digits
console.log(num.toPrecision(8));       // '123.45600' — pads with zeros

// With small numbers
const small = 0.000456;
console.log(small.toPrecision(2));     // '4.6e-4'
console.log(small.toPrecision(3));     // '4.56e-4'

// Practical: engineering measurements
const measurement = 1234.5678;
console.log(measurement.toPrecision(4)); // '1235' — 4 significant figures
```

---

## 5. The Math Object

The **Math** object provides mathematical constants and functions:

### Math Constants

```javascript
console.log(Math.PI);                  // 3.141592653589793
console.log(Math.E);                   // 2.718281828459045 (Euler's number)
console.log(Math.LN2);                 // Natural log of 2
console.log(Math.LN10);                // Natural log of 10
console.log(Math.LOG2E);               // Log base 2 of E
console.log(Math.LOG10E);              // Log base 10 of E
console.log(Math.SQRT1_2);             // √(1/2)
console.log(Math.SQRT2);               // √2
```

### Absolute Value: `Math.abs(x)`

```javascript
console.log(Math.abs(42));             // 42
console.log(Math.abs(-42));            // 42
console.log(Math.abs(0));              // 0
console.log(Math.abs(-0));             // 0

// With infinity
console.log(Math.abs(Infinity));       // Infinity
console.log(Math.abs(-Infinity));      // Infinity

// Practical: distance calculation
const start = 10;
const end = 3;
const distance = Math.abs(end - start);
console.log(distance); // 7
```

### Sign: `Math.sign(x)`
Returns 1, -1, or 0 based on sign:

```javascript
console.log(Math.sign(42));            // 1 (positive)
console.log(Math.sign(-42));           // -1 (negative)
console.log(Math.sign(0));             // 0
console.log(Math.sign(-0));            // -0 (special case)
console.log(Math.sign(NaN));           // NaN

// Practical: direction determination
const direction = Math.sign(target - current);
if (direction === 1) {
  console.log('Move right');
} else if (direction === -1) {
  console.log('Move left');
} else {
  console.log('At target');
}
```

### Rounding Functions

#### `Math.floor(x)` — Round Down
```javascript
console.log(Math.floor(3.7));          // 3
console.log(Math.floor(3.2));          // 3
console.log(Math.floor(-3.7));         // -4 (still down!)
```

#### `Math.ceil(x)` — Round Up
```javascript
console.log(Math.ceil(3.2));           // 4
console.log(Math.ceil(3.7));           // 4
console.log(Math.ceil(-3.2));          // -3 (up from negative)
```

#### `Math.round(x)` — Round to Nearest
```javascript
console.log(Math.round(3.5));          // 4 (rounds up at .5)
console.log(Math.round(3.4));          // 3
console.log(Math.round(-3.5));         // -3 (rounds toward positive)
```

#### `Math.trunc(x)` — Remove Decimal Part
```javascript
console.log(Math.trunc(3.7));          // 3
console.log(Math.trunc(-3.7));         // -3 (just removes decimal)
```

### Comparison:

```javascript
const num = 3.7;
const neg = -3.7;

console.log(Math.floor(num));  // 3
console.log(Math.ceil(num));   // 4
console.log(Math.round(num));  // 4
console.log(Math.trunc(num));  // 3

console.log(Math.floor(neg));  // -4 (toward -∞)
console.log(Math.ceil(neg));   // -3 (toward +∞)
console.log(Math.round(neg));  // -4
console.log(Math.trunc(neg));  // -3 (toward 0)

// Practical: pagination
function getPageCount(totalItems, itemsPerPage) {
  return Math.ceil(totalItems / itemsPerPage);
}
console.log(getPageCount(25, 10)); // 3 pages
```

### Min and Max: `Math.min()` and `Math.max()`

```javascript
console.log(Math.min(10, 5, 20, 3));   // 3
console.log(Math.max(10, 5, 20, 3));   // 20

// With arrays (use spread)
const nums = [10, 5, 20, 3];
console.log(Math.min(...nums));        // 3
console.log(Math.max(...nums));        // 20

// Single value
console.log(Math.min(42));             // 42
console.log(Math.max(42));             // 42

// With NaN
console.log(Math.min(10, NaN));        // NaN
console.log(Math.max(10, NaN));        // NaN

// Practical: clamping values
function clamp(value, min, max) {
  return Math.min(Math.max(value, min), max);
}
console.log(clamp(5, 0, 10));          // 5
console.log(clamp(15, 0, 10));         // 10 (clamped)
console.log(clamp(-5, 0, 10));         // 0 (clamped)
```

### Powers and Roots

#### `Math.pow(base, exponent)`
```javascript
console.log(Math.pow(2, 3));           // 8
console.log(Math.pow(2, 10));          // 1024
console.log(Math.pow(10, 2));          // 100

// With negative exponent
console.log(Math.pow(2, -1));          // 0.5
console.log(Math.pow(10, -2));         // 0.01

// Alternative: use ** operator
console.log(2 ** 3);                   // 8 (exponentiation operator)
```

#### `Math.sqrt(x)` — Square Root
```javascript
console.log(Math.sqrt(4));             // 2
console.log(Math.sqrt(16));            // 4
console.log(Math.sqrt(2));             // 1.414...
console.log(Math.sqrt(-1));            // NaN (no negative roots)

// Practical: distance formula
function distance(x1, y1, x2, y2) {
  const dx = x2 - x1;
  const dy = y2 - y1;
  return Math.sqrt(dx * dx + dy * dy);
}
console.log(distance(0, 0, 3, 4)); // 5 (3-4-5 triangle)
```

#### `Math.cbrt(x)` — Cube Root
```javascript
console.log(Math.cbrt(8));             // 2
console.log(Math.cbrt(27));            // 3
console.log(Math.cbrt(-8));            // -2 (handles negatives)
```

### Logarithms

#### `Math.log(x)` — Natural Logarithm (base e)
```javascript
console.log(Math.log(Math.E));         // 1
console.log(Math.log(1));              // 0
console.log(Math.log(10));             // 2.302...
console.log(Math.log(0));              // -Infinity
console.log(Math.log(-1));             // NaN
```

#### `Math.log10(x)` — Logarithm Base 10
```javascript
console.log(Math.log10(1));            // 0
console.log(Math.log10(10));           // 1
console.log(Math.log10(100));          // 2
console.log(Math.log10(1000));         // 3
```

#### `Math.log2(x)` — Logarithm Base 2
```javascript
console.log(Math.log2(1));             // 0
console.log(Math.log2(2));             // 1
console.log(Math.log2(8));             // 3
console.log(Math.log2(1024));          // 10
```

#### `Math.exp(x)` — e to the Power
```javascript
console.log(Math.exp(0));              // 1
console.log(Math.exp(1));              // 2.718... (e)
console.log(Math.exp(2));              // 7.389...
```

### Trigonometric Functions

```javascript
// Radians (not degrees!)
console.log(Math.sin(0));              // 0
console.log(Math.sin(Math.PI / 2));    // 1
console.log(Math.sin(Math.PI));        // ~0

console.log(Math.cos(0));              // 1
console.log(Math.cos(Math.PI / 2));    // ~0
console.log(Math.cos(Math.PI));        // -1

console.log(Math.tan(0));              // 0
console.log(Math.tan(Math.PI / 4));    // 1

// Inverse functions (return radians)
console.log(Math.asin(0));             // 0
console.log(Math.asin(1));             // π/2
console.log(Math.acos(0));             // π/2
console.log(Math.atan(1));             // π/4

// Convert radians to degrees
function toDegrees(radians) {
  return radians * 180 / Math.PI;
}
console.log(toDegrees(Math.PI));       // 180
console.log(toDegrees(Math.PI / 2));   // 90
```

### Random Numbers: `Math.random()`

Returns random number in range [0, 1):

```javascript
console.log(Math.random());            // e.g., 0.8234...
console.log(Math.random());            // e.g., 0.1923... (different)

// Random integer from 0 to 9
function randomInt(max) {
  return Math.floor(Math.random() * max);
}
console.log(randomInt(10)); // 0-9

// Random integer in range [min, max]
function randomRange(min, max) {
  return Math.floor(Math.random() * (max - min + 1)) + min;
}
console.log(randomRange(1, 6));  // Dice roll 1-6
console.log(randomRange(1, 100)); // 1-100

// Random choice from array
function randomChoice(arr) {
  return arr[Math.floor(Math.random() * arr.length)];
}
const choices = ['apple', 'banana', 'cherry'];
console.log(randomChoice(choices)); // Random fruit

// Shuffle array (Fisher-Yates)
function shuffle(arr) {
  const result = [...arr];
  for (let i = result.length - 1; i > 0; i--) {
    const j = Math.floor(Math.random() * (i + 1));
    [result[i], result[j]] = [result[j], result[i]];
  }
  return result;
}
console.log(shuffle([1, 2, 3, 4, 5]));
```

---

## 6. Floating-Point Arithmetic Gotchas

### The Classic Problem: `0.1 + 0.2 !== 0.3`

This happens because of IEEE 754 floating-point representation:

```javascript
console.log(0.1 + 0.2);                // 0.30000000000000004 — not 0.3!
console.log(0.1 + 0.2 === 0.3);        // false

// Why?
console.log((0.1).toString(2));        // Binary: never-ending, so rounded
console.log((0.2).toString(2));        // Binary: never-ending, so rounded
console.log((0.3).toString(2));        // Binary: never-ending, so rounded

// The actual values stored
console.log(0.1 + 0.2 - 0.3);          // 5.551115123125783e-17
```

### Rounding Strategies

#### Strategy 1: Use `toFixed()` and Convert Back

```javascript
function add(a, b, decimals = 2) {
  const result = a + b;
  return parseFloat(result.toFixed(decimals));
}

console.log(add(0.1, 0.2));            // 0.3
console.log(add(0.1, 0.2) === 0.3);    // true!
```

#### Strategy 2: Multiply, Compute, Divide

```javascript
function addCents(cents1, cents2) {
  // Work with integers (cents)
  return (cents1 + cents2) / 100;
}

console.log(addCents(10, 20));         // 0.3
console.log(addCents(15, 25));         // 0.4

// For currency: store as cents (integers), not dollars
const price1 = 10.50; // Don't use!
const price1Cents = 1050; // Use this!

const purchase = (1050 + 2000 + 500) / 100; // 35.50
console.log(purchase);
```

#### Strategy 3: Check Closeness

```javascript
function almostEqual(a, b, tolerance = 1e-10) {
  return Math.abs(a - b) < tolerance;
}

console.log(almostEqual(0.1 + 0.2, 0.3)); // true
console.log(almostEqual(0.1, 0.2));      // false

// Practical: physics simulations
if (almostEqual(velocity, 0, 0.001)) {
  console.log('Velocity is essentially zero');
}
```

---

## 7. BigInt

### What is BigInt?

**BigInt** is a primitive type for arbitrarily large integers (no upper limit like `Number`). Cannot have decimals.

```javascript
// BigInt literals (n suffix)
const big1 = 123n;
const big2 = 999999999999999999999999999999n;

console.log(typeof big1);              // "bigint"
console.log(big1);                     // 123n

// Creating from number
const big3 = BigInt(123);
const big4 = BigInt('999999999999999999999999999999');

console.log(big3);                     // 123n
console.log(big4);                     // 999999999999999999999999999999n
```

### Arithmetic with BigInt

```javascript
const a = 10n;
const b = 3n;

console.log(a + b);                    // 13n
console.log(a - b);                    // 7n
console.log(a * b);                    // 30n
console.log(a / b);                    // 3n (floor division, no decimals)
console.log(a % b);                    // 1n
console.log(a ** b);                   // 1000n (exponentiation)

// **Cannot mix BigInt and Number**
// This will error:
// console.log(10n + 5); // TypeError

// Must convert first
console.log(10n + BigInt(5));          // 15n
console.log(Number(10n) + 5);          // 15

// Comparison works across types
console.log(10n > 5);                  // true
console.log(10n === 10);               // false (different types!)
console.log(10n == 10);                // true (loose equality)
```

### No Decimals with BigInt

```javascript
// These cause errors
// const decimal = 3.14n; // SyntaxError
// const pi = BigInt(3.14); // RangeError

// Must convert to integer
const result = BigInt(Math.floor(3.14 * 100)) / 100n;
console.log(result); // 313n / 100n
console.log(Number(result)); // 3.13
```

### Practical BigInt Use Cases

```javascript
// Cryptography
const privateKey = 12345678901234567890123456789012345678901234567890n;
console.log(privateKey.toString(16)); // Hex representation

// Large factorials
function factorial(n) {
  if (n === 0n) return 1n;
  return n * factorial(n - 1n);
}
console.log(factorial(20n)); // Huge number!

// Iteration with BigInt
for (let i = 1n; i <= 5n; i++) {
  console.log(i);
}
// 1n, 2n, 3n, 4n, 5n

// BigInt doesn't have methods like toFixed()
// But toString() works
const big = 12345n;
console.log(big.toString());           // '12345'
console.log(big.toString(2));          // '11000000111001' (binary)
console.log(big.toString(16));         // '3039' (hex)
```

### Converting Between Number and BigInt

```javascript
const num = 42;
const fromNum = BigInt(num);
console.log(fromNum); // 42n

const big = 100n;
const fromBig = Number(big);
console.log(fromBig); // 100
console.log(typeof fromBig); // "number"

// Safe conversion
function safeConvert(big) {
  if (big > Number.MAX_SAFE_INTEGER) {
    console.warn('BigInt too large to safely convert');
  }
  return Number(big);
}
```

---

## Summary: Number Methods Quick Reference

| Method | Purpose |
|--------|---------|
| `Number.isNaN()` | Check if value is NaN (strict) |
| `Number.isFinite()` | Check if value is finite |
| `Number.isInteger()` | Check if value is integer |
| `Number.isSafeInteger()` | Check if value is in safe range |
| `toString(radix)` | Convert to string (with base) |
| `toFixed(digits)` | Format with decimal places |
| `toExponential(digits)` | Scientific notation |
| `toPrecision(digits)` | Significant figures |

---

## Summary: Math Methods Quick Reference

| Category | Methods |
|----------|---------|
| **Rounding** | `floor`, `ceil`, `round`, `trunc` |
| **Power/Root** | `pow`, `sqrt`, `cbrt` |
| **Logarithm** | `log`, `log10`, `log2`, `exp` |
| **Trigonometry** | `sin`, `cos`, `tan`, `asin`, `acos`, `atan` |
| **Min/Max** | `min`, `max` |
| **Other** | `abs`, `sign`, `random` |

---

## Best Practices

✅ **Always specify radix in `parseInt()`** — Use `parseInt(str, 10)`

✅ **Use `Number.isNaN()` instead of global `isNaN()`** — Avoids type coercion

✅ **Use `Number.isSafeInteger()` for large numbers** — Especially financial data

✅ **For currency, work with cents (integers)** — Avoid floating-point errors

✅ **Use `toFixed()` only for display** — Convert back to number for calculations

✅ **Use `Math.max(...arr)` with spread operator** — Not `Math.max(arr)`

✅ **Use `Number.EPSILON` for floating-point comparisons** — Check if difference is tiny

✅ **Use BigInt for cryptography and large integers** — Not regular numbers

```javascript
// Floating-point comparison with epsilon
function areEqual(a, b) {
  return Math.abs(a - b) < Number.EPSILON;
}
console.log(areEqual(0.1 + 0.2, 0.3)); // true
```

---

## Common Gotchas

❌ **`parseInt()` without radix is unpredictable**
```javascript
parseInt('10');     // 10 (OK)
parseInt('010');    // 10 (but was 8 in older JS!)
parseInt('0xFF');   // 255 (auto-detects hex)
// Always use radix!
parseInt('10', 10); // 10
```

❌ **`isNaN()` does type coercion**
```javascript
isNaN('hello');     // true — 'hello' converts to NaN
isNaN('42');        // false — '42' converts to 42
Number.isNaN('hello'); // false — strict, no conversion
```

❌ **Floating-point arithmetic is imprecise**
```javascript
0.1 + 0.2 === 0.3; // false!
0.1 + 0.2;         // 0.30000000000000004
```

❌ **Cannot mix BigInt and Number**
```javascript
10n + 5;           // TypeError
10n + BigInt(5);   // 15n — works
Number(10n) + 5;   // 15 — works
```

❌ **Math.round() rounds toward positive infinity at 0.5**
```javascript
Math.round(2.5);   // 3
Math.round(-2.5);  // -2 (toward positive)
// For banker's rounding, use other techniques
```

❌ **`Math.min()` and `Math.max()` need spread for arrays**
```javascript
const nums = [1, 2, 3];
Math.max(nums);     // NaN — expects number args
Math.max(...nums);  // 3 — correct
```
