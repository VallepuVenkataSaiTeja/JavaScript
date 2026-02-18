# Arrays in JavaScript

## What is an Array?

An **array** is a fundamental data structure in JavaScript used to store multiple values in a single variable. Arrays are **objects** where indices are string property keys (`"0"`, `"1"`, `"2"`, etc.), even though they appear as numbers. Arrays can hold any data type and have a dynamic `.length` property.

```javascript
const arr = [10, 'hello', true, null, { name: 'John' }];
console.log(typeof arr);        // "object"
console.log(Array.isArray(arr)); // true
```

---

## 1. Creating Arrays

### Literal Syntax (Most Common)
```javascript
const emptyArray = [];
const numbers = [1, 2, 3, 4, 5];
const mixed = [1, 'two', true, null, undefined, { id: 1 }];
```

### `new Array(length)`
Creates an array with specified length (but empty slots/holes):
```javascript
const arr1 = new Array(5);
console.log(arr1.length);        // 5
console.log(arr1[0]);            // undefined
console.log(arr1);               // [ <5 empty items> ]
```

### `new Array(element1, element2, ...)`
```javascript
const arr2 = new Array(10, 20, 30);
console.log(arr2);               // [10, 20, 30]
console.log(arr2.length);        // 3
```

### `Array.from(iterable, mapFn?)`
Creates array from an iterable with optional mapping function:
```javascript
// From string
const arr3 = Array.from('hello');
console.log(arr3);               // ['h', 'e', 'l', 'l', 'o']

// From array-like object with mapping
const arr4 = Array.from([1, 2, 3], x => x * 2);
console.log(arr4);               // [2, 4, 6]

// From Set
const arr5 = Array.from(new Set([1, 2, 2, 3]));
console.log(arr5);               // [1, 2, 3]

// From NodeList (array-like)
const divs = document.querySelectorAll('div');
const divArray = Array.from(divs);
```

### `Array.of(...elements)`
Creates array from arguments (safer than `new Array()`):
```javascript
const arr6 = Array.of(5);
console.log(arr6);               // [5] — not [<5 empty items>]
console.log(arr6.length);        // 1

const arr7 = Array.of(10, 20, 30);
console.log(arr7);               // [10, 20, 30]
```

---

## 2. The `.length` Property

The `.length` property is **writable** and represents the highest index + 1:

```javascript
const arr = [1, 2, 3, 4, 5];
console.log(arr.length);         // 5

// Truncate array by reducing length
arr.length = 2;
console.log(arr);                // [1, 2]
console.log(arr.length);         // 2

// Extend array with undefined
arr.length = 5;
console.log(arr);                // [1, 2, <3 empty items>]
```

### Sparse Arrays (Holes)
Arrays can have "holes" — missing elements between indices:
```javascript
const sparse = [1, , 3, , 5];    // holes at indices 1 and 3
console.log(sparse.length);      // 5
console.log(sparse[1]);          // undefined
console.log(1 in sparse);        // false — hole exists
console.log(2 in sparse);        // true — value exists

// forEach skips holes
sparse.forEach((val, idx) => console.log(idx, val));
// Output: 0 1, 2 3, 4 5

// map also skips holes
const mapped = sparse.map(x => x * 2);
console.log(mapped);             // [2, <1 empty item>, 6, <1 empty item>, 10]
```

---

## 3. Indexing

Access elements using bracket notation:

```javascript
const arr = ['a', 'b', 'c', 'd'];

// First element
console.log(arr[0]);             // 'a'

// Last element
console.log(arr[arr.length - 1]); // 'd'

// Out-of-bounds index returns undefined
console.log(arr[10]);            // undefined
console.log(arr[-1]);            // undefined
```

---

## 4. Mutating Methods (Change Original Array)

### `push(element1, element2, ...)`
Adds elements to **end**, returns new length:
```javascript
const arr = [1, 2, 3];
const newLength = arr.push(4, 5);
console.log(arr);                // [1, 2, 3, 4, 5]
console.log(newLength);          // 5
```

### `pop()`
Removes last element, returns it (or `undefined` if empty):
```javascript
const arr = [1, 2, 3];
const last = arr.pop();
console.log(last);               // 3
console.log(arr);                // [1, 2]
```

### `shift()`
Removes first element, returns it:
```javascript
const arr = [1, 2, 3];
const first = arr.shift();
console.log(first);              // 1
console.log(arr);                // [2, 3]
```

### `unshift(element1, element2, ...)`
Adds elements to **beginning**, returns new length:
```javascript
const arr = [2, 3];
const newLength = arr.unshift(0, 1);
console.log(arr);                // [0, 1, 2, 3]
console.log(newLength);          // 4
```

### `splice(start, deleteCount?, item1?, item2?, ...)`
Removes/inserts elements at any position, returns deleted elements:
```javascript
const arr = ['a', 'b', 'c', 'd', 'e'];

// Remove 2 elements starting at index 1
const removed = arr.splice(1, 2);
console.log(removed);            // ['b', 'c']
console.log(arr);                // ['a', 'd', 'e']

// Insert without removing
arr.splice(1, 0, 'x', 'y');
console.log(arr);                // ['a', 'x', 'y', 'd', 'e']

// Replace
arr.splice(2, 1, 'z');
console.log(arr);                // ['a', 'x', 'z', 'd', 'e']
```

### `reverse()`
Reverses array in place:
```javascript
const arr = [1, 2, 3, 4, 5];
arr.reverse();
console.log(arr);                // [5, 4, 3, 2, 1]
```

### `sort(compareFn?)`
Sorts array in place. **Default**: sorts as strings (converts to string):
```javascript
const arr1 = [30, 10, 5, 100, 2];
arr1.sort();
console.log(arr1);               // [10, 100, 2, 30, 5] — lexicographic order!

// Sort numbers correctly
const arr2 = [30, 10, 5, 100, 2];
arr2.sort((a, b) => a - b);      // ascending
console.log(arr2);               // [2, 5, 10, 30, 100]

// Descending order
arr2.sort((a, b) => b - a);
console.log(arr2);               // [100, 30, 10, 5, 2]

// Sort strings
const words = ['banana', 'apple', 'cherry'];
words.sort();
console.log(words);              // ['apple', 'banana', 'cherry']

// Sort objects by property
const people = [
  { name: 'Alice', age: 25 },
  { name: 'Bob', age: 20 },
  { name: 'Charlie', age: 30 }
];
people.sort((a, b) => a.age - b.age);
console.log(people);
// [{ name: 'Bob', age: 20 }, { name: 'Alice', age: 25 }, { name: 'Charlie', age: 30 }]

// Note: sort() is stable (maintains relative order of equal elements)
const data = [
  { x: 1, order: 'a' },
  { x: 1, order: 'b' },
  { x: 2, order: 'c' }
];
data.sort((a, b) => a.x - b.x);
console.log(data);
// Order of 'a' and 'b' is preserved: [{ x: 1, order: 'a' }, { x: 1, order: 'b' }, ...]
```

### `fill(value, start?, end?)`
Fills array with a static value:
```javascript
const arr1 = [1, 2, 3, 4, 5];
arr1.fill(0);
console.log(arr1);               // [0, 0, 0, 0, 0]

const arr2 = [1, 2, 3, 4, 5];
arr2.fill(99, 1, 4);             // from index 1 to 4 (exclusive)
console.log(arr2);               // [1, 99, 99, 99, 5]

const arr3 = new Array(5).fill(0);
console.log(arr3);               // [0, 0, 0, 0, 0]
```

### `copyWithin(target, start?, end?)`
Copies part of array to another location within the same array:
```javascript
const arr = [1, 2, 3, 4, 5];
arr.copyWithin(0, 3, 5);         // copy indices 3-5 (exclusive) to index 0
console.log(arr);                // [4, 5, 3, 4, 5]

const arr2 = [1, 2, 3, 4, 5];
arr2.copyWithin(2, 0, 2);        // copy indices 0-2 to index 2
console.log(arr2);               // [1, 2, 1, 2, 5]
```

---

## 5. Non-Mutating Methods (Return New Array/Value)

### `slice(start?, end?)`
Returns shallow copy of portion (doesn't modify original):
```javascript
const arr = ['a', 'b', 'c', 'd', 'e'];

// Copy entire array
const copy = arr.slice();
console.log(copy);               // ['a', 'b', 'c', 'd', 'e']
console.log(copy === arr);       // false — different object

// Get portion
console.log(arr.slice(1, 4));    // ['b', 'c', 'd'] (4 is exclusive)
console.log(arr.slice(2));       // ['c', 'd', 'e'] (to end)
console.log(arr.slice(-2));      // ['d', 'e'] (last 2 elements)

console.log(arr);                // unchanged
```

### `concat(...items)`
Combines arrays, returns new array:
```javascript
const arr1 = [1, 2];
const arr2 = [3, 4];
const result = arr1.concat(arr2, [5, 6], 7);
console.log(result);             // [1, 2, 3, 4, 5, 6, 7]
console.log(arr1);               // unchanged

// Shallow copy with concat
const copy = [1, 2, 3].concat();
console.log(copy);               // [1, 2, 3]
```

### `join(separator?)`
Joins elements into string:
```javascript
const arr = ['apple', 'banana', 'cherry'];

console.log(arr.join());         // 'apple,banana,cherry' (default comma)
console.log(arr.join(' - '));    // 'apple - banana - cherry'
console.log(arr.join(''));       // 'applebananacherry'

const nums = [1, 2, 3];
console.log(nums.join(' > '));   // '1 > 2 > 3'
```

### `indexOf(searchElement, fromIndex?)`
Returns index of first occurrence (or -1):
```javascript
const arr = ['a', 'b', 'c', 'b', 'd'];

console.log(arr.indexOf('b'));   // 1
console.log(arr.indexOf('b', 2)); // 3 (start search from index 2)
console.log(arr.indexOf('x'));   // -1 (not found)

// With numbers
const nums = [10, 20, 30, 20];
console.log(nums.indexOf(20));   // 1

// Uses strict equality (===)
console.log([1, '1'].indexOf(1)); // 0
console.log([1, '1'].indexOf('1')); // 1
```

### `lastIndexOf(searchElement, fromIndex?)`
Returns index of last occurrence:
```javascript
const arr = ['a', 'b', 'c', 'b', 'd'];

console.log(arr.lastIndexOf('b')); // 3 (last occurrence)
console.log(arr.lastIndexOf('b', 2)); // 1 (search backwards from index 2)
console.log(arr.lastIndexOf('x')); // -1
```

### `includes(searchElement, fromIndex?)`
Returns boolean if element exists:
```javascript
const arr = [1, 2, 3, NaN];

console.log(arr.includes(2));    // true
console.log(arr.includes(5));    // false
console.log(arr.includes(3, 3)); // false (search from index 3)
console.log(arr.includes(NaN));  // true (includes handles NaN correctly!)

// Difference from indexOf with NaN
console.log([NaN].indexOf(NaN)); // -1
console.log([NaN].includes(NaN)); // true
```

---

## 6. Iteration Methods

These methods loop through array elements. Many accept a callback function.

### `forEach(callback(element, index, array))`
Executes function for each element (no return value):
```javascript
const arr = [10, 20, 30];

arr.forEach((element, index, array) => {
  console.log(`Index ${index}: ${element}`);
});
// Output:
// Index 0: 10
// Index 1: 20
// Index 2: 30

// Practical example
const students = ['Alice', 'Bob', 'Charlie'];
students.forEach((student, idx) => {
  console.log(`${idx + 1}. ${student}`);
});
// Output:
// 1. Alice
// 2. Bob
// 3. Charlie
```

### `map(callback(element, index, array))`
Transforms each element, returns **new array**:
```javascript
const numbers = [1, 2, 3, 4];

const squared = numbers.map(x => x * x);
console.log(squared);            // [1, 4, 9, 16]
console.log(numbers);            // unchanged

// Map objects
const users = [
  { id: 1, name: 'Alice', age: 25 },
  { id: 2, name: 'Bob', age: 30 }
];

const names = users.map(user => user.name);
console.log(names);              // ['Alice', 'Bob']

const ages = users.map(user => ({ id: user.id, age: user.age }));
console.log(ages);
// [{ id: 1, age: 25 }, { id: 2, age: 30 }]
```

### `filter(callback(element, index, array))`
Selects elements that pass test, returns **new array**:
```javascript
const numbers = [1, 2, 3, 4, 5, 6];

const evens = numbers.filter(x => x % 2 === 0);
console.log(evens);              // [2, 4, 6]

const greaterThan3 = numbers.filter(x => x > 3);
console.log(greaterThan3);       // [4, 5, 6]

// Filter objects
const users = [
  { name: 'Alice', age: 25 },
  { name: 'Bob', age: 17 },
  { name: 'Charlie', age: 30 }
];

const adults = users.filter(user => user.age >= 18);
console.log(adults);
// [{ name: 'Alice', age: 25 }, { name: 'Charlie', age: 30 }]
```

### `find(callback(element, index, array))`
Returns **first element** that passes test (or `undefined`):
```javascript
const numbers = [1, 2, 3, 4, 5];

const firstEven = numbers.find(x => x % 2 === 0);
console.log(firstEven);          // 2

const greaterThan10 = numbers.find(x => x > 10);
console.log(greaterThan10);      // undefined

// Find object
const users = [
  { id: 1, name: 'Alice' },
  { id: 2, name: 'Bob' },
  { id: 3, name: 'Charlie' }
];

const user = users.find(u => u.id === 2);
console.log(user);               // { id: 2, name: 'Bob' }
```

### `findIndex(callback(element, index, array))`
Returns **index** of first element that passes test (or -1):
```javascript
const numbers = [10, 20, 30, 40];

const idx = numbers.findIndex(x => x > 25);
console.log(idx);                // 2 (element 30 at index 2)

const notFound = numbers.findIndex(x => x > 100);
console.log(notFound);           // -1

// Use case: finding position for insertion
const users = [
  { id: 1, name: 'Alice' },
  { id: 3, name: 'Bob' }
];
const insertIdx = users.findIndex(u => u.id > 2);
console.log(insertIdx);          // 1 — insert at position 1
```

### `findLast(callback(element, index, array))`
Returns **last element** that passes test (ES2023):
```javascript
const numbers = [1, 2, 3, 4, 5];

const lastEven = numbers.findLast(x => x % 2 === 0);
console.log(lastEven);           // 4

const notFound = numbers.findLast(x => x > 100);
console.log(notFound);           // undefined
```

### `findLastIndex(callback(element, index, array))`
Returns **index** of last element that passes test (ES2023):
```javascript
const numbers = [1, 2, 3, 4, 5];

const idx = numbers.findLastIndex(x => x % 2 === 0);
console.log(idx);                // 3 (element 4 at index 3)

const notFound = numbers.findLastIndex(x => x > 100);
console.log(notFound);           // -1
```

### `reduce(callback(accumulator, current, index, array), initialValue?)`
Reduces array to single value:
```javascript
const numbers = [1, 2, 3, 4];

// Sum
const sum = numbers.reduce((acc, val) => acc + val, 0);
console.log(sum);                // 10

// Product
const product = numbers.reduce((acc, val) => acc * val, 1);
console.log(product);            // 24

// Without initial value (first element is accumulator)
const sum2 = numbers.reduce((acc, val) => acc + val);
console.log(sum2);               // 10

// Complex example: group by property
const users = [
  { name: 'Alice', dept: 'IT' },
  { name: 'Bob', dept: 'HR' },
  { name: 'Charlie', dept: 'IT' }
];

const grouped = users.reduce((acc, user) => {
  if (!acc[user.dept]) {
    acc[user.dept] = [];
  }
  acc[user.dept].push(user.name);
  return acc;
}, {});

console.log(grouped);
// { IT: ['Alice', 'Charlie'], HR: ['Bob'] }

// Build object from array
const pairs = [['name', 'Alice'], ['age', 25], ['city', 'NYC']];
const obj = pairs.reduce((acc, [key, val]) => {
  acc[key] = val;
  return acc;
}, {});
console.log(obj);                // { name: 'Alice', age: 25, city: 'NYC' }
```

### `reduceRight(callback(accumulator, current, index, array), initialValue?)`
Same as `reduce` but processes from **right to left**:
```javascript
const numbers = [1, 2, 3, 4];

const result = numbers.reduceRight((acc, val) => acc + val, 0);
console.log(result);             // 10 (same result)

// Difference visible with non-commutative operation
const result2 = numbers.reduceRight((acc, val) => `${acc}-${val}`, '');
console.log(result2);            // '-4-3-2-1'

const result3 = numbers.reduce((acc, val) => `${acc}-${val}`, '');
console.log(result3);            // '-1-2-3-4'
```

### `some(callback(element, index, array))`
Returns boolean if **any** element passes test:
```javascript
const numbers = [1, 2, 3, 4, 5];

console.log(numbers.some(x => x > 3)); // true
console.log(numbers.some(x => x > 10)); // false

// Check if any user is admin
const users = [
  { name: 'Alice', role: 'user' },
  { name: 'Bob', role: 'admin' },
  { name: 'Charlie', role: 'user' }
];

const hasAdmin = users.some(u => u.role === 'admin');
console.log(hasAdmin);           // true
```

### `every(callback(element, index, array))`
Returns boolean if **all** elements pass test:
```javascript
const numbers = [2, 4, 6, 8];

console.log(numbers.every(x => x % 2 === 0)); // true (all even)
console.log(numbers.every(x => x > 5));     // false (not all > 5)

// Check if all users are adults
const users = [
  { name: 'Alice', age: 25 },
  { name: 'Bob', age: 17 },
  { name: 'Charlie', age: 30 }
];

const allAdults = users.every(u => u.age >= 18);
console.log(allAdults);          // false (Bob is 17)
```

### `flat(depth?)` and `flatMap(callback(element, index, array))`
Flatten nested arrays:
```javascript
// flat()
const nested = [1, [2, 3], [4, [5, 6]]];

const shallow = nested.flat();
console.log(shallow);            // [1, 2, 3, 4, [5, 6]] (depth 1, default)

const deep = nested.flat(2);
console.log(deep);               // [1, 2, 3, 4, 5, 6] (depth 2)

const veryDeep = nested.flat(Infinity);
console.log(veryDeep);           // [1, 2, 3, 4, 5, 6] (flatten completely)

// flatMap() — combines map and flat
const numbers = [1, 2, 3];
const result = numbers.flatMap(x => [x, x * 2]);
console.log(result);             // [1, 2, 2, 4, 3, 6]

// Equivalent to map then flat
const step1 = numbers.map(x => [x, x * 2]);
console.log(step1);              // [[1, 2], [2, 4], [3, 6]]
const step2 = step1.flat();
console.log(step2);              // [1, 2, 2, 4, 3, 6]
```

---

## 7. Spread Operator & Destructuring

### Spread Operator (`...`) for Arrays
```javascript
// Shallow copy
const original = [1, 2, 3];
const copy = [...original];
console.log(copy);               // [1, 2, 3]
console.log(copy === original);  // false — different object

// Concatenation
const arr1 = [1, 2];
const arr2 = [3, 4];
const combined = [...arr1, ...arr2];
console.log(combined);           // [1, 2, 3, 4]

// Insert elements
const arr = [1, 2, 5];
const newArr = [1, 2, 3, 4, ...arr.slice(2)];
console.log(newArr);             // [1, 2, 3, 4, 5]

// Function arguments
const nums = [1, 2, 3];
Math.max(...nums);               // Equivalent to Math.max(1, 2, 3)

// Note: creates shallow copy (nested arrays/objects still reference original)
const nested = [[1, 2], [3, 4]];
const shallowCopy = [...nested];
shallowCopy[0][0] = 99;
console.log(nested[0][0]);       // 99 — nested arrays shared!
```

### Destructuring
```javascript
// Basic destructuring
const [a, b, c] = [10, 20, 30];
console.log(a, b, c);           // 10 20 30

// Skip elements
const [first, , third] = [10, 20, 30];
console.log(first, third);      // 10 30

// Rest operator
const [head, ...tail] = [1, 2, 3, 4, 5];
console.log(head);              // 1
console.log(tail);              // [2, 3, 4, 5]

// Default values
const [x = 0, y = 0, z = 0] = [1];
console.log(x, y, z);           // 1 0 0

// Swap variables
let p = 5, q = 10;
[p, q] = [q, p];
console.log(p, q);              // 10 5

// Nested destructuring
const arr = [1, [2, 3], 4];
const [num1, [num2, num3], num4] = arr;
console.log(num1, num2, num3, num4); // 1 2 3 4

// In function parameters
function printCoords([x, y]) {
  console.log(`X: ${x}, Y: ${y}`);
}
printCoords([10, 20]);          // X: 10, Y: 20

// With objects in array
const users = [
  { id: 1, name: 'Alice' },
  { id: 2, name: 'Bob' }
];
const [{ name: firstName }, { name: secondName }] = users;
console.log(firstName, secondName); // Alice Bob
```

---

## 8. Multidimensional Arrays (Nested Arrays)

```javascript
// Creating 2D array
const matrix = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9]
];

console.log(matrix[0]);          // [1, 2, 3]
console.log(matrix[1][2]);       // 6
console.log(matrix[2][0]);       // 7

// Accessing and modifying
matrix[0][0] = -1;
console.log(matrix[0]);          // [-1, 2, 3]

// 3D array
const cube = [
  [[1, 2], [3, 4]],
  [[5, 6], [7, 8]]
];
console.log(cube[1][0][1]);      // 6

// Creating multidimensional array
const rows = 3, cols = 3;
const grid = Array(rows).fill(null).map(() => Array(cols).fill(0));
console.log(grid);
// [[0, 0, 0], [0, 0, 0], [0, 0, 0]]

// Flattening
const nested = [1, [2, 3], [4, [5, 6]]];

// Using flat()
const flattened = nested.flat(Infinity);
console.log(flattened);          // [1, 2, 3, 4, 5, 6]

// Using reduce
const flatManual = nested.reduce((acc, val) => {
  return acc.concat(Array.isArray(val) ? flatManual(val) : val);
}, []);
console.log(flatManual);         // [1, 2, 3, 4, 5, 6]

// Using flatMap
const doubled = nested.flatMap(x => Array.isArray(x) ? x : [x]);
console.log(doubled);            // [1, 2, 3, 4, 5, 6]
```

---

## 9. Checking if Something is an Array

### `Array.isArray()`
The **correct** way to check if value is array:
```javascript
console.log(Array.isArray([1, 2, 3])); // true
console.log(Array.isArray('hello'));  // false
console.log(Array.isArray({ 0: 'a', length: 1 })); // false
```

### `typeof` is NOT reliable
```javascript
const arr = [1, 2, 3];
console.log(typeof arr);         // "object" — NOT useful for arrays!
console.log(typeof {});          // "object" — arrays and objects both return "object"

// Better to use Array.isArray()
if (Array.isArray(arr)) {
  console.log('It\'s an array!');
}
```

---

## 10. Array-like Objects

Objects that have `.length` property and numeric indices but aren't arrays.

### Common Array-like Objects
```javascript
// arguments object in function
function showArgs() {
  console.log(arguments);        // Array-like but not Array
  console.log(Array.isArray(arguments)); // false
  console.log(arguments.length); // number of arguments
  console.log(arguments[0]);     // first argument
}
showArgs(1, 2, 3);

// NodeList (DOM)
const divs = document.querySelectorAll('div');
console.log(Array.isArray(divs)); // false — it's a NodeList

// String acts array-like
const str = 'hello';
console.log(str.length);         // 5
console.log(str[0]);             // 'h'
```

### Converting Array-like to Array

#### Using `Array.from()`
```javascript
function demo() {
  const argsArray = Array.from(arguments);
  console.log(Array.isArray(argsArray)); // true
}
demo(1, 2, 3);

// With mapping function
const numbers = Array.from('hello', (char, idx) => {
  return `${idx}: ${char}`;
});
console.log(numbers);
// ['0: h', '1: e', '2: l', '3: l', '4: o']
```

#### Using Spread Operator
```javascript
const divs = document.querySelectorAll('div');
const divArray = [...divs];      // true array
console.log(Array.isArray(divArray)); // true

// But doesn't work on all array-like (needs Symbol.iterator)
function demo() {
  try {
    const argsArray = [...arguments]; // Works in non-strict mode
  } catch(e) {
    // Might fail depending on environment
  }
}
```

#### Using `Array.prototype.slice.call()`
```javascript
function demo() {
  const argsArray = Array.prototype.slice.call(arguments);
  console.log(Array.isArray(argsArray)); // true
}
demo(1, 2, 3);

const divs = document.querySelectorAll('div');
const divArray = Array.prototype.slice.call(divs);
```

---

## Summary: Methods Quick Reference

| Category | Methods |
|----------|---------|
| **Creating** | `[]`, `new Array()`, `Array.from()`, `Array.of()` |
| **Mutating** | `push`, `pop`, `shift`, `unshift`, `splice`, `sort`, `reverse`, `fill`, `copyWithin` |
| **Non-mutating** | `slice`, `concat`, `join`, `indexOf`, `lastIndexOf`, `includes` |
| **Iteration** | `forEach`, `map`, `filter`, `reduce`, `find`, `findIndex`, `some`, `every`, `flat`, `flatMap` |
| **ES2023** | `findLast`, `findLastIndex` |
| **Checking** | `Array.isArray()` |

---

## Best Practices

✅ **Use `Array.isArray()` to check for arrays**
✅ **Prefer iteration methods (`map`, `filter`, etc.) over loops when possible**
✅ **Use spread operator `[...]` for shallow copies**
✅ **Remember `sort()` treats values as strings by default**
✅ **Use `Array.from()` or spread to convert array-like objects**
✅ **Use `includes()` with `includes()` for existence checks (handles NaN)**
✅ **Remember mutating methods change the original array**
✅ **Use `reduce()` for complex transformations**

---

## Common Gotchas

❌ **`new Array(5)` creates holes, not `[undefined, undefined, undefined, undefined, undefined]`**
```javascript
new Array(5).map(x => 0); // Still has holes! Returns [<5 empty items>]
Array(5).fill(0).map(x => 0); // Works correctly
```

❌ **`sort()` converts to strings by default**
```javascript
[3, 1, 10, 2].sort(); // [1, 10, 2, 3] NOT [1, 2, 3, 10]
```

❌ **Spread creates shallow copy, not deep copy**
```javascript
const arr = [[1, 2]];
const copy = [...arr];
copy[0][0] = 99;
console.log(arr[0][0]); // 99 — nested array still shared
```

❌ **Arrow functions in `map/filter/reduce` need braces for multiple statements**
```javascript
arr.map(x => {
  console.log(x);       // Need braces for statement
  return x * 2;
});
```
