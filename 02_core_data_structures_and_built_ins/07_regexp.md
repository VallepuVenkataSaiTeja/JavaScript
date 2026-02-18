# 2.7 Regular Expressions (RegExp)

## What is a Regular Expression?

A **Regular Expression** (RegExp) is a pattern used to match, search, and manipulate strings. It defines a sequence of characters that represent a search pattern. Regular expressions are powerful tools for text processing, validation, and transformation.

```javascript
const pattern = /hello/;
console.log(pattern.test('hello world')); // true
console.log(pattern.test('goodbye'));    // false
```

---

## 1. Creating Regular Expressions

### Literal Syntax (Most Common)

Use forward slashes to define regex patterns:

```javascript
// Simple pattern
const regex1 = /hello/;

// Pattern with flags
const regex2 = /world/i; // case-insensitive

// Complex pattern
const regex3 = /\d{3}-\d{3}-\d{4}/; // Phone number

console.log(regex1.test('hello')); // true
console.log(regex2.test('WORLD')); // true
console.log(regex3.test('555-123-4567')); // true
```

### Constructor Syntax (For Dynamic Patterns)

Use the `RegExp` constructor when pattern comes from a variable:

```javascript
// Literal pattern
const pattern1 = new RegExp('hello');
console.log(pattern1.test('hello')); // true

// With flags
const pattern2 = new RegExp('world', 'i');
console.log(pattern2.test('WORLD')); // true

// Dynamic pattern (necessary for variables)
const searchTerm = 'javascript';
const flag = 'i'; // case-insensitive
const regex = new RegExp(searchTerm, flag);
console.log(regex.test('JavaScript')); // true

// Escaping special characters in constructor
const pattern3 = new RegExp('\\d{3}-\\d{3}-\\d{4}'); // Phone
// Note: double backslash in constructor strings!
```

### Literal vs Constructor

```javascript
// Literal: / at start and end
const lit = /[abc]/;

// Constructor: string with pattern
const con = new RegExp('[abc]');

// They're equivalent
console.log(lit.test('a')); // true
console.log(con.test('a')); // true

// Constructor is necessary for dynamic patterns
function createPattern(text) {
  return new RegExp(text, 'i'); // Can't use literal syntax
}

const regex = createPattern('hello');
console.log(regex.test('HELLO')); // true
```

---

## 2. Flags

Flags modify how the pattern matches. Can be combined:

### `g` — Global

Matches **all** occurrences, not just first:

```javascript
// Without g (finds first only)
const text = 'cat cat cat';
console.log(text.match(/cat/)); // ['cat'] — first only!

// With g (finds all)
console.log(text.match(/cat/g)); // ['cat', 'cat', 'cat'] — all!

// In exec() without g
const regex1 = /cat/;
console.log(regex1.exec(text)); // ['cat'] then ['cat'] then ['cat']
console.log(regex1.lastIndex); // 0 — resets each time

// In exec() with g
const regex2 = /cat/g;
console.log(regex2.exec(text)); // ['cat'] — index 0
console.log(regex2.lastIndex); // 3
console.log(regex2.exec(text)); // ['cat'] — index 4
console.log(regex2.lastIndex); // 7
```

### `i` — Case-Insensitive

Matches regardless of uppercase/lowercase:

```javascript
const regex1 = /hello/;
console.log(regex1.test('Hello')); // false

const regex2 = /hello/i;
console.log(regex2.test('Hello')); // true
console.log(regex2.test('HELLO')); // true
console.log(regex2.test('HeLLo')); // true

// Useful for searches
const email = 'Alice@Example.COM';
console.log(/^[a-z]+@[a-z]+\.[a-z]+$/i.test(email)); // true
```

### `m` — Multiline

Treats `^` and `$` as line boundaries, not string boundaries:

```javascript
const text = `line1
line2
line3`;

// Without m: ^ and $ match string boundaries only
const regex1 = /^line/;
console.log(text.match(regex1)); // ['line1'] — only at start

// With m: ^ and $ match line boundaries
const regex2 = /^line/m;
console.log(text.match(regex2)); // ['line1'] — still first

// Better example:
const regex3 = /^line\d/gm;
console.log(text.match(regex3)); // ['line1', 'line2', 'line3'] — all lines!
```

### `s` — DotAll

Makes `.` match newline characters:

```javascript
const text = `hello
world`;

// Without s: . doesn't match newline
const regex1 = /hello.world/;
console.log(regex1.test(text)); // false — dot won't match newline

// With s: . matches everything including newline
const regex2 = /hello.world/s;
console.log(regex2.test(text)); // true — dot matches newline

// Practical: match across multiple lines
const html = `<p>
  Some text here
</p>`;

const regex3 = /<p>.*?<\/p>/s; // Without s fails
const regex4 = /<p>.*?<\/p>/s; // With s works
console.log(regex4.test(html)); // true
```

### `u` — Unicode

Properly handles Unicode characters and escape sequences:

```javascript
// Without u: some Unicode may not work correctly
const emoji = '😀';
const regex1 = /./;
console.log(emoji.match(regex1)); // May be broken

// With u: proper Unicode support
const regex2 = /./u;
console.log('😀'.match(regex2)); // ['😀']

// Unicode property escapes require u flag
const regex3 = /\p{Letter}/u;
console.log(regex3.test('a')); // true
console.log(regex3.test('α')); // true (Greek)
console.log(regex3.test('中')); // true (Chinese)
```

### `y` — Sticky

Matches only at `lastIndex` position:

```javascript
const text = 'hello';

const regex = /l/y;
regex.lastIndex = 2;
console.log(regex.exec(text)); // ['l'] at position 2

regex.lastIndex = 0;
console.log(regex.exec(text)); // null — l is not at position 0

// Useful for tokenizers
const tokenRegex = /\d+|\w+|[+*]/y;
const input = '123 + abc';
let match;
const tokens = [];

while ((match = tokenRegex.exec(input)) !== null) {
  tokens.push(match[0]);
}
console.log(tokens); // ['123', '+', 'abc']
```

### `v` — ES2024 Unicode Sets

Extended Unicode support with character sets:

```javascript
// with v flag, can use extended character classes
const regex = /[\p{Letter}\p{Mark}]/v;
console.log(regex.test('a')); // true
console.log(regex.test('ñ')); // true (letter with mark)

// Character set subtraction
const noDigits = /[^\d]/v;
console.log(noDigits.test('a')); // true
console.log(noDigits.test('5')); // false
```

### Combining Flags

```javascript
// Multiple flags together
const regex = /hello/gim; // global, case-insensitive, multiline

// In constructor
const regex2 = new RegExp('hello', 'gim');

// Access flags as properties
const reg = /test/gi;
console.log(reg.global); // true
console.log(reg.ignoreCase); // true
console.log(reg.multiline); // false
console.log(reg.flags); // "gi"
```

---

## 3. Pattern Syntax

### Character Classes

#### Specific Characters `[abc]`

```javascript
const regex = /[aeiou]/; // Match any vowel
console.log('hello'.match(regex)); // ['e']

const regex2 = /[abc]/g; // Match a, b, or c
console.log('cabbage'.match(regex2)); // ['c', 'a', 'b', 'b', 'a']

// Ranges
const digit = /[0-9]/; // Match 0-9
const letter = /[a-z]/; // Match a-z
const upper = /[A-Z]/; // Match A-Z
const both = /[a-zA-Z]/; // Match any letter

// Negation [^abc]
const notVowel = /[^aeiou]/g; // Match non-vowels
console.log('hello'.match(notVowel)); // ['h', 'l', 'l']
```

#### Shorthand Classes

```javascript
// \d — digit (0-9)
console.log('test123'.match(/\d/g)); // ['1', '2', '3']

// \D — non-digit
console.log('test123'.match(/\D/g)); // ['t', 'e', 's', 't']

// \w — word character (a-z, A-Z, 0-9, _)
console.log('hello_world123!'.match(/\w/g)); // ['h','e',...,'3']

// \W — non-word character
console.log('hello_world!'.match(/\W/g)); // ['!']

// \s — whitespace (space, tab, newline, etc.)
console.log('hello world'.match(/\s/g)); // [' ']

// \S — non-whitespace
console.log('hello world'.match(/\S/g)); // ['h','e',...,'d']

// . — any character except newline
const regex = /h.llo/;
console.log('hello'.match(regex)); // ['hello']
console.log('hallo'.match(regex)); // ['hallo']
```

### Quantifiers

#### `*` — 0 or More

```javascript
const regex = /ab*c/; // a, then 0+ b's, then c
console.log('ac'.match(regex)); // ['ac'] — 0 b's
console.log('abc'.match(regex)); // ['abc'] — 1 b
console.log('abbc'.match(regex)); // ['abbc'] — 2 b's
console.log('abbbc'.match(regex)); // ['abbbc'] — 3 b's
console.log('xyz'.match(regex)); // null — no match
```

#### `+` — 1 or More

```javascript
const regex = /ab+c/; // a, then 1+ b's, then c
console.log('ac'.match(regex)); // null — needs at least 1 b
console.log('abc'.match(regex)); // ['abc'] — 1+ b's
console.log('abbc'.match(regex)); // ['abbc'] — matches
console.log('abbbc'.match(regex)); // ['abbbc'] — matches

// Practical: email validation needs +
const email = /^[a-z]+@[a-z]+\.[a-z]+$/i;
console.log(email.test('user@example.com')); // true
```

#### `?` — 0 or 1

```javascript
const regex = /ab?c/; // a, then optional b, then c
console.log('ac'.match(regex)); // ['ac'] — 0 b's
console.log('abc'.match(regex)); // ['abc'] — 1 b
console.log('abbc'.match(regex)); // null — too many b's

// Optional hyphen in phone
const phone = /\d{3}-?\d{3}-?\d{4}/;
console.log(phone.test('5551234567')); // true
console.log(phone.test('555-123-4567')); // true
```

#### `{n,m}` — Specific Count

```javascript
const regex = /a{2,4}/; // 2 to 4 a's
console.log('a'.match(regex)); // null
console.log('aa'.match(regex)); // ['aa']
console.log('aaa'.match(regex)); // ['aaa']
console.log('aaaa'.match(regex)); // ['aaaa']
console.log('aaaaa'.match(regex)); // ['aaaa'] — matches 4, ignores 5th

// Exactly n
const exact = /a{3}/; // exactly 3 a's
console.log('aaa'.match(exact)); // ['aaa']

// n or more
const atLeast = /a{3,}/; // 3 or more a's
console.log('aaa'.match(atLeast)); // ['aaa']
console.log('aaaa'.match(atLeast)); // ['aaaa']

// Practical: password strength
const strongPassword = /^(?=.*[A-Z])(?=.*[a-z])(?=.*\d)(?=.*[!@#$%]).{8,}$/;
// At least 1 uppercase, 1 lowercase, 1 digit, 1 special, 8+ chars
```

#### Greedy vs Non-Greedy

```javascript
const text = 'aaa';

// Greedy (default): match as much as possible
const greedy = /a+/;
console.log(text.match(greedy)); // ['aaa'] — all 3

// Non-greedy: match as little as possible
const nonGreedy = /a+?/;
console.log(text.match(nonGreedy)); // ['a'] — just 1

// Practical: HTML tags
const html = '<div>content</div>';

// Greedy: matches too much
console.log(html.match(/<.*>/)); // ['<div>content</div>']

// Non-greedy: correct
console.log(html.match(/<.*?>/)); // ['<div>']
```

### Anchors

#### `^` — Start of String/Line

```javascript
const regex = /^hello/;
console.log('hello world'.match(regex)); // ['hello']
console.log('say hello'.match(regex)); // null — not at start

// With multiline flag
const text = `hello
world`;
const regexM = /^hello/m;
console.log(text.match(regexM)); // ['hello'] — matches at start

// Practical: must start with
const validUsername = /^[a-z_][a-z0-9_]*$/i;
console.log(validUsername.test('user_123')); // true
console.log(validUsername.test('_user')); // true
console.log(validUsername.test('123user')); // false
```

#### `$` — End of String/Line

```javascript
const regex = /world$/;
console.log('hello world'.match(regex)); // ['world']
console.log('world hello'.match(regex)); // null — not at end

// Practical: file extension
const validImage = /\.(jpg|png|gif)$/i;
console.log(validImage.test('photo.jpg')); // true
console.log(validImage.test('photo.JPG')); // true
console.log(validImage.test('photo.txt')); // false
```

#### `\b` — Word Boundary

```javascript
const regex = /\bcat\b/;
console.log('cat sat on mat'.match(regex)); // ['cat']
console.log('caterpillar'.match(regex)); // null — cat is part of word

// Without boundary
const regex2 = /cat/;
console.log('caterpillar'.match(regex2)); // ['cat'] — matches anywhere

// Practical: whole words only
const text = 'The quick brown fox';
console.log(/\bfox\b/.test(text)); // true
console.log(/\bfo\b/.test(text)); // false
```

### Alternation `|`

```javascript
const regex = /cat|dog/;
console.log('I have a cat'.match(regex)); // ['cat']
console.log('I have a dog'.match(regex)); // ['dog']
console.log('I have a bird'.match(regex)); // null

// Multiple alternatives
const color = /red|green|blue/;
console.log(color.test('green')); // true

// With groups for clarity
const protocol = /(http|https|ftp):\/\//;
console.log(protocol.test('https://example.com')); // true
```

### Groups

#### Capturing Groups `()`

Groups capture substrings for later use:

```javascript
const regex = /(\w+)@(\w+)\.(\w+)/;
const match = 'user@example.com'.match(regex);
console.log(match);
// ['user@example.com', 'user', 'example', 'com']
// [0] full match, [1] first group, [2] second group, [3] third group

// Access groups separately
const [full, user, domain, tld] = match;
console.log(user); // 'user'
console.log(domain); // 'example'
console.log(tld); // 'com'

// With exec()
const regex2 = /(\d{2})-(\d{2})-(\d{4})/;
const result = regex2.exec('12-31-2026');
console.log(result[1]); // '12' (month)
console.log(result[2]); // '31' (day)
console.log(result[3]); // '2026' (year)
```

#### Non-Capturing Groups `(?:)`

Don't capture, just group:

```javascript
// Capturing
const regex1 = /(cat|dog) food/;
const match1 = 'cat food'.match(regex1);
console.log(match1[1]); // 'cat' — captured

// Non-capturing
const regex2 = /(?:cat|dog) food/;
const match2 = 'cat food'.match(regex2);
console.log(match2[1]); // undefined — not captured

// Useful when you need grouping for quantifiers but not capture
const html = /(?:<div>.*?<\/div>)+/s;
// Groups for +, but doesn't capture individual divs
```

#### Named Groups `(?<name>)`

Capture with meaningful names:

```javascript
const regex = /(?<month>\d{2})-(?<day>\d{2})-(?<year>\d{4})/;
const match = '12-31-2026'.match(regex);

// Access by name
console.log(match.groups.month); // '12'
console.log(match.groups.day); // '31'
console.log(match.groups.year); // '2026'

// More readable than numbered groups
const emailRegex = /(?<user>[a-z]+)@(?<domain>[a-z]+)\.(?<tld>[a-z]+)/i;
const emailMatch = 'alice@example.com'.match(emailRegex);
console.log(emailMatch.groups.user); // 'alice'
console.log(emailMatch.groups.domain); // 'example'
console.log(emailMatch.groups.tld); // 'com'
```

### Lookahead

#### Positive Lookahead `(?=)`

Assert that what follows matches (without consuming):

```javascript
// Find number followed by 'px'
const regex = /\d+(?=px)/;
console.log('width: 100px'.match(regex)); // ['100']
console.log('100px'.match(regex)); // ['100']
console.log('100'.match(regex)); // null — no 'px' after

// Practical: currency validation
const currency = /\d+(?=\$)/;
console.log('$100'.match(currency)); // null — $ before 100
console.log('100$'.match(currency)); // ['100'] — matches

// Better: find all prices
const prices = /\$(\d+)/g;
console.log('Items: $10, $20, $30'.match(prices)); // ['$10', '$20', '$30']
```

#### Negative Lookahead `(?!)`

Assert that what follows does NOT match:

```javascript
// Find 'test' not followed by 'ing'
const regex = /test(?!ing)/;
console.log('testing'.match(regex)); // null — followed by 'ing'
console.log('test case'.match(regex)); // ['test'] — not followed by 'ing'

// Practical: find all numbers not followed by '%'
const notPercent = /\d+(?!%)/;
console.log('100% complete, 50 items'.match(notPercent)); // ['50']

// Password without 'password' word
const notPassword = /^(?!.*password)(?=.*[A-Z])(?=.*\d).{8,}$/;
```

### Lookahead Lookbehind (if supported)

Some engines support lookbehind:

```javascript
// Positive lookbehind: preceded by
const regex = /(?<=price: )\d+/;
console.log('price: 100'.match(regex)); // ['100']
console.log('100'.match(regex)); // null

// Negative lookbehind: not preceded by
const regex2 = /(?<!error: )\d+/;
```

### Backreferences

Reference captured groups with `\1`, `\2`, etc.:

```javascript
// Match repeated word
const regex = /(\w+)\s+\1/;
console.log('hello hello'.match(regex)); // ['hello hello']
console.log('hello world'.match(regex)); // null

// Find duplicate words
const text = 'This this is is a test.';
console.log(text.match(/(\w+)\s+\1/g)); // ['This this', 'is is']

// HTML tag validation
const tagRegex = /<(\w+)>.*?<\/\1>/;
console.log('<div>content</div>'.match(tagRegex)); // ['<div>content</div>']
console.log('<div>content</span>'.match(tagRegex)); // null — mismatched

// With named groups
const dateRegex = /(?<day>\d{2})-(?<month>\d{2})-\k<year>\d{4}/;
// \k<name> references named group
```

---

## 4. RegExp Methods

### `test(string)` — Boolean Test

Returns true if pattern matches, false otherwise:

```javascript
const regex = /hello/;
console.log(regex.test('hello world')); // true
console.log(regex.test('goodbye')); // false

// With flags
const caseInsensitive = /hello/i;
console.log(caseInsensitive.test('HELLO')); // true

// With global flag (affects lastIndex)
const globalRegex = /o/g;
console.log(globalRegex.test('foo')); // true — first 'o'
console.log(globalRegex.lastIndex); // 2
console.log(globalRegex.test('foo')); // true — second 'o'
console.log(globalRegex.lastIndex); // 3
console.log(globalRegex.test('foo')); // false — no more matches
console.log(globalRegex.lastIndex); // 0 — reset
```

### `exec(string)` — Detailed Match

Returns array with match details, or null:

```javascript
const regex = /\d+/;
const result = regex.exec('I have 123 apples');
// [
//   '123',      // [0] full match
//   index: 7,   // position of match
//   input: 'I have 123 apples', // original string
//   groups: undefined
// ]

console.log(result[0]); // '123'
console.log(result.index); // 7
console.log(result.input); // 'I have 123 apples'

// With capturing groups
const emailRegex = /(\w+)@(\w+)/;
const emailResult = 'user@example'.match(emailRegex);
console.log(emailResult[1]); // 'user'
console.log(emailResult[2]); // 'example'

// With global flag (loops through all matches)
const globalRegex = /\d+/g;
let match;
const numbers = [];
while ((match = globalRegex.exec('123 456 789')) !== null) {
  numbers.push(match[0]);
  console.log(`Found ${match[0]} at index ${match.index}`);
}
console.log(numbers); // ['123', '456', '789']
```

---

## 5. String Methods with RegExp

### `match(regex)` — Find Matches

Returns array of matches or null:

```javascript
const str = 'hello world hello';

// Without global flag
const regex1 = /hello/;
console.log(str.match(regex1)); // ['hello'] — first only

// With global flag
const regex2 = /hello/g;
console.log(str.match(regex2)); // ['hello', 'hello'] — all matches

// No match
console.log(str.match(/xyz/)); // null

// With capturing groups
const email = 'Contact: user@example.com';
const emailRegex = /(\w+)@(\w+)\.(\w+)/;
const emailMatch = email.match(emailRegex);
console.log(emailMatch[1]); // 'user'
```

### `matchAll(regex)` — Iterator of Matches

Returns iterator of all matches (requires `g` flag):

```javascript
const str = 'test 123 and 456';
const regex = /(\d+)/g;

// matchAll returns iterator
for (const match of str.matchAll(regex)) {
  console.log(match[0]); // '123', then '456'
  console.log(match.index); // 5, then 13
}

// Convert to array
const matches = [...str.matchAll(/\d+/g)];
console.log(matches.length); // 2
console.log(matches[0][0]); // '123'
```

### `search(regex)` — Find Index

Returns index of first match, or -1:

```javascript
const str = 'hello world';

console.log(str.search(/world/)); // 6

// Case-insensitive
console.log(str.search(/WORLD/i)); // 6

// No match
console.log(str.search(/xyz/)); // -1

// Useful for checking position
if (str.search(/\d/) !== -1) {
  console.log('String contains digits');
}
```

### `replace(pattern, replacement)` — Replace First

Replaces first match with replacement:

```javascript
const str = 'hello hello world';

// Replace first occurrence
console.log(str.replace(/hello/, 'hi'));
// 'hi hello world'

// With global flag — replace all
console.log(str.replace(/hello/g, 'hi'));
// 'hi hi world'

// Replacement patterns
const matched = str.replace(/(\w+)\s+(\w+)/, '$2 $1');
// '$1' = first group, '$2' = second group
console.log(matched); // 'hello world hello world'

// $& is entire match
console.log(str.replace(/hello/g, '[$&]'));
// '[hello] [hello] world'

// Replacement function
console.log(str.replace(/\w+/g, (match) => {
  return match.toUpperCase();
}));
// 'HELLO HELLO WORLD'

// Function with groups
const dateStr = '2026-02-18';
const formattedDate = dateStr.replace(/(\d{4})-(\d{2})-(\d{2})/, (match, year, month, day) => {
  return `${day}/${month}/${year}`;
});
console.log(formattedDate); // '18/02/2026'
```

### `replaceAll(pattern, replacement)` — Replace All

Replaces all matches (equivalent to `replace(..., 'g')`):

```javascript
const str = 'cat cat cat';

// With regex (must have g flag)
console.log(str.replaceAll(/cat/g, 'dog'));
// 'dog dog dog'

// With string (no g flag needed!)
console.log(str.replaceAll('cat', 'dog'));
// 'dog dog dog'

// replaceAll doesn't need g flag if you use string literal
const text = 'apple apple apple';
console.log(text.replaceAll('apple', 'orange'));
// 'orange orange orange'
```

### `split(pattern, limit?)` — Split by Pattern

Splits string using regex pattern:

```javascript
// Simple split
console.log('a,b,c'.split(/,/));
// ['a', 'b', 'c']

// Multiple separators
console.log('a,b;c:d'.split(/[,;:]/));
// ['a', 'b', 'c', 'd']

// Whitespace
console.log('hello   world   test'.split(/\s+/));
// ['hello', 'world', 'test']

// With capturing groups — captured parts included!
console.log('hello1world2test'.split(/(\d)/));
// ['hello', '1', 'world', '2', 'test']

// Limit results
console.log('a,b,c,d'.split(/,/, 2));
// ['a', 'b']
```

---

## 6. Practical RegExp Examples

### Email Validation

```javascript
// Simple pattern
const simpleEmail = /\w+@\w+\.\w+/i;
console.log(simpleEmail.test('user@example.com')); // true

// Better pattern
const betterEmail = /^[a-z0-9._-]+@[a-z0-9.-]+\.[a-z]{2,}$/i;
console.log(betterEmail.test('user.name@example.co.uk')); // true
console.log(betterEmail.test('invalid.email@')); // false

// Extract parts
const emailRegex = /(?<user>[a-z0-9._-]+)@(?<domain>[a-z0-9.-]+)\.(?<tld>[a-z]{2,})/i;
const match = 'alice@example.com'.match(emailRegex);
console.log(match.groups); // { user: 'alice', domain: 'example', tld: 'com' }
```

### URL Validation

```javascript
const urlRegex = /^(https?|ftp):\/\/(www\.)?[-a-z0-9@:%._\+~#=]{1,256}\.[a-z0-9()]{1,6}\b([-a-z0-9()@:%_\+.~#?&\/\/=]*)$/i;
console.log(urlRegex.test('https://www.example.com')); // true
console.log(urlRegex.test('http://example.com/path')); // true
console.log(urlRegex.test('not a url')); // false
```

### Phone Number

```javascript
// Format: (555) 123-4567 or 555-123-4567 or 5551234567
const phoneRegex = /^(\(\d{3}\)|\d{3})[-\s]?\d{3}[-\s]?\d{4}$/;
console.log(phoneRegex.test('(555) 123-4567')); // true
console.log(phoneRegex.test('555-123-4567')); // true
console.log(phoneRegex.test('5551234567')); // true
```

### Password Strength

```javascript
// At least 8 chars, 1 uppercase, 1 lowercase, 1 digit, 1 special char
const strongPassword = /^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[@$!%*?&])[A-Za-z\d@$!%*?&]{8,}$/;
console.log(strongPassword.test('Weak')); // false
console.log(strongPassword.test('Strong@123')); // true
```

### Extract Numbers

```javascript
const text = 'The cost is $10.50 and quantity is 5 units';
const numbers = text.match(/\d+(\.\d{2})?/g);
console.log(numbers); // ['10.50', '5']
```

### Remove HTML Tags

```javascript
const html = '<p>Hello <b>world</b></p>';
const plain = html.replace(/<[^>]+>/g, '');
console.log(plain); // 'Hello world'
```

### Capitalize Words

```javascript
const text = 'hello world javascript';
const capitalized = text.replace(/\b\w/g, (match) => match.toUpperCase());
console.log(capitalized); // 'Hello World Javascript'
```

---

## Summary: RegExp Methods & Properties

| Method | Purpose |
|--------|---------|
| `test()` | Boolean test if matches |
| `exec()` | Detailed match info (with groups, index) |
| `.match()` | Find matches (string method) |
| `.matchAll()` | Iterator of all matches |
| `.search()` | Find index of first match |
| `.replace()` | Replace first/all (string method) |
| `.replaceAll()` | Replace all (string method) |
| `.split()` | Split by pattern (string method) |

| Property | Purpose |
|----------|---------|
| `global` | Has `g` flag |
| `ignoreCase` | Has `i` flag |
| `multiline` | Has `m` flag |
| `dotAll` | Has `s` flag |
| `unicode` | Has `u` flag |
| `sticky` | Has `y` flag |
| `flags` | String of all flags |
| `source` | Pattern string |
| `lastIndex` | Current index (for `g`/`y`) |

---

## Best Practices

✅ **Use character classes `\d`, `\w`, `\s`** — More readable than `[0-9]`, `[a-zA-Z0-9_]`

✅ **Use named groups `(?<name>)`** — More maintainable than numbered groups

✅ **Use non-capturing groups `(?:)`** — When you don't need capture

✅ **Make patterns explicit with anchors** — Use `^` and `$` for full match

✅ **Use raw strings where possible** — Single backslash in `/pattern/`, double in `"pattern"`

✅ **Test special characters carefully** — Many need escaping

✅ **Use `.split()` with limit** — Avoid huge arrays

✅ **Cache regex objects** — Don't recreate in loops

```javascript
// ❌ Bad: recreates regex each iteration
for (let i = 0; i < 1000; i++) {
  text.match(/pattern/g);
}

// ✅ Good: reuse regex
const regex = /pattern/g;
for (let i = 0; i < 1000; i++) {
  text.match(regex);
}
```

---

## Common Gotchas

❌ **Global flag affects subsequent calls**
```javascript
const regex = /hello/g;
console.log(regex.test('hello')); // true, lastIndex becomes 5
console.log(regex.test('hello')); // false! lastIndex at 5, not found
// Reset: regex.lastIndex = 0
```

❌ **Dot doesn't match newlines without `s` flag**
```javascript
const regex1 = /a.b/;
console.log('a\nb'.match(regex1)); // null
const regex2 = /a.b/s;
console.log('a\nb'.match(regex2)); // ['a\nb'] — correct
```

❌ **Escaped characters in constructor need double backslash**
```javascript
const lit = /\d/;        // Single backslash
const con = new RegExp('\\d'); // Double backslash
```

❌ **Match doesn't capture groups without exec/matchAll**
```javascript
const str = 'test 123';
const match = str.match(/(\d+)/);
console.log(match[1]); // '123' — has groups

// With global
const matchAll = str.match(/(\d+)/g);
console.log(matchAll[0]); // '123'
console.log(matchAll[0][1]); // undefined — no group info
// Use matchAll() instead
```

❌ **`$` doesn't exclude trailing newline**
```javascript
const regex = /test$/;
console.log(regex.test('test\n')); // true in some contexts
// Use explicit: /test$(?!\n)/
```

❌ **Backreference with wrong group number**
```javascript
const regex = /(\w+)\s+\2/; // Wrong: should be \1
const regex2 = /(\w+)\s+\1/; // Correct
```

❌ **Forgetting `g` flag with `match()` for multiple results**
```javascript
const text = 'a b c';
console.log(text.match(/\w/)); // ['a'] — first only!
console.log(text.match(/\w/g)); // ['a', 'b', 'c'] — all
```
