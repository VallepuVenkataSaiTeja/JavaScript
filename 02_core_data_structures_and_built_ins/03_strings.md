# 2.3 Strings

## What is a String?

A **string** is a sequence of characters representing text. In JavaScript, strings are a **primitive data type** and are **immutable** — once created, they cannot be changed. However, JavaScript provides many methods to create new strings based on existing ones. Strings are created using single quotes (`'`), double quotes (`"`), or backticks (`` ` ``).

```javascript
const str1 = 'Hello';
const str2 = "World";
const str3 = `JavaScript`;

console.log(typeof str1); // "string"
```

---

## 1. Auto-boxing and String Objects

### What is Auto-boxing?

When you call a method on a primitive string, JavaScript temporarily wraps it in a **String object** (auto-boxing) so it can access object methods. This wrapper is then discarded after the method completes.

```javascript
// Primitive string
const str = 'hello';

// Auto-boxing: JavaScript internally converts to String object
const upper = str.toUpperCase();
// Equivalent to: new String('hello').toUpperCase()

console.log(upper);       // 'HELLO'
console.log(typeof str);  // "string" — still primitive!

// The primitive is unchanged (immutability)
console.log(str);         // 'hello'
```

### String vs String Object

```javascript
// Primitive string
const primitive = 'hello';
console.log(typeof primitive);     // "string"
console.log(primitive instanceof String); // false

// String object
const obj = new String('hello');
console.log(typeof obj);           // "object"
console.log(obj instanceof String); // true
console.log(obj === 'hello');      // false — different types

// String objects are truthy, even empty strings!
console.log(Boolean(new String(''))); // true
console.log(Boolean(''));             // false

// Avoid using String objects — use primitives
```

### Why Auto-boxing is Cool

```javascript
// You can call methods directly on string literals
console.log('hello'.toUpperCase());           // 'HELLO'
console.log('HELLO'.toLowerCase());           // 'hello'
console.log('  spaces  '.trim());             // 'spaces'
console.log('hello world'.split(' '));        // ['hello', 'world']

// Without auto-boxing, you'd need:
// const str = new String('hello');
// str.toUpperCase();
```

---

## 2. The `.length` Property

The `.length` property returns the number of **UTF-16 code units** (not always the visual character count):

```javascript
const str = 'Hello';
console.log(str.length); // 5

const empty = '';
console.log(empty.length); // 0

// With spaces
console.log('Hello World'.length); // 11
```

### Gotcha: Emojis and Surrogate Pairs

Some characters (like emojis) take up 2 UTF-16 code units, so `.length` might not equal the visual character count:

```javascript
const simple = 'ABC';
console.log(simple.length); // 3 — three characters

// Emoji 😀 is 1 visual character but 2 UTF-16 code units
const emoji = '😀';
console.log(emoji.length); // 2 — not 1!

const mixed = 'Hi 😀';
console.log(mixed.length); // 5 — 'H' + 'i' + ' ' + emoji(2)

// More complex example
const text = '👨‍👩‍👦'; // Family emoji (woman + man + child)
console.log(text.length); // 8 — even longer!

// For accurate character count, use Array.from() or spread
console.log(Array.from(emoji).length);     // 1
console.log([...emoji].length);            // 1
console.log(Array.from(mixed).length);     // 4 — correct!
console.log([...text].length);             // 4 — family emoji
```

### Accessing Characters by Index

```javascript
const str = 'Hello';

// Index access (read-only)
console.log(str[0]); // 'H'
console.log(str[1]); // 'e'
console.log(str[4]); // 'o'
console.log(str[10]); // undefined — out of bounds

// Negative indices don't work
console.log(str[-1]); // undefined

// Last character
console.log(str[str.length - 1]); // 'o'
```

### Immutability

Strings cannot be modified. Any "modification" creates a new string:

```javascript
const str = 'Hello';

// This doesn't work
str[0] = 'h';
console.log(str); // 'Hello' — unchanged

// You must create a new string
const modified = 'h' + str.slice(1);
console.log(modified); // 'hello'
console.log(str);      // 'Hello' — original unchanged

// Why immutability matters
const original = 'Important';
const backup = original; // Still references the same string

// If strings were mutable:
// original[0] = 'X';
// backup would also be 'Xmportant'

// But with immutability:
const modified2 = 'X' + original.slice(1);
console.log(original); // 'Important' — safe!
console.log(backup);   // 'Important' — safe!
console.log(modified2); // 'Xmportant'
```

---

## 3. Searching Strings

### `indexOf(searchString, fromIndex?)`
Returns the index of first occurrence (or -1):

```javascript
const str = 'Hello World Hello';

console.log(str.indexOf('Hello'));   // 0 — first occurrence
console.log(str.indexOf('World'));   // 6
console.log(str.indexOf('xyz'));     // -1 — not found

// Start search from specific index
console.log(str.indexOf('Hello', 1)); // 12 — second occurrence

// Case sensitive
console.log(str.indexOf('hello'));   // -1 — case matters
console.log(str.indexOf('HELLO'));   // -1
```

### `lastIndexOf(searchString, fromIndex?)`
Returns the index of last occurrence:

```javascript
const str = 'Hello World Hello';

console.log(str.lastIndexOf('Hello'));   // 12 — last occurrence
console.log(str.lastIndexOf('Hello', 11)); // 0 — search backwards from index 11

// Find position of file extension
const filename = 'document.pdf.txt';
const lastDot = filename.lastIndexOf('.');
const extension = filename.slice(lastDot + 1);
console.log(extension); // 'txt'
```

### `includes(searchString, fromIndex?)`
Returns boolean if substring exists:

```javascript
const str = 'Hello World';

console.log(str.includes('Hello'));  // true
console.log(str.includes('World'));  // true
console.log(str.includes('xyz'));    // false

// Start from index
console.log(str.includes('World', 6)); // true
console.log(str.includes('Hello', 2)); // false

// Case sensitive
console.log(str.includes('hello'));  // false

// Check if email is valid domain
const email = 'user@gmail.com';
console.log(email.includes('@'));    // true
console.log(email.includes('.'));    // true
```

### `startsWith(searchString, position?)`
Returns boolean if string starts with substring:

```javascript
const str = 'Hello World';

console.log(str.startsWith('Hello'));   // true
console.log(str.startsWith('World'));   // false
console.log(str.startsWith('o W', 4));  // true — position 4

// Validate file path
const filepath = '/home/user/documents/file.txt';
console.log(filepath.startsWith('/'));  // true — absolute path

// Check protocol
const url = 'https://example.com';
console.log(url.startsWith('https://'));  // true
console.log(url.startsWith('http://'));   // false
```

### `endsWith(searchString, length?)`
Returns boolean if string ends with substring:

```javascript
const str = 'Hello World';

console.log(str.endsWith('World'));      // true
console.log(str.endsWith('Hello'));      // false
console.log(str.endsWith('World', 11));  // true

// Validate file extension
const filename = 'document.pdf';
console.log(filename.endsWith('.pdf'));  // true
console.log(filename.endsWith('.txt'));  // false

// Check if array-like
function isArrayLike(str) {
  return str.startsWith('[') && str.endsWith(']');
}
console.log(isArrayLike('[1,2,3]')); // true
console.log(isArrayLike('1,2,3'));  // false
```

### `search(regex)`
Returns index of first match with regex (or -1):

```javascript
const str = 'Hello World 123';

// Search with regex
console.log(str.search(/\d/));      // 12 — first digit
console.log(str.search(/[aeiou]/i)); // 1 — first vowel (case-insensitive)

// Compare with indexOf
console.log(str.indexOf('o'));      // 4
console.log(str.search(/o/));       // 4 — same result

// More complex pattern
const email = 'user123@domain.com';
console.log(email.search(/@/));     // 7
console.log(email.search(/\d+/));   // 4 — digits
```

### `match(regex)` and `matchAll(regex)`
Returns array of matches:

```javascript
const str = 'The price is $10, €8, and ¥500';

// Single match (without global flag)
const match1 = str.match(/[$€¥]/);
console.log(match1);
// ['$', index: 13, input: '...', groups: undefined]

// All matches (with global flag)
const match2 = str.match(/[$€¥]/g);
console.log(match2); // ['$', '€', '¥']

// No match returns null
console.log(str.match(/xyz/)); // null

// Extract all numbers
const numbers = str.match(/\d+/g);
console.log(numbers); // ['10', '8', '500']

// matchAll() — returns iterator (ES2020)
const text = 'test 123 and 456';
const matches = text.matchAll(/\d+/g);

for (const match of matches) {
  console.log(match[0], 'at', match.index);
}
// Output:
// '123' at 5
// '456' at 13

// Detailed info with matchAll
const result = [...text.matchAll(/(\d+)/g)];
result.forEach(m => {
  console.log(m[0], m.index, m.input);
});
```

---

## 4. Extracting Substrings

### `slice(start, end)`
Returns substring from `start` to `end` (end excluded):

```javascript
const str = 'Hello World';

console.log(str.slice(0, 5));   // 'Hello'
console.log(str.slice(6));      // 'World'
console.log(str.slice(0));      // 'Hello World' — from start

// Negative indices count from end
console.log(str.slice(-5));     // 'World' — last 5 chars
console.log(str.slice(-5, -1)); // 'Worl' — last 5, excluding last 1
console.log(str.slice(-10, -6)); // 'Worl'

// Empty string for out of bounds
console.log(str.slice(20));     // ''
console.log(str.slice(-100));   // 'Hello World' — starts from beginning
```

### `substring(start, end)`
Similar to `slice`, but **no negative indices**:

```javascript
const str = 'Hello World';

console.log(str.substring(0, 5));   // 'Hello'
console.log(str.substring(6));      // 'World'

// Negative indices treated as 0
console.log(str.substring(-5));     // 'Hello World' — starts at 0
console.log(str.substring(5, 0));   // 'Hello' — swaps if start > end

// substring() swaps arguments
console.log(str.substring(6, 0));   // 'Hello World' — treated as (0, 6)
console.log(str.slice(6, 0));       // '' — doesn't swap
```

### `substr(start, length)` (Legacy — Avoid)

⚠️ **Deprecated**: Use `slice()` instead

```javascript
const str = 'Hello World';

// Returns substring of specified length
console.log(str.substr(0, 5));  // 'Hello'
console.log(str.substr(6, 5));  // 'World'

// Negative start counted from end
console.log(str.substr(-5, 3)); // 'Wor'

// AVOID THIS — use slice() instead
// slice is more intuitive and standard
console.log(str.slice(0, 5));   // 'Hello' — better
```

### Comparison: `slice` vs `substring` vs `substr`

```javascript
const str = 'JavaScript';

// slice(): supports negative indices
console.log(str.slice(0, 4));      // 'Java'
console.log(str.slice(-6));        // 'Script'

// substring(): no negative, swaps arguments
console.log(str.substring(0, 4));  // 'Java'
console.log(str.substring(-5));    // 'JavaScript' (treated as 0)

// substr(): LENGTH not end (LEGACY)
console.log(str.substr(0, 4));     // 'Java' (length 4)

// **Use slice() — it's the best!**
```

---

## 5. Transforming Strings

### `toUpperCase()` and `toLowerCase()`
```javascript
const str = 'Hello World';

console.log(str.toUpperCase());  // 'HELLO WORLD'
console.log(str.toLowerCase());  // 'hello world'

// With non-ASCII
const greek = 'Σίσυφος'; // Sisyphus in Greek
console.log(greek.toUpperCase()); // 'ΣΊΣΥΦΟΣ'
console.log(greek.toLowerCase()); // 'σίσυφος'

// Case-insensitive comparison
const email1 = 'User@Gmail.Com';
const email2 = 'user@gmail.com';
console.log(email1.toLowerCase() === email2.toLowerCase()); // true
```

### `trim()`, `trimStart()`, `trimEnd()`
Removes whitespace (spaces, tabs, newlines):

```javascript
const str = '  Hello World  ';

// Remove from both ends
console.log(str.trim());       // 'Hello World'
console.log(str.length);       // 15
console.log(str.trim().length); // 11

// Remove from start only
console.log(str.trimStart());  // 'Hello World  '
console.log(str.trimLeft());   // Same as trimStart (alias)

// Remove from end only
console.log(str.trimEnd());    // '  Hello World'
console.log(str.trimRight());  // Same as trimEnd (alias)

// With newlines and tabs
const messy = '\n\t  text  \n\t';
console.log(messy.trim());     // 'text'

// Practical: clean user input
const userInput = '  john.doe@example.com  ';
const cleanEmail = userInput.trim();
console.log(cleanEmail);       // 'john.doe@example.com'
```

### `repeat(count)`
Repeats string count times:

```javascript
console.log('ab'.repeat(3));    // 'ababab'
console.log('x'.repeat(10));    // 'xxxxxxxxxx'
console.log('Hi '.repeat(2));   // 'Hi Hi '

// Edge cases
console.log('a'.repeat(0));     // ''
console.log('a'.repeat(1));     // 'a'

// Practical: create divider
const divider = '='.repeat(50);
console.log('Report');
console.log(divider);
console.log('Content');

// Create indent
const indent = ' '.repeat(4);
console.log(indent + 'Indented text');

// Repeat fractional count (truncated)
console.log('x'.repeat(2.5)); // 'xx' (rounds down to 2)
```

### `padStart(targetLength, padString?)`
Pads string from the **start** to reach target length:

```javascript
const str = '5';

// Pad with spaces (default)
console.log(str.padStart(3));      // '  5'
console.log(str.padStart(5));      // '    5'

// Pad with custom string
console.log(str.padStart(3, '0'));  // '005'
console.log(str.padStart(5, '0'));  // '00005'
console.log(str.padStart(5, 'x'));  // 'xxxx5'

// Already longer than target
console.log('hello'.padStart(3));   // 'hello' — unchanged

// Practical: format numbers
const hours = '8';
const minutes = '5';
console.log(`${hours.padStart(2, '0')}:${minutes.padStart(2, '0')}`);
// '08:05'

// Format invoice numbers
const invoiceNum = '42';
console.log('INV-' + invoiceNum.padStart(6, '0'));
// 'INV-000042'
```

### `padEnd(targetLength, padString?)`
Pads string from the **end** to reach target length:

```javascript
const str = 'hi';

// Pad with spaces
console.log(str.padEnd(5));      // 'hi   '
console.log(str.padEnd(6));      // 'hi    '

// Pad with custom string
console.log(str.padEnd(5, '.'));  // 'hi...'
console.log(str.padEnd(6, '='));  // 'hi===='

// Practical: align text
const items = ['Name', 'Price', 'Qty'];
const prices = [10.5, 25.0, 5.99];

console.log(items[0].padEnd(10) + items[1].padEnd(10) + items[2]);
// 'Name      Price     Qty'
console.log(prices[0].toString().padEnd(10) + prices[1].toString().padEnd(10) + prices[2]);
// '10.5      25        5.99'
```

---

## 6. Replacing Substrings

### `replace(pattern, replacement)`
Replaces **first** match:

```javascript
const str = 'Hello World Hello';

// Replace first occurrence
console.log(str.replace('Hello', 'Hi'));  // 'Hi World Hello'
console.log(str.replace('o', 'O'));      // 'HellO World Hello'

// With regex (case-insensitive)
console.log(str.replace(/hello/i, 'Hi')); // 'Hi World Hello'

// Replace with function
const result = str.replace('Hello', (match) => {
  return match.toUpperCase(); // 'HELLO'
});
console.log(result); // 'HELLO World Hello'

// Replacement patterns
const text = 'John is John';
console.log(text.replace(/(\w+)/, 'Hello $1')); // 'Hello John is John'
```

### `replaceAll(pattern, replacement)` (ES2021)
Replaces **all** matches:

```javascript
const str = 'Hello World Hello';

// Replace all with string
console.log(str.replaceAll('Hello', 'Hi')); // 'Hi World Hi'
console.log(str.replaceAll('o', 'O'));     // 'HellO WOrld HellO'

// Must use /g flag with regex
console.log(str.replaceAll(/Hello/g, 'Hi')); // 'Hi World Hi'

// Replace all with function
const result = str.replaceAll('o', (match) => {
  return match.toUpperCase();
});
console.log(result); // 'HellO WOrld HellO'

// Practical: remove all spaces
const messy = 'hello   world   test';
console.log(messy.replaceAll(' ', ''));  // 'helloworldtest'

// Escape special characters
const text = 'a.b.c';
console.log(text.replace(/\./g, '-'));   // 'a-b-c'
```

### Replacement Patterns

```javascript
const str = 'John Smith';

// $& — the entire match
console.log(str.replace('John', '[$&]'));      // '[John] Smith'

// $1, $2, ... — captured groups
const date = '2026-02-18';
console.log(date.replace(/(\d{4})-(\d{2})-(\d{2})/, '$3/$2/$1'));
// '18/02/2026'

// Function replacement with groups
const text = 'James Brown';
const swapped = text.replace(/(\w+)\s(\w+)/, (match, first, second) => {
  return `${second}, ${first}`;
});
console.log(swapped); // 'Brown, James'

// Complex example: handle capture groups
const html = '<div class="box">Content</div>';
html.replace(/<(\w+)\s*([^>]*)>([^<]*)<\/\1>/g, (match, tag, attrs, content) => {
  console.log({ tag, attrs, content });
  return `<${tag} modified>${content}</${tag}>`;
});
```

---

## 7. Splitting Strings

### `split(separator?, limit?)`
Splits string into array:

```javascript
const str = 'apple,banana,cherry';

// Split by separator
console.log(str.split(','));  // ['apple', 'banana', 'cherry']
console.log(str.split('-'));  // ['apple,banana,cherry'] — no match

// Split by empty string (each character)
console.log('hello'.split(''));  // ['h', 'e', 'l', 'l', 'o']

// No separator (returns array with whole string)
console.log(str.split());        // ['apple,banana,cherry']

// Limit results
console.log(str.split(',', 1));  // ['apple']
console.log(str.split(',', 2));  // ['apple', 'banana']

// Split by regex
const csv = 'John,25,New York';
console.log(csv.split(/,\s*/)); // ['John', '25', 'New York']

// Split on whitespace
const sentence = 'Hello   World   Test';
console.log(sentence.split(/\s+/)); // ['Hello', 'World', 'Test']

// Split by multiple separators
const text = 'a,b;c:d';
console.log(text.split(/[,;:]/)); // ['a', 'b', 'c', 'd']
```

### Practical Split Examples

```javascript
// Parse CSV
const csvLine = 'John,30,Developer';
const [name, age, role] = csvLine.split(',');
console.log(name, age, role); // 'John' '30' 'Developer'

// Parse URL path
const path = '/user/profile/settings';
const parts = path.split('/').filter(p => p); // remove empty strings
console.log(parts); // ['user', 'profile', 'settings']

// Parse email domain
const email = 'user@example.com';
const [local, domain] = email.split('@');
console.log({ local, domain }); // { local: 'user', domain: 'example.com' }

// Split and rejoin (trim + normalize spaces)
const messy = 'hello    world   test';
const clean = messy.split(/\s+/).join(' ');
console.log(clean); // 'hello world test'
```

---

## 8. Template Literals

### Backtick Syntax
Template literals use backticks instead of quotes:

```javascript
const name = 'Alice';
const age = 30;

// Regular string concatenation
const old = 'Hello ' + name + ', you are ' + age + ' years old';

// Template literal (much cleaner!)
const modern = `Hello ${name}, you are ${age} years old`;

console.log(modern);
// 'Hello Alice, you are 30 years old'
```

### Embedding Expressions
Any JavaScript expression can be embedded:

```javascript
const x = 10;
const y = 20;

// Arithmetic
console.log(`Sum: ${x + y}`);           // 'Sum: 30'
console.log(`Product: ${x * y}`);       // 'Product: 200'

// Function calls
function greet(name) {
  return `Hello, ${name}!`;
}
console.log(`${greet('Bob')}`);         // 'Hello, Bob!'

// Ternary operators
const time = 14;
console.log(`Good ${time < 12 ? 'morning' : 'afternoon'}`);
// 'Good afternoon'

// Method calls
const str = 'hello';
console.log(`Uppercase: ${str.toUpperCase()}`);
// 'Uppercase: HELLO'

// Objects and arrays
const person = { name: 'Charlie', work: 'Engineer' };
console.log(`${person.name} is a ${person.work}`);
// 'Charlie is a Engineer'

const nums = [1, 2, 3];
console.log(`Numbers: ${nums.join(', ')}`);
// 'Numbers: 1, 2, 3'

// Nested template literals
const level = 2;
console.log(`${'='.repeat(10)} Level ${level} ${'='.repeat(10)}`);
// '========== Level 2 =========='
```

### Multi-line Strings

```javascript
// Old way (concatenation or escape)
const old = 'Line 1\n' +
            'Line 2\n' +
            'Line 3';

// Template literal (preserves formatting)
const modern = `Line 1
Line 2
Line 3`;

console.log(modern);
// Line 1
// Line 2
// Line 3

// HTML template
const html = `
<div class="card">
  <h2>Title</h2>
  <p>Description</p>
</div>
`;
console.log(html);

// JSON-like structure
const config = `
{
  "name": "app",
  "version": "1.0",
  "debug": true
}
`;
console.log(config);

// Multi-line with expressions
const table = `
┌────────┬────────┐
│ Name   │ Score  │
├────────┼────────┤
│ Alice  │  95    │
│ Bob    │  87    │
└────────┴────────┘
`;
console.log(table);
```

### Escaping in Template Literals

```javascript
// Backticks need escaping inside template literals
const str = `This is a \`quoted\` word`;
console.log(str); // This is a `quoted` word

// Dollar signs with ${ need escaping when not immediate
const price = 100;
console.log(`Price: $${price}`); // Price: $100
console.log(`Cost: \${price}`);  // Cost: ${price}

// Other escapes work normally
console.log(`Line 1\nLine 2`);   // Line 1 (newline) Line 2
console.log(`Tab\tseparated`);   // Tab    separated
```

---

## 9. Tagged Template Literals

### What are Tagged Templates?

A **tagged template** is a function that receives the string segments and expressions separately:

```javascript
// Define a tag function
function tag(strings, ...values) {
  console.log(strings); // Array of string segments
  console.log(values);  // Array of expression values
}

const name = 'Alice';
const age = 30;

// Call the tag with template literal
tag`Hello ${name}, you are ${age}`;

// Output:
// strings: ['Hello ', ', you are ', '']
// values: ['Alice', 30]
```

### Structure of Tag Functions

```javascript
function myTag(strings, ...expressions) {
  // strings: array of literal parts
  //   - strings[0]: before first ${}
  //   - strings[1]: between {} and {}
  //   - strings[n]: after last {}
  
  // expressions: array of evaluated expressions
  
  // Usually return a modified string
  return result;
}

const x = 5;
const y = 10;

myTag`${x} plus ${y} equals ${x + y}`;
// strings: ['', ' plus ', ' equals ', '']
// expressions: [5, 10, 15]
```

### Practical Tagged Template Examples

#### HTML Escaping

```javascript
function html(strings, ...values) {
  let result = '';
  for (let i = 0; i < strings.length; i++) {
    result += strings[i];
    if (i < values.length) {
      // Escape HTML special characters
      const escaped = String(values[i])
        .replace(/&/g, '&amp;')
        .replace(/</g, '&lt;')
        .replace(/>/g, '&gt;')
        .replace(/"/g, '&quot;');
      result += escaped;
    }
  }
  return result;
}

const user = '<script>alert("xss")</script>';
console.log(html`<p>User: ${user}</p>`);
// <p>User: &lt;script&gt;alert(&quot;xss&quot;)&lt;/script&gt;</p>
```

#### SQL Query Builder

```javascript
function sql(strings, ...values) {
  let query = '';
  for (let i = 0; i < strings.length; i++) {
    query += strings[i];
    if (i < values.length) {
      // Properly escape SQL values
      const value = values[i];
      if (typeof value === 'string') {
        query += `'${value.replace(/'/g, "''")}'`;
      } else if (value === null) {
        query += 'NULL';
      } else {
        query += value;
      }
    }
  }
  return query;
}

const name = "O'Brien";
const age = 30;
const query = sql`SELECT * FROM users WHERE name = ${name} AND age > ${age}`;
console.log(query);
// SELECT * FROM users WHERE name = 'O''Brien' AND age > 30
```

#### Highlighting/Styling

```javascript
function highlight(strings, ...values) {
  let result = '';
  for (let i = 0; i < strings.length; i++) {
    result += strings[i];
    if (i < values.length) {
      result += `\x1b[1m${values[i]}\x1b[0m`; // Bold ANSI
    }
  }
  return result;
}

const user = 'Alice';
const action = 'logged in';
console.log(highlight`User ${user} ${action} successfully`);
// Shows "Alice" and "logged in" in bold in terminal
```

#### Localization/Translation

```javascript
function i18n(strings, ...values) {
  const translations = {
    'Hello , you have  messages': 'Bonjour {0}, vous avez {1} messages'
  };
  
  let template = '';
  for (let i = 0; i < strings.length; i++) {
    template += strings[i];
    if (i < values.length) {
      template += `{${i}}`;
    }
  }
  
  let translated = translations[template] || template;
  
  for (let i = 0; i < values.length; i++) {
    translated = translated.replace(`{${i}}`, values[i]);
  }
  
  return translated;
}

const user = 'Alice';
const messages = 5;
console.log(i18n`Hello ${user}, you have ${messages} messages`);
// 'Bonjour Alice, vous avez 5 messages'
```

---

## 10. Unicode and Special Characters

### Unicode Escape Sequences

```javascript
// 16-bit Unicode escape: \uXXXX
console.log('\u0041'); // 'A' (ASCII 41 in hex)
console.log('\u03B1'); // 'α' (Greek alpha)
console.log('\u4E2D');  // '中' (Chinese character)

// Code point escape: \u{XXXXX} (for code points > 16 bits)
console.log('\u{1F600}'); // '😀' (Grinning face emoji)
console.log('\u{1F923}'); // '🤣' (Rolling eyes emoji)
console.log('\u{1F30E}'); // '🌎' (Earth with Americas emoji)

// Variables
const codePoint = 0x1F600;
console.log(`Emoji: \u{${codePoint}}`); // May not work; use String.fromCodePoint()
```

### `String.fromCharCode()` and `String.fromCodePoint()`

```javascript
// fromCharCode() — 16-bit units (legacy)
console.log(String.fromCharCode(65));        // 'A'
console.log(String.fromCharCode(0x03B1));    // 'α'
console.log(String.fromCharCode(0x4E2D));    // '中'

// fromCharCode() with emojis — may produce garbled output
console.log(String.fromCharCode(0xD83D, 0xDE00)); // '😀' — requires two codes

// fromCodePoint() — handles full Unicode (ES2015)
console.log(String.fromCodePoint(65));       // 'A'
console.log(String.fromCodePoint(0x1F600));  // '😀' — single code!
console.log(String.fromCodePoint(0x03B1, 0x03B2, 0x03B3)); // 'αβγ'

// The difference
String.fromCharCode(0x1F600); // May produce unexpected result
String.fromCodePoint(0x1F600); // Correctly produces '😀'
```

### `charCodeAt()` and `codePointAt()`

Returns the numeric code of a character:

```javascript
const str = 'A';

// charCodeAt() — 16-bit
console.log(str.charCodeAt(0)); // 65

// With emojis — only gets first unit
const emoji = '😀';
console.log(emoji.charCodeAt(0)); // 55357 (first 16-bit unit)
console.log(emoji.charCodeAt(1)); // 56832 (second 16-bit unit)

// codePointAt() — full Unicode (ES2015)
console.log(emoji.codePointAt(0)); // 128512 (correct code point)

// Working with strings
const text = 'ABC';
for (let char of text) {
  console.log(String.fromCodePoint(char.codePointAt(0)));
}
// A, B, C

// Practical: check if character is emoji
function isEmoji(str) {
  const codePoint = str.codePointAt(0);
  return codePoint > 0x1F000; // Simplified check
}

console.log(isEmoji('😀')); // true
console.log(isEmoji('A'));  // false
```

### Iterating Code Points

With emojis, `.length` can be misleading. Use iteration:

```javascript
const text = 'Hi 😀';

// Wrong: length includes surrogates
console.log(text.length); // 4 — not 3!

// Correct: use for...of (iterates code points)
let count = 0;
for (const char of text) {
  console.log(char);
  count++;
}
// H, i, (space), 😀
console.log(count); // 4 — correct!

// Convert to array
const chars = [...text]; // or Array.from(text)
console.log(chars);      // ['H', 'i', ' ', '😀']
console.log(chars.length); // 4 — correct!

// Practical: reverse string with emojis
const original = 'Hi 😀';
const reversed1 = original.split('').reverse().join('');
console.log(reversed1); // Broken emoji!

const reversed2 = [...original].reverse().join('');
console.log(reversed2); // 😀 iH — correct!
```

### Normalizing Unicode

Some characters can be represented multiple ways:

```javascript
// Three different ways to represent "é"
const composed = 'é';      // Single character U+00E9
const decomposed = 'e\u0301'; // 'e' + combining acute accent

console.log(composed === decomposed); // false — different!
console.log(composed.length); // 1
console.log(decomposed.length); // 2

// Normalize to same form
console.log(composed.normalize('NFC')); // Composed form
console.log(decomposed.normalize('NFC')); // Converts to composed
console.log(composed.normalize('NFC') === decomposed.normalize('NFC')); // true

// Four normalization forms
console.log('café'.normalize('NFC')); // Composed (default)
console.log('café'.normalize('NFD')); // Decomposed
console.log('café'.normalize('NFKC')); // Compatibility composed
console.log('café'.normalize('NFKD')); // Compatibility decomposed
```

---

## Summary: String Methods Quick Reference

| Category | Methods |
|----------|---------|
| **Search** | `indexOf`, `lastIndexOf`, `includes`, `startsWith`, `endsWith`, `search`, `match`, `matchAll` |
| **Extract** | `slice`, `substring`, `substr` |
| **Transform** | `toUpperCase`, `toLowerCase`, `trim`, `trimStart`, `trimEnd`, `repeat`, `padStart`, `padEnd` |
| **Replace** | `replace`, `replaceAll` |
| **Split/Join** | `split`, `charAt`, `concat` |
| **Unicode** | `charCodeAt`, `codePointAt`, `String.fromCharCode`, `String.fromCodePoint`, `normalize` |

---

## Best Practices

✅ **Use template literals for string interpolation** — Cleaner than concatenation

✅ **Use `slice()` for substring extraction** — Supports negative indices

✅ **Use `includes()` for search** — More readable than `indexOf() !== -1`

✅ **Use `padStart()`/`padEnd()` for formatting** — Useful for tables and alignment

✅ **Use `.trim()` for user input** — Always clean data at boundaries

✅ **Use `String.fromCodePoint()` and `codePointAt()` for Unicode** — Handles emojis correctly

✅ **Use `for...of` to iterate strings with emojis** — Correctly iterates code points

✅ **Use `split()` then `join()` for complex replacements** — More flexible than `replace()`

---

## Common Gotchas

❌ **`.length` doesn't match character count for emojis**
```javascript
const emoji = '😀';
console.log(emoji.length); // 2 — not 1!
console.log([...emoji].length); // 1 — correct
```

❌ **Strings are immutable**
```javascript
const str = 'hello';
str[0] = 'H'; // Doesn't work
// Create new string instead:
const modified = 'H' + str.slice(1);
```

❌ **`split('')` breaks emojis**
```javascript
const text = '😀';
console.log(text.split('')); // ['\uD83D', '\uDE00'] — broken!
console.log([...text]); // ['😀'] — correct
```

❌ **`replace()` only replaces first match**
```javascript
const str = 'a-a-a';
console.log(str.replace('-', '_')); // 'a_a-a' — only first
console.log(str.replaceAll('-', '_')); // 'a_a_a' — all
// Or use regex with /g flag
console.log(str.replace(/-/g, '_')); // 'a_a_a'
```

❌ **`indexOf()` returns -1, not boolean**
```javascript
// Don't do this
if (str.indexOf('foo')) { ... } // Wrong! -1 is falsy but 0 is falsy

// Do this instead
if (str.indexOf('foo') !== -1) { ... }
if (str.includes('foo')) { ... } // Better!
```

❌ **Template literals inside template literals are tricky**
```javascript
const greeting = `Hello ${`World`}`; // Works
const nested = `Outer ${`Inner ${value}`}`; // Each level needs its own function
```

❌ **Unicode escape sequences with dynamic values**
```javascript
const code = 0x1F600;
// This doesn't work:
console.log(`\u{code}`); // Literal string "\u{code}"

// Do this instead:
console.log(String.fromCodePoint(code)); // '😀'
```
