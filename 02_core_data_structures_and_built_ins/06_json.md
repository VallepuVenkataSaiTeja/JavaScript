# 2.6 JSON

## What is JSON?

**JSON** (JavaScript Object Notation) is a lightweight text format for exchanging data. It's based on JavaScript object and array syntax but is language-independent and text-based. JSON is the de facto standard for APIs, configuration files, and data storage.

JavaScript provides two built-in methods for working with JSON:
- **`JSON.stringify()`** — Convert objects to JSON strings
- **`JSON.parse()`** — Convert JSON strings back to objects

---

## 1. JSON.stringify()

### Basic Usage

Converts JavaScript values to JSON string format:

```javascript
// Object
const person = { name: 'Alice', age: 30 };
const json = JSON.stringify(person);
console.log(json); // '{"name":"Alice","age":30}'
console.log(typeof json); // "string"

// Array
const arr = [1, 2, 3];
const jsonArr = JSON.stringify(arr);
console.log(jsonArr); // '[1,2,3]'

// Simple values
JSON.stringify('hello');    // '"hello"'
JSON.stringify(42);         // '42'
JSON.stringify(true);       // 'true'
JSON.stringify(null);       // 'null'
```

### The `space` Parameter

Makes JSON human-readable with indentation:

```javascript
const person = { name: 'Alice', age: 30, email: 'alice@example.com' };

// Without space (compact)
console.log(JSON.stringify(person));
// '{"name":"Alice","age":30,"email":"alice@example.com"}'

// With space: number of spaces
console.log(JSON.stringify(person, null, 2));
// {
//   "name": "Alice",
//   "age": 30,
//   "email": "alice@example.com"
// }

// With space: 4 spaces
console.log(JSON.stringify(person, null, 4));
// {
//     "name": "Alice",
//     "age": 30,
//     "email": "alice@example.com"
// }

// With space: string (tab character)
console.log(JSON.stringify(person, null, '\t'));
// {
// 	"name": "Alice",
// 	"age": 30,
// 	"email": "alice@example.com"
// }

// Maximum space is 10
JSON.stringify(person, null, 20); // Treated as 10 spaces
```

### The `replacer` Parameter

Filters or transforms values during serialization:

#### Replacer as Array (Whitelist)

Include only specified keys:

```javascript
const person = { name: 'Alice', age: 30, email: 'alice@example.com', phone: '555-1234' };

// Only include name and age
const json = JSON.stringify(person, ['name', 'age']);
console.log(json);
// '{"name":"Alice","age":30}'

// Email and phone are excluded

// Works with nested objects
const user = {
  name: 'Alice',
  address: {
    city: 'New York',
    zip: '10001'
  },
  email: 'alice@example.com'
};

const json2 = JSON.stringify(user, ['name', 'address', 'city']);
console.log(json2);
// '{"name":"Alice","address":{"city":"New York"}}'
```

#### Replacer as Function

Transform values during serialization:

```javascript
const person = { name: 'Alice', age: 30, salary: 100000 };

// Hide sensitive data
const json = JSON.stringify(person, (key, value) => {
  // Skip salary field
  if (key === 'salary') return undefined;
  return value;
});
console.log(json);
// '{"name":"Alice","age":30}'

// Transform values
const json2 = JSON.stringify(person, (key, value) => {
  // Convert age to string
  if (key === 'age') return `${value} years`;
  return value;
});
console.log(json2);
// '{"name":"Alice","age":"30 years","salary":100000}'

// Uppercase string values
const json3 = JSON.stringify(person, (key, value) => {
  if (typeof value === 'string') return value.toUpperCase();
  return value;
});
console.log(json3);
// '{"name":"ALICE","age":30,"salary":100000}'

// Replace all numeric values
const data = { x: 10, y: 20, name: 'test' };
const json4 = JSON.stringify(data, (key, value) => {
  if (typeof value === 'number') return value * 2;
  return value;
});
console.log(json4);
// '{"x":20,"y":40,"name":"test"}'
```

**Note**: The replacer function receives all keys, including the root object (empty key) and array indices.

```javascript
const obj = { a: 1, b: 2 };
const json = JSON.stringify(obj, (key, value) => {
  console.log(`key: "${key}", value:`, value);
  return value;
});

// Output:
// key: "", value: { a: 1, b: 2 }  — root object
// key: "a", value: 1
// key: "b", value: 2
```

### Practical Replacer Examples

#### Hide Sensitive Fields

```javascript
function stringifyWithoutPasswords(obj) {
  return JSON.stringify(obj, (key, value) => {
    if (key === 'password' || key === 'apiKey' || key === 'token') {
      return undefined; // Exclude
    }
    return value;
  });
}

const user = {
  name: 'Alice',
  email: 'alice@example.com',
  password: 'secret123', // Won't appear in JSON
  apiKey: 'xyz789'       // Won't appear in JSON
};

console.log(stringifyWithoutPasswords(user));
// '{"name":"Alice","email":"alice@example.com"}'
```

#### Serialize Class Instances

```javascript
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  greet() {
    return `Hello, I'm ${this.name}`;
  }
}

const person = new Person('Alice', 30);
console.log(JSON.stringify(person));
// '{"name":"Alice","age":30}' — methods excluded automatically

// But if Person has methods you want to include:
const json = JSON.stringify(person, (key, value) => {
  if (typeof value === 'function') {
    return `[Function: ${value.name}]`; // Or exclude: return undefined
  }
  return value;
});
console.log(json);
// '{"name":"Alice","age":30}'
```

---

## 2. JSON.parse()

### Basic Usage

Converts JSON strings back to JavaScript objects:

```javascript
// Parse object
const json = '{"name":"Alice","age":30}';
const person = JSON.parse(json);
console.log(person);        // { name: 'Alice', age: 30 }
console.log(person.name);   // 'Alice'

// Parse array
const jsonArr = '[1,2,3]';
const arr = JSON.parse(jsonArr);
console.log(arr);           // [1, 2, 3]

// Parse simple values
JSON.parse('"hello"');      // 'hello'
JSON.parse('42');           // 42
JSON.parse('true');         // true
JSON.parse('null');         // null

// Whitespace is ignored
JSON.parse('  { "x": 1 }  '); // { x: 1 }
```

### Invalid JSON Throws Error

```javascript
// Missing quotes on key
try {
  JSON.parse('{name: "Alice"}');
} catch (e) {
  console.error(e.message); // Unexpected token n in JSON at position 1
}

// Single quotes instead of double
try {
  JSON.parse("{'name': 'Alice'}");
} catch (e) {
  console.error(e.message); // Unexpected token ' in JSON at position 1
}

// Trailing comma
try {
  JSON.parse('{"x": 1,}');
} catch (e) {
  console.error(e.message); // Unexpected token } in JSON at position 9
}

// Always validate before parsing
function safeJsonParse(str, fallback = null) {
  try {
    return JSON.parse(str);
  } catch (e) {
    console.error('Invalid JSON:', e.message);
    return fallback;
  }
}

console.log(safeJsonParse('invalid')); // null
console.log(safeJsonParse('{"x":1}')); // { x: 1 }
```

### The `reviver` Parameter

Transform values during deserialization:

```javascript
const json = '{"name":"Alice","age":30}';

// Basic reviver
const person = JSON.parse(json, (key, value) => {
  console.log(`key: "${key}", value: ${value}`);
  return value;
});

// Output shows each key/value pair:
// key: "name", value: Alice
// key: "age", value: 30
// key: "", value: { name: 'Alice', age: 30 } — root object

// Transform values
const json2 = '{"x":10,"y":20}';
const data = JSON.parse(json2, (key, value) => {
  if (typeof value === 'number') return value * 2;
  return value;
});
console.log(data); // { x: 20, y: 40 }

// Convert to specific type
const json3 = '{"numbers":[1,2,3]}';
const result = JSON.parse(json3, (key, value) => {
  if (key === 'numbers' && Array.isArray(value)) {
    return new Set(value); // Convert array to Set
  }
  return value;
});
console.log(result); // { numbers: Set(3) { 1, 2, 3 } }
```

---

## 3. Supported and Unsupported Types

### Supported Types

JSON supports these types:

```javascript
const supported = {
  object: { name: 'Alice' },
  array: [1, 2, 3],
  string: 'hello',
  number: 42,
  boolean: true,
  null: null
};

const json = JSON.stringify(supported);
console.log(json);
// { "object":{"name":"Alice"},"array":[1,2,3],"string":"hello","number":42,"boolean":true,"null":null }

// Parse it back
const parsed = JSON.parse(json);
console.log(parsed); // Works perfectly
```

### Unsupported Types

These types are **not** supported in JSON:

#### 1. Functions
```javascript
const obj = {
  name: 'Alice',
  greet: function() { return 'Hello!'; }
};

const json = JSON.stringify(obj);
console.log(json);
// '{"name":"Alice"}' — function is omitted!

// Can't restore
const parsed = JSON.parse(json);
console.log(parsed.greet); // undefined
```

#### 2. Undefined
```javascript
const obj = {
  name: 'Alice',
  middle: undefined
};

const json = JSON.stringify(obj);
console.log(json);
// '{"name":"Alice"}' — undefined property omitted

// In arrays, undefined becomes null
const arr = [1, undefined, 3];
const jsonArr = JSON.stringify(arr);
console.log(jsonArr);
// '[1,null,3]' — undefined became null!
```

#### 3. Symbol
```javascript
const obj = {
  name: 'Alice',
  [Symbol.for('id')]: 123
};

const json = JSON.stringify(obj);
console.log(json);
// '{"name":"Alice"}' — Symbol omitted
```

#### 4. BigInt

```javascript
const big = {
  value: 100n
};

try {
  JSON.stringify(big);
} catch (e) {
  console.error(e.message); // Do not know how to serialize a BigInt
}

// Workaround: use replacer to convert
const json = JSON.stringify(big, (key, value) => {
  if (typeof value === 'bigint') {
    return value.toString(); // Convert to string
  }
  return value;
});
console.log(json); // '{"value":"100"}'
```

#### 5. NaN, Infinity

```javascript
const obj = {
  regular: 42,
  notANumber: NaN,
  positive: Infinity,
  negative: -Infinity
};

const json = JSON.stringify(obj);
console.log(json);
// '{"regular":42,"notANumber":null,"positive":null,"negative":null}'
// All non-finite numbers become null!

// Workaround:
const json2 = JSON.stringify(obj, (key, value) => {
  if (typeof value === 'number') {
    if (!isFinite(value)) {
      return `[${value.toString()}]`; // Or custom representation
    }
  }
  return value;
});
console.log(json2);
// '{"regular":42,"notANumber":"[NaN]","positive":"[Infinity]","negative":"[-Infinity]"}'
```

### Summary Table

| Type | JSON | Behavior |
|------|------|----------|
| Object | ✅ | Serialized as `{...}` |
| Array | ✅ | Serialized as `[...]` |
| String | ✅ | Quoted: `"text"` |
| Number | ✅ | `42`, `3.14`; (not NaN/Infinity) |
| Boolean | ✅ | `true`, `false` |
| null | ✅ | `null` |
| Function | ❌ | Omitted (or null in arrays) |
| undefined | ❌ | Omitted (or null in arrays) |
| Symbol | ❌ | Omitted |
| BigInt | ❌ | Error (must convert) |
| NaN | ❌ | Becomes `null` |
| Infinity | ❌ | Becomes `null` |
| Date | ⚠️ | Becomes ISO string |
| Map/Set | ❌ | Becomes `{}` or `[]` |
| RegExp | ❌ | Becomes `{}` |

---

## 4. Serializing Dates

### Problem: Dates Become Strings

By default, Date objects serialize to ISO 8601 strings:

```javascript
const event = {
  name: 'Conference',
  date: new Date('2026-02-18T14:30:00')
};

const json = JSON.stringify(event);
console.log(json);
// '{"name":"Conference","date":"2026-02-18T14:30:00.000Z"}'

// Date is now a string!
const parsed = JSON.parse(json);
console.log(typeof parsed.date); // "string" — not Date!
console.log(parsed.date); // "2026-02-18T14:30:00.000Z"
```

### Restore Dates in Reviver

Use the `reviver` function to convert ISO strings back to Date objects:

```javascript
const event = {
  name: 'Conference',
  date: new Date('2026-02-18T14:30:00')
};

const json = JSON.stringify(event);
console.log(json);

// Parse with reviver
const restored = JSON.parse(json, (key, value) => {
  // Check if value looks like ISO date string
  if (typeof value === 'string' && /^\d{4}-\d{2}-\d{2}T/.test(value)) {
    return new Date(value);
  }
  return value;
});

console.log(restored.date); // Date object
console.log(restored.date instanceof Date); // true
console.log(restored.date.getFullYear()); // 2026
```

### Custom Date Reviver

More robust pattern matching:

```javascript
function dateReviver(key, value) {
  // Check if value is ISO 8601 date string
  if (typeof value === 'string') {
    // ISO format: YYYY-MM-DDTHH:mm:ss.sssZ
    const datePattern = /^\d{4}-\d{2}-\d{2}T\d{2}:\d{2}:\d{2}/;
    if (datePattern.test(value)) {
      return new Date(value);
    }
  }
  return value;
}

const json = '{"event":"Conference","date":"2026-02-18T14:30:00Z"}';
const data = JSON.parse(json, dateReviver);

console.log(data.event); // "Conference" (unchanged)
console.log(data.date instanceof Date); // true
console.log(data.date.getFullYear()); // 2026
```

### Hint Keys for Specific Fields

If only certain fields are dates, check the key:

```javascript
function dateReviverByKey(key, value) {
  const dateFields = ['date', 'birthDate', 'createdAt', 'updatedAt'];
  
  if (dateFields.includes(key) && typeof value === 'string') {
    return new Date(value);
  }
  return value;
}

const json = '{"name":"Alice","birthDate":"1990-05-15","created":"2026-02-18T10:00:00Z"}';
const data = JSON.parse(json, dateReviverByKey);

console.log(data.birthDate instanceof Date); // true
console.log(data.created instanceof Date); // false (key didn't match)
```

---

## 5. Circular References

### Problem: Circular References Cause Error

Objects that reference themselves cannot be serialized:

```javascript
const obj = { name: 'Alice' };
obj.self = obj; // Circular reference!

try {
  JSON.stringify(obj);
} catch (e) {
  console.error(e.message);
  // Converting circular structure to JSON
}
```

### Replacer to Skip Circular References

```javascript
function stringifyWithoutCircular(obj) {
  const seen = new WeakSet();

  return JSON.stringify(obj, (key, value) => {
    if (typeof value === 'object' && value !== null) {
      if (seen.has(value)) {
        return undefined; // Skip circular reference
      }
      seen.add(value);
    }
    return value;
  });
}

const obj = { name: 'Alice' };
obj.self = obj; // Circular reference

const json = stringifyWithoutCircular(obj);
console.log(json);
// '{"name":"Alice"}' — self reference omitted
```

### Replacer to Detect Depth

Limit serialization depth:

```javascript
function stringifyWithMaxDepth(obj, maxDepth) {
  return JSON.stringify(obj, (key, value) => {
    const depth = key.split('.').length - 1;
    if (depth > maxDepth) {
      return undefined;
    }
    return value;
  }, 2);
}

// Note: Above approach has issues. Better approach:
function stringifyWithDepth(obj, maxDepth) {
  let depth = 0;

  return JSON.stringify(obj, (key, value) => {
    // Simple approach: if it's an object and we're too deep, skip
    if (Object.prototype.toString.call(value) === '[object Object]') {
      if (key && key.split('.').length > maxDepth) {
        return undefined;
      }
    }
    return value;
  }, 2);
}
```

---

## 6. The `toJSON()` Method

### Custom Serialization with toJSON

Objects can implement a `toJSON()` method for custom serialization:

```javascript
// Class with toJSON
class Person {
  constructor(name, age, ssn) {
    this.name = name;
    this.age = age;
    this.ssn = ssn; // Sensitive!
  }

  toJSON() {
    // Return only safe data
    return {
      name: this.name,
      age: this.age
      // ssn excluded
    };
  }
}

const person = new Person('Alice', 30, '123-45-6789');
const json = JSON.stringify(person);
console.log(json);
// '{"name":"Alice","age":30}' — SSN not included
```

### Date Already Uses toJSON

Date objects have built-in `toJSON()`:

```javascript
const date = new Date('2026-02-18T14:30:00');
console.log(date.toJSON());
// '2026-02-18T14:30:00.000Z'

// That's why dates serialize to ISO strings in JSON.stringify()
const obj = { date: date };
console.log(JSON.stringify(obj));
// '{"date":"2026-02-18T14:30:00.000Z"}'
```

### Custom toJSON Examples

#### Hide Sensitive Data

```javascript
class User {
  constructor(name, email, password) {
    this.name = name;
    this.email = email;
    this.password = password;
  }

  toJSON() {
    const { password, ...safe } = this; // Exclude password
    return safe;
  }
}

const user = new User('Alice', 'alice@example.com', 'secret123');
const json = JSON.stringify(user);
console.log(json);
// '{"name":"Alice","email":"alice@example.com"}'
```

#### Transform Data Types

```javascript
class Product {
  constructor(name, price, inStock) {
    this.name = name;
    this.price = price;
    this.inStock = inStock;
  }

  toJSON() {
    return {
      name: this.name,
      price: `$${this.price.toFixed(2)}`, // Format as currency
      inStock: this.inStock ? 'In Stock' : 'Out of Stock' // Descriptive
    };
  }
}

const product = new Product('Laptop', 999.99, true);
const json = JSON.stringify(product);
console.log(json);
// '{"name":"Laptop","price":"$999.99","inStock":"In Stock"}'
```

#### Custom Date Format

```javascript
class DateWithCustomFormat extends Date {
  toJSON() {
    // Return custom format instead of ISO
    const year = this.getFullYear();
    const month = String(this.getMonth() + 1).padStart(2, '0');
    const day = String(this.getDate()).padStart(2, '0');
    return `${day}/${month}/${year}`; // DD/MM/YYYY
  }
}

const date = new DateWithCustomFormat('2026-02-18');
console.log(JSON.stringify({ date }));
// '{"date":"18/02/2026"}'
```

#### Include Computed Properties

```javascript
class Rectangle {
  constructor(width, height) {
    this.width = width;
    this.height = height;
  }

  get area() {
    return this.width * this.height;
  }

  toJSON() {
    return {
      width: this.width,
      height: this.height,
      area: this.area // Include computed property
    };
  }
}

const rect = new Rectangle(10, 20);
const json = JSON.stringify(rect);
console.log(json);
// '{"width":10,"height":20,"area":200}'
```

---

## 7. Practical Patterns

### Request Body

```javascript
const data = {
  username: 'alice',
  email: 'alice@example.com',
  password: 'secret123'
};

const json = JSON.stringify(data);

// Send to server
fetch('https://api.example.com/register', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: json
});
```

### Response Parsing

```javascript
fetch('https://api.example.com/users/1')
  .then(response => response.text())
  .then(text => {
    const user = JSON.parse(text);
    console.log(user.name);
  });

// Or with automatic JSON parsing
fetch('https://api.example.com/users/1')
  .then(response => response.json()) // Automatically parses JSON
  .then(user => console.log(user.name));
```

### Configuration Files

```javascript
// config.json
{
  "app": {
    "name": "MyApp",
    "version": "1.0.0"
  },
  "database": {
    "host": "localhost",
    "port": 5432
  }
}

// Load and parse
const fs = require('fs');
const configText = fs.readFileSync('config.json', 'utf-8');
const config = JSON.parse(configText);
console.log(config.app.name); // "MyApp"
```

### Local Storage

```javascript
// Save object to localStorage
const user = { name: 'Alice', age: 30 };
localStorage.setItem('user', JSON.stringify(user));

// Retrieve from localStorage
const stored = localStorage.getItem('user');
const restored = JSON.parse(stored);
console.log(restored.name); // 'Alice'

// With reviver for dates
const userData = {
  name: 'Alice',
  lastLogin: new Date()
};

localStorage.setItem('userData', JSON.stringify(userData));

// Restore with reviver
const retrieved = JSON.parse(localStorage.getItem('userData'), (key, value) => {
  if (key === 'lastLogin' && typeof value === 'string') {
    return new Date(value);
  }
  return value;
});
console.log(retrieved.lastLogin instanceof Date); // true
```

### Deep Cloning

```javascript
// Shallow clone (also works with Objects that don't have circular refs)
const original = { name: 'Alice', address: { city: 'NYC' } };
const clone = JSON.parse(JSON.stringify(original));

clone.address.city = 'LA';
console.log(original.address.city); // 'NYC' — unchanged (deep copy!)

// WARNING: Doesn't work for:
// - Functions
// - Dates (become strings)
// - Undefined
// - Symbols
// - BigInt
// Use structuredClone() for a true deep copy

const better = structuredClone(original);
```

---

## Summary: JSON Methods Quick Reference

| Method | Purpose |
|--------|---------|
| `JSON.stringify(value, replacer?, space?)` | Convert to JSON string |
| `JSON.parse(string, reviver?)` | Convert from JSON string |

| Parameters | Purpose |
|-----------|---------|
| `replacer` (array) | Whitelist of keys to include |
| `replacer` (function) | Transform/filter values |
| `space` (number) | Indentation (0-10) |
| `space` (string) | Indentation string (tab, etc.) |
| `reviver` (function) | Transform/filter parsed values |

---

## Best Practices

✅ **Always use `JSON.stringify()` for APIs** — Don't concatenate JSON manually

✅ **Always validate JSON input** — Use try/catch with `JSON.parse()`

✅ **Use `replacer` to hide sensitive data** — Don't send passwords/tokens

✅ **Restore Dates with reviver** — They become strings after parsing

✅ **Implement `toJSON()` for custom classes** — More control over serialization

✅ **Use `space` parameter for debugging** — Makes JSON readable

✅ **Use WeakSet for circular reference detection** — More efficient than tracking strings

✅ **Use `structuredClone()` instead of JSON for deep cloning** — More reliable

---

## Common Gotchas

❌ **Functions are omitted in JSON**
```javascript
const obj = { name: 'Alice', greet: () => 'Hi' };
const json = JSON.stringify(obj);
console.log(json); // '{"name":"Alice"}' — greet is gone!
```

❌ **Undefined becomes null in arrays**
```javascript
const arr = [1, undefined, 3];
const json = JSON.stringify(arr);
console.log(json); // '[1,null,3]' — undefined became null!
```

❌ **Dates become strings**
```javascript
const obj = { date: new Date() };
const json = JSON.stringify(obj);
const parsed = JSON.parse(json);
console.log(typeof parsed.date); // "string" — not Date!
// Use reviver to restore: JSON.parse(json, dateReviver)
```

❌ **Circular references throw error**
```javascript
const obj = { name: 'Alice' };
obj.self = obj;
JSON.stringify(obj); // TypeError: Converting circular structure to JSON
// Use replacer with WeakSet to skip
```

❌ **BigInt not supported**
```javascript
const obj = { value: 100n };
JSON.stringify(obj); // TypeError: Do not know how to serialize a BigInt
// Convert to string first
```

❌ **Month is 0-indexed in ISO dates**
```javascript
new Date('2026-02-18'); // February 18
// But when parsed from JSON, it's already correct (ISO string)
```

❌ **Replacer array doesn't work with arrays**
```javascript
const arr = [1, 2, 3];
JSON.stringify(arr, ['0', '1']); // '[1,2,3]' — replacer doesn't filter arrays
// Replacer array only filters object keys, not array indices
```

❌ **NaN and Infinity become null**
```javascript
const obj = { x: NaN, y: Infinity };
const json = JSON.stringify(obj);
console.log(json); // '{"x":null,"y":null}'
// Both become null, losing information
// Use replacer to handle: (key, value) => !isFinite(value) ? String(value) : value
```
