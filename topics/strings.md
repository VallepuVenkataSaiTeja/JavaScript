# 🔵 1. What is a String?

A **string** is a sequence of characters used to represent text.

Characters include:

* Letters → `A-Z`
* Numbers → `0-9`
* Symbols → `@ # $`
* Spaces
* Emojis 😊

Example:

```js
let name = "John";
let city = 'Paris';
```

Strings are:

* ✅ Primitive data type
* ✅ Immutable
* ✅ UTF-16 encoded
* ✅ Zero-indexed

---

# 🔵 2. Ways to Create Strings

## 2.1 Using Double Quotes

```js
let str = "Hello";
```

## 2.2 Using Single Quotes

```js
let str = 'Hello';
```

No difference between single and double quotes.

---

## 2.3 Template Literals (Backticks ` `)

Introduced in ES6.

```js
let name = "John";
let message = `Hello ${name}`;
```

### Features of Template Literals

### ✅ 1. Variable Interpolation

```js
let a = 10;
let b = 20;
let result = `Sum is ${a + b}`;
```

### ✅ 2. Multi-line Strings

```js
let text = `Line 1
Line 2
Line 3`;
```

### ✅ 3. Expression Evaluation

```js
let price = 100;
let tax = 0.1;

let total = `Total: ${price + price * tax}`;
```

---

## 2.4 Using String Constructor (Not Recommended)

```js
let str = new String("Hello");
```

This creates a **String object**, not a primitive.

---

# 🔵 3. Primitive vs String Object

```js
let str1 = "Hello";              // Primitive
let str2 = new String("Hello");  // Object
```

Check type:

```js
typeof str1; // "string"
typeof str2; // "object"
```

Comparison:

```js
str1 === str2; // false
```

⚠ Always use primitive strings.

---

# 🔵 4. String Immutability (Very Important)

Strings cannot be changed after creation.

```js
let str = "Hello";
str[0] = "Y";

console.log(str); // "Hello"
```

To modify:

```js
str = "Y" + str.slice(1);
```

Each modification creates a **new string in memory**.

---

# 🔵 5. String Properties

## length

```js
let text = "JavaScript";
console.log(text.length); // 10
```

For emoji:

```js
console.log("😊".length); // 2
```

Because JS uses UTF-16 encoding.

---

# 🔵 6. Accessing Characters

## 6.1 Using Index

```js
let str = "Hello";
console.log(str[0]); // H
```

## 6.2 charAt()

```js
str.charAt(1); // e
```

## 6.3 at() (Modern)

Supports negative index:

```js
str.at(-1); // o
```

## 6.4 charCodeAt()

Returns UTF-16 code:

```js
"H".charCodeAt(0); // 72
```

## 6.5 codePointAt()

Works correctly with emoji:

```js
"😊".codePointAt(0); // 128522
```

---

# 🔵 7. String Concatenation

## Using +

```js
let full = "Hello " + "World";
```

## Using +=

```js
let str = "Hello";
str += " World";
```

## Using Template Literals (Best Practice)

```js
let name = "Sam";
let msg = `Hello ${name}`;
```

---

# 🔵 8. Searching in Strings

## indexOf()

```js
"hello".indexOf("l"); // 2
```

Returns -1 if not found.

## lastIndexOf()

```js
"hello".lastIndexOf("l"); // 3
```

## includes()

```js
"JavaScript".includes("Script"); // true
```

## startsWith()

```js
"JavaScript".startsWith("Java"); // true
```

## endsWith()

```js
"JavaScript".endsWith("Script"); // true
```

---

# 🔵 9. Extracting Substrings

## slice(start, end)

```js
let str = "JavaScript";
str.slice(0, 4); // "Java"
```

Supports negative index:

```js
str.slice(-6); // "Script"
```

---

## substring(start, end)

```js
str.substring(0, 4);
```

Does NOT support negative values.

---

## substr(start, length) (Deprecated)

```js
str.substr(0, 4);
```

Avoid using.

---

# 🔵 10. Replacing Text

## replace()

```js
"Hello World".replace("World", "JS");
```

Replaces only first match.

---

## replaceAll()

```js
"aaa".replaceAll("a", "b"); // "bbb"
```

---

## Using Regular Expressions

```js
"aaa".replace(/a/g, "b");
```

---

# 🔵 11. Splitting Strings

```js
let words = "one two three".split(" ");
```

Split into characters:

```js
"hello".split("");
```

---

# 🔵 12. Trimming Spaces

```js
let str = "   Hello   ";

str.trim();
str.trimStart();
str.trimEnd();
```

---

# 🔵 13. Padding

```js
"5".padStart(3, "0"); // "005"
"5".padEnd(3, "0");   // "500"
```

---

# 🔵 14. Repeat

```js
"Hi".repeat(3); // "HiHiHi"
```

---

# 🔵 15. Case Conversion

```js
let str = "JavaScript";

str.toUpperCase();
str.toLowerCase();
```

---

# 🔵 16. String Comparison

```js
"apple" < "banana"; // true
```

Comparison is based on Unicode values.

---

## localeCompare()

```js
"a".localeCompare("b"); // -1
```

Returns:

* -1 → smaller
* 0 → equal
* 1 → greater

---

# 🔵 17. Escape Characters

Used for special characters:

```js
let str = "He said \"Hello\"";
```

Common escapes:

| Escape | Meaning   |
| ------ | --------- |
| \n     | New line  |
| \t     | Tab       |
| \      | Backslash |

---

# 🔵 18. UTF-16 & Surrogate Pairs

JavaScript strings use UTF-16 encoding.

Most characters = 1 code unit (16 bits).
Emojis = 2 code units (32 bits).

```js
"😊".length; // 2
```

Correct iteration:

```js
for (let char of "😊") {
  console.log(char);
}
```

---

# 🔵 19. Iterating Over Strings

## Using for loop

```js
let str = "Hello";

for (let i = 0; i < str.length; i++) {
  console.log(str[i]);
}
```

## Using for...of

```js
for (let char of str) {
  console.log(char);
}
```

---

# 🔵 20. Template Literals Advanced

## Tagged Templates

```js
function tag(strings, value) {
  return strings[0] + value.toUpperCase();
}

tag`Hello ${"world"}`;
```

---

## String.raw()

```js
String.raw`Hello\nWorld`;
```

Outputs:

```
Hello\nWorld
```

---

# 🔵 21. Regular Expressions with Strings

## match()

```js
"cat bat rat".match(/at/g);
```

## search()

```js
"hello".search(/e/);
```

## matchAll()

```js
let regex = /t(e)(st)/g;

for (let match of "test1test2".matchAll(regex)) {
  console.log(match);
}
```

---

# 🔵 22. Converting to String

```js
String(123);
(123).toString();
true.toString();
```

---

# 🔵 23. Automatic Boxing

When calling methods:

```js
let str = "hello";
str.toUpperCase();
```

JavaScript temporarily converts primitive string to object.

---

# 🔵 24. Performance Considerations

* Strings are immutable → new string created on change
* Avoid repeated `+` in large loops
* Use `join()` for combining arrays

Example:

```js
let arr = ["Hello", "World"];
arr.join(" ");
```

---

# 🔵 25. Edge Cases

```js
"" == false;   // true
"" === false;  // false
```

```js
null + "text"; // "nulltext"
```

---

# 🔵 26. Real-World Algorithms

## Reverse String

```js
let reversed = str.split("").reverse().join("");
```

## Check Palindrome

```js
function isPalindrome(str) {
  let cleaned = str.toLowerCase().replace(/[^a-z]/g, "");
  return cleaned === cleaned.split("").reverse().join("");
}
```

---

# 🔵 27. Important Interview Differences

| Method    | Negative Support | Notes                 |
| --------- | ---------------- | --------------------- |
| slice     | Yes              | Most flexible         |
| substring | No               | Swaps negative values |
| substr    | Deprecated       | Avoid                 |

---

# 🔵 28. Internal Behavior Summary

Strings are:

* Stored as UTF-16
* Immutable
* Indexed
* Primitive
* Temporarily boxed when methods are called

---



