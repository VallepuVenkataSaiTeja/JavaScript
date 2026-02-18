# 2.8 Map and Set

## What are Map and Set?

**Map** and **Set** are built-in collections that provide alternatives to objects and arrays:

- **Map**: Key-value pairs where keys can be **any type** (not just strings)
- **Set**: Collection of **unique values**

Both maintain **insertion order** and have useful built-in methods.

---

## 1. Map

### Creating Maps

#### Basic Creation

```javascript
// Empty map
const map1 = new Map();

// From array of [key, value] pairs
const map2 = new Map([
  ['name', 'Alice'],
  ['age', 30],
  ['email', 'alice@example.com']
]);

console.log(map2.get('name')); // 'Alice'
console.log(map2.get('age'));  // 30
```

#### Any Key Type

Map keys can be any data type, unlike plain objects:

```javascript
const map = new Map();

// String keys
map.set('greeting', 'hello');

// Number keys
map.set(1, 'one');
map.set(2, 'two');

// Object keys
const keyObj = { id: 1 };
map.set(keyObj, 'object key');

// Function keys
const keyFunc = () => {};
map.set(keyFunc, 'function key');

// Boolean keys
map.set(true, 'boolean key');

// null and undefined
map.set(null, 'null key');
map.set(undefined, 'undefined key');

console.log(map.get('greeting'));    // 'hello'
console.log(map.get(1));             // 'one'
console.log(map.get(keyObj));        // 'object key'
console.log(map.get(keyFunc));       // 'function key'
console.log(map.get(true));          // 'boolean key'
console.log(map.get(null));          // 'null key'
```

### Map Methods

#### `set(key, value)` — Add/Update

```javascript
const map = new Map();

// Add entries
map.set('x', 10);
map.set('y', 20);

// Update existing (overwrites)
map.set('x', 15);
console.log(map.get('x')); // 15

// Returns the map (chainable)
map.set('a', 1).set('b', 2).set('c', 3);
console.log(map.size); // 5
```

#### `get(key)` — Retrieve Value

```javascript
const map = new Map([
  ['name', 'Alice'],
  ['age', 30]
]);

console.log(map.get('name')); // 'Alice'
console.log(map.get('age'));  // 30
console.log(map.get('email')); // undefined — not found

// Default value pattern
const email = map.get('email') || 'no-email@example.com';
console.log(email); // 'no-email@example.com'
```

#### `has(key)` — Check Existence

```javascript
const map = new Map([
  ['name', 'Alice'],
  ['age', 30]
]);

console.log(map.has('name'));  // true
console.log(map.has('age'));   // true
console.log(map.has('email'));  // false

// Useful for conditionals
if (map.has('age')) {
  console.log(`Age is ${map.get('age')}`);
}
```

#### `delete(key)` — Remove Entry

```javascript
const map = new Map([
  ['a', 1],
  ['b', 2],
  ['c', 3]
]);

console.log(map.size); // 3

map.delete('b');
console.log(map.size); // 2
console.log(map.has('b')); // false

// Returns boolean
const deleted = map.delete('x');
console.log(deleted); // false — key didn't exist
```

#### `clear()` — Remove All Entries

```javascript
const map = new Map([
  ['a', 1],
  ['b', 2]
]);

console.log(map.size); // 2

map.clear();
console.log(map.size); // 0
console.log(map.get('a')); // undefined
```

#### `size` — Get Entry Count

```javascript
const map = new Map();

console.log(map.size); // 0

map.set('a', 1);
console.log(map.size); // 1

map.set('b', 2);
console.log(map.size); // 2

map.delete('a');
console.log(map.size); // 1

// Unlike Object.keys().length, size is O(1)
```

### Iterating Over Maps

#### `keys()` — Get All Keys

```javascript
const map = new Map([
  ['name', 'Alice'],
  ['age', 30],
  ['city', 'NYC']
]);

// Returns iterator
const keys = map.keys();
console.log(keys); // MapIterator { 'name', 'age', 'city' }

// Convert to array
const keyArray = [...map.keys()];
console.log(keyArray); // ['name', 'age', 'city']

// For loop
for (const key of map.keys()) {
  console.log(key);
}
```

#### `values()` — Get All Values

```javascript
const map = new Map([
  ['name', 'Alice'],
  ['age', 30],
  ['city', 'NYC']
]);

const values = [...map.values()];
console.log(values); // ['Alice', 30, 'NYC']

for (const value of map.values()) {
  console.log(value);
}
```

#### `entries()` — Get All [Key, Value] Pairs

```javascript
const map = new Map([
  ['name', 'Alice'],
  ['age', 30]
]);

const entries = [...map.entries()];
console.log(entries);
// [['name', 'Alice'], ['age', 30]]

for (const [key, value] of map.entries()) {
  console.log(`${key}: ${value}`);
}
// name: Alice
// age: 30

// Map is iterable by entries by default
for (const [key, value] of map) {
  console.log(`${key}: ${value}`);
}
```

#### `forEach(callback)` — Iterate with Callback

```javascript
const map = new Map([
  ['name', 'Alice'],
  ['age', 30],
  ['city', 'NYC']
]);

// Callback: (value, key, map)
map.forEach((value, key) => {
  console.log(`${key}: ${value}`);
});

// Full signature with all parameters
map.forEach((value, key, mapItself) => {
  console.log(value, key);
});
```

### Practical Map Examples

#### Using Objects as Keys

```javascript
const userMap = new Map();

const user1 = { id: 1, name: 'Alice' };
const user2 = { id: 2, name: 'Bob' };

// Use objects as keys
userMap.set(user1, { score: 95, level: 'advanced' });
userMap.set(user2, { score: 87, level: 'intermediate' });

// Retrieve by same object reference
console.log(userMap.get(user1)); // { score: 95, level: 'advanced' }

// Different object with same content? No match
const otherUser = { id: 1, name: 'Alice' };
console.log(userMap.get(otherUser)); // undefined — different object
```

#### Counting Occurrences

```javascript
function countOccurrences(arr) {
  const counts = new Map();
  
  for (const item of arr) {
    counts.set(item, (counts.get(item) || 0) + 1);
  }
  
  return counts;
}

const counts = countOccurrences(['a', 'b', 'a', 'c', 'b', 'a']);
console.log(counts);
// Map(3) { 'a' => 3, 'b' => 2, 'c' => 1 }

console.log(counts.get('a')); // 3
```

#### Group By Property

```javascript
function groupBy(array, key) {
  const grouped = new Map();
  
  for (const item of array) {
    const groupKey = item[key];
    if (!grouped.has(groupKey)) {
      grouped.set(groupKey, []);
    }
    grouped.get(groupKey).push(item);
  }
  
  return grouped;
}

const users = [
  { name: 'Alice', dept: 'IT' },
  { name: 'Bob', dept: 'HR' },
  { name: 'Charlie', dept: 'IT' },
  { name: 'David', dept: 'Sales' },
  { name: 'Eve', dept: 'HR' }
];

const byDept = groupBy(users, 'dept');
console.log(byDept);
// Map(3) {
//   'IT' => [{name: 'Alice', dept: 'IT'}, {name: 'Charlie', dept: 'IT'}],
//   'HR' => [{name: 'Bob', dept: 'HR'}, {name: 'Eve', dept: 'HR'}],
//   'Sales' => [{name: 'David', dept: 'Sales'}]
// }

console.log(byDept.get('IT')); // Alice and Charlie
```

---

## 2. Set

### Creating Sets

#### Basic Creation

```javascript
// Empty set
const set1 = new Set();

// From array
const set2 = new Set([1, 2, 3, 4]);
console.log(set2); // Set(4) { 1, 2, 3, 4 }

// Duplicates are removed
const set3 = new Set([1, 2, 2, 3, 3, 3]);
console.log(set3); // Set(3) { 1, 2, 3 }
```

#### Remove Duplicates from Array

```javascript
// Remove duplicates
const arr = [1, 2, 2, 3, 3, 3, 4];
const unique = [...new Set(arr)];
console.log(unique); // [1, 2, 3, 4]

// String characters
const str = 'mississippi';
const uniqueChars = [...new Set(str)];
console.log(uniqueChars); // ['m', 'i', 's', 'p']
```

### Set Methods

#### `add(value)` — Add Value

```javascript
const set = new Set();

set.add(1);
set.add('hello');
set.add(true);
set.add({ id: 1 });

console.log(set.size); // 4

// Duplicate ignored
set.add(1);
console.log(set.size); // Still 4

// Chainable
set.add('a').add('b').add('c');
console.log(set.size); // 7
```

#### `has(value)` — Check Existence

```javascript
const set = new Set([1, 2, 3]);

console.log(set.has(1)); // true
console.log(set.has(4)); // false

// Objects checked by reference
const obj = { id: 1 };
set.add(obj);
console.log(set.has(obj)); // true

const other = { id: 1 };
console.log(set.has(other)); // false — different object
```

#### `delete(value)` — Remove Value

```javascript
const set = new Set([1, 2, 3, 4]);

console.log(set.size); // 4

set.delete(3);
console.log(set.size); // 3
console.log(set.has(3)); // false

// Returns boolean
const deleted = set.delete(10);
console.log(deleted); // false — wasn't in set
```

#### `clear()` — Remove All Values

```javascript
const set = new Set([1, 2, 3]);

console.log(set.size); // 3

set.clear();
console.log(set.size); // 0
```

#### `size` — Get Value Count

```javascript
const set = new Set();

console.log(set.size); // 0

set.add('a');
console.log(set.size); // 1

set.add('b');
set.add('c');
console.log(set.size); // 3

set.delete('b');
console.log(set.size); // 2
```

### Iterating Over Sets

#### `keys()` and `values()`

In Set, both return the same thing (values):

```javascript
const set = new Set(['a', 'b', 'c']);

// keys() and values() are identical for Set
const keys = [...set.keys()];
const values = [...set.values()];

console.log(keys);   // ['a', 'b', 'c']
console.log(values); // ['a', 'b', 'c']
```

#### `entries()` — Get [Value, Value] Pairs

Sets have no keys, so entries returns [value, value]:

```javascript
const set = new Set(['a', 'b']);

const entries = [...set.entries()];
console.log(entries);
// [['a', 'a'], ['b', 'b']]
```

#### `forEach(callback)` — Iterate with Callback

```javascript
const set = new Set(['x', 'y', 'z']);

// Callback: (value, value, set) — note value appears twice
set.forEach((value) => {
  console.log(value);
});
// x, y, z

// All parameters
set.forEach((value1, value2, setItself) => {
  console.log(value1, value2); // Both are same
});
```

#### Direct Iteration (for...of)

```javascript
const set = new Set([10, 20, 30]);

for (const value of set) {
  console.log(value);
}
// 10, 20, 30

// Destructuring
for (const [val] of set) {
  console.log(val); // Just the value
}
```

### ES2024 Set Methods

JavaScript 2024 adds set algebra methods:

#### `union(...sets)` — Combine Sets

```javascript
const set1 = new Set([1, 2, 3]);
const set2 = new Set([3, 4, 5]);

const combined = set1.union(set2);
console.log(combined); // Set(5) { 1, 2, 3, 4, 5 }

// Multiple unions
const set3 = new Set([5, 6]);
const all = set1.union(set2).union(set3);
console.log(all); // Set(6) { 1, 2, 3, 4, 5, 6 }
```

#### `intersection(...sets)` — Common Elements

```javascript
const set1 = new Set([1, 2, 3, 4]);
const set2 = new Set([3, 4, 5, 6]);

const common = set1.intersection(set2);
console.log(common); // Set(2) { 3, 4 }

// No common elements
const set3 = new Set([7, 8]);
const noneCommon = set1.intersection(set3);
console.log(noneCommon); // Set(0) {}
```

#### `difference(...sets)` — In First But Not Others

```javascript
const set1 = new Set([1, 2, 3, 4]);
const set2 = new Set([3, 4, 5, 6]);

const diff = set1.difference(set2);
console.log(diff); // Set(2) { 1, 2 } — in set1 but not set2

// Remove multiple sets
const set3 = new Set([2]);
const result = set1.difference(set2, set3);
console.log(result); // Set(1) { 1 }
```

#### `symmetricDifference(...sets)` — In Either But Not Both

```javascript
const set1 = new Set([1, 2, 3]);
const set2 = new Set([3, 4, 5]);

const symDiff = set1.symmetricDifference(set2);
console.log(symDiff); // Set(4) { 1, 2, 4, 5 }
// Elements in either set but not in both
```

#### `isSubsetOf(other)` — Is Subset?

```javascript
const set1 = new Set([1, 2]);
const set2 = new Set([1, 2, 3, 4]);
const set3 = new Set([1, 2]);

console.log(set1.isSubsetOf(set2)); // true — all of set1 in set2
console.log(set1.isSubsetOf(set3)); // true — equal sets are subsets
console.log(set2.isSubsetOf(set1)); // false — set2 has extra elements
```

#### `isSupersetOf(other)` — Is Superset?

```javascript
const set1 = new Set([1, 2, 3, 4]);
const set2 = new Set([1, 2]);

console.log(set1.isSupersetOf(set2)); // true — set1 contains all of set2
console.log(set2.isSupersetOf(set1)); // false
```

#### Practical Sets Example

```javascript
// Find intersection of user interests
const alice = new Set(['coding', 'gaming', 'reading']);
const bob = new Set(['gaming', 'sports', 'reading']);
const charlie = new Set(['cooking', 'reading', 'gaming']);

const commonInterests = alice
  .intersection(bob)
  .intersection(charlie);

console.log(commonInterests); // Set(1) { 'reading' }
// All three like reading and gaming

const allInterests = alice.union(bob).union(charlie);
console.log(allInterests); 
// Set(7) { 'coding', 'gaming', 'reading', 'sports', 'cooking' }

// Alice's unique interests (not shared with both)
const aliceUnique = alice
  .difference(bob)
  .difference(charlie);
console.log(aliceUnique); // Set(1) { 'coding' }
```

### Practical Set Examples

#### Unique Tags from Array

```javascript
function extractUniqueTags(posts) {
  const tags = new Set();
  
  for (const post of posts) {
    post.tags.forEach(tag => tags.add(tag));
  }
  
  return [...tags].sort();
}

const posts = [
  { title: 'Post 1', tags: ['javascript', 'web'] },
  { title: 'Post 2', tags: ['python', 'data'] },
  { title: 'Post 3', tags: ['javascript', 'node'] }
];

const uniqueTags = extractUniqueTags(posts);
console.log(uniqueTags);
// ['data', 'javascript', 'node', 'python', 'web']
```

#### Find Missing Numbers

```javascript
function findMissing(arr, n) {
  const set = new Set(arr);
  const missing = new Set();
  
  for (let i = 1; i <= n; i++) {
    if (!set.has(i)) {
      missing.add(i);
    }
  }
  
  return [...missing];
}

const arr = [1, 3, 4, 6, 7, 10];
const missing = findMissing(arr, 10);
console.log(missing); // [2, 5, 8, 9]
```

---

## 3. WeakMap

### What is WeakMap?

A **WeakMap** holds weak references to object **keys** only (not primitives). Keys can be garbage collected if no other references exist. WeakMaps are not iterable.

### Creating WeakMaps

```javascript
const weakMap = new WeakMap();

// Keys MUST be objects
const obj1 = { id: 1 };
const obj2 = { id: 2 };

weakMap.set(obj1, 'value1');
weakMap.set(obj2, 'value2');

console.log(weakMap.get(obj1)); // 'value1'

// Can't use primitives as keys
// weakMap.set('string', 'value'); // TypeError
// weakMap.set(42, 'value'); // TypeError
```

### WeakMap Methods

```javascript
const weakMap = new WeakMap();
const key = { id: 1 };

// set(key, value)
weakMap.set(key, 'data');

// get(key)
console.log(weakMap.get(key)); // 'data'

// has(key)
console.log(weakMap.has(key)); // true

// delete(key)
weakMap.delete(key);
console.log(weakMap.has(key)); // false

// NO: size, keys(), values(), entries(), forEach()
// WeakMap is not iterable!
```

### Garbage Collection

WeakMap keys can be garbage collected:

```javascript
let obj = { id: 1 };
const weakMap = new WeakMap();

weakMap.set(obj, 'data');
console.log(weakMap.has(obj)); // true

// obj is removed from memory (in a real GC scenario)
obj = null;
// Eventually, garbage collector might remove obj
// Then: weakMap.get(obj reference) would return undefined

// But we can't check this directly — no way to iterate
```

### Practical WeakMap Uses

#### Private Data on Objects

```javascript
const privateData = new WeakMap();

class User {
  constructor(name) {
    this.name = name;
    privateData.set(this, { password: 'secret', ssn: '123-45-6789' });
  }

  authenticate(pwd) {
    const data = privateData.get(this);
    return data && data.password === pwd;
  }
}

const user = new User('Alice');
console.log(user.name); // 'Alice' (public)
console.log(privateData.get(user)); // { password, ssn } (private)
console.log(user.password); // undefined (not accessible)

// When user is deleted, private data is auto-cleaned
```

#### DOM Element Metadata

```javascript
const elementData = new WeakMap();

function addDataToElement(element, data) {
  elementData.set(element, data);
}

function getElementData(element) {
  return elementData.get(element);
}

const btn = document.getElementById('myBtn');
addDataToElement(btn, { clicks: 0, lastClicked: null });

// When button is removed from DOM, associated data is cleaned up
```

---

## 4. WeakSet

### What is WeakSet?

A **WeakSet** holds weak references to **values** (must be objects). Values can be garbage collected. WeakSets are not iterable.

### Creating WeakSets

```javascript
const weakSet = new WeakSet();

const obj1 = { id: 1 };
const obj2 = { id: 2 };

weakSet.add(obj1);
weakSet.add(obj2);

console.log(weakSet.has(obj1)); // true
console.log(weakSet.has(obj2)); // true

// Can't add primitives
// weakSet.add('string'); // TypeError
// weakSet.add(42); // TypeError
```

### WeakSet Methods

```javascript
const weakSet = new WeakSet();
const obj = { id: 1 };

// add(value)
weakSet.add(obj);

// has(value)
console.log(weakSet.has(obj)); // true

// delete(value)
weakSet.delete(obj);
console.log(weakSet.has(obj)); // false

// NO: size, values(), keys(), entries(), forEach()
// WeakSet is not iterable!
```

### Practical WeakSet Uses

#### Track Objects for Validity

```javascript
const validUsers = new WeakSet();

class User {
  constructor(name, isValid = true) {
    this.name = name;
    if (isValid) {
      validUsers.add(this);
    }
  }

  isValid() {
    return validUsers.has(this);
  }

  deactivate() {
    validUsers.delete(this);
  }
}

const alice = new User('Alice', true);
const eve = new User('Eve', false);

console.log(alice.isValid()); // true
console.log(eve.isValid()); // false

alice.deactivate();
console.log(alice.isValid()); // false
```

#### Track Objects That Need Cleanup

```javascript
const registeredObjects = new WeakSet();

class Resource {
  constructor(name) {
    this.name = name;
    registeredObjects.add(this);
  }
}

// Objects in WeakSet don't prevent GC
const resource1 = new Resource('Resource 1');
const resource2 = new Resource('Resource 2');

console.log(registeredObjects.has(resource1)); // true

// When resource1 is no longer referenced, it can be garbage collected
// and automatically removed from the WeakSet
```

---

## 5. Map vs Object, Set vs Array

### When to Use Map Over Object

```javascript
// Use Object when:
// - Keys are strings or symbols
// - Simple data structures
// - JSON serialization needed

const config = {
  theme: 'dark',
  language: 'en'
};

// Use Map when:
// - Keys aren't strings
// - Need insertion order
// - Need methods like has(), clear()
// - Performance matters (Map faster for large datasets)

const cache = new Map();
cache.set(userId, userData); // userId is a number
cache.set(apiKey, tokenData); // apiKey is an object

// Comparison
const obj = {};
obj[1] = 'value'; // Key becomes string "1"
obj['1'] === obj[1]; // true

const map = new Map();
map.set(1, 'value');
map.set('1', 'other');
map.size; // 2 — different keys!
```

### When to Use Set Over Array

```javascript
// Use Array when:
// - Order and duplicates matter
// - Need array methods (map, filter, slice, etc.)

const numbers = [1, 2, 2, 3, 3, 3];
const doubled = numbers.map(x => x * 2);

// Use Set when:
// - Only unique values
// - Need fast lookup (has is O(1))
// - Order doesn't matter or insertion order sufficient
// - Need set operations (union, intersection, etc.)

const userIds = new Set([1, 2, 3]);
if (userIds.has(userId)) { // O(1) lookup, faster than array indexOf
  // Process user
}

// Performance comparison
const arr = new Array(1000000).fill(0).map((_, i) => i);
const set = new Set(arr);

console.time('Array indexOf');
arr.includes(999999); // O(n)
console.timeEnd('Array indexOf');

console.time('Set has');
set.has(999999); // O(1)
console.timeEnd('Set has');
```

### Conversion Between Types

```javascript
// Object → Map
const obj = { a: 1, b: 2 };
const mapFromObj = new Map(Object.entries(obj));
console.log(mapFromObj); // Map { 'a' => 1, 'b' => 2 }

// Map → Object
const map = new Map([['x', 10], ['y', 20]]);
const objFromMap = Object.fromEntries(map);
console.log(objFromMap); // { x: 10, y: 20 }

// Array → Set
const arr = [1, 2, 2, 3, 3, 3];
const setFromArr = new Set(arr);
console.log(setFromArr); // Set(3) { 1, 2, 3 }

// Set → Array
const set = new Set(['a', 'b', 'c']);
const arrFromSet = [...set]; // or Array.from(set)
console.log(arrFromSet); // ['a', 'b', 'c']
```

---

## 6. Practical Examples

### LRU Cache with Map

```javascript
class LRUCache {
  constructor(maxSize) {
    this.maxSize = maxSize;
    this.cache = new Map();
  }

  get(key) {
    if (!this.cache.has(key)) return null;
    
    // Move to end (most recently used)
    const value = this.cache.get(key);
    this.cache.delete(key);
    this.cache.set(key, value);
    return value;
  }

  set(key, value) {
    // Remove old value if exists
    if (this.cache.has(key)) {
      this.cache.delete(key);
    }
    // Add to end
    this.cache.set(key, value);
    
    // Remove oldest if over size
    if (this.cache.size > this.maxSize) {
      const firstKey = this.cache.keys().next().value;
      this.cache.delete(firstKey);
    }
  }
}

const cache = new LRUCache(3);
cache.set('a', 1);
cache.set('b', 2);
cache.set('c', 3);
cache.get('a'); // a is now most recent
cache.set('d', 4); // b gets removed (least recently used)
```

### Graph with Map of Sets

```javascript
class Graph {
  constructor() {
    this.adjacencyList = new Map();
  }

  addVertex(vertex) {
    if (!this.adjacencyList.has(vertex)) {
      this.adjacencyList.set(vertex, new Set());
    }
  }

  addEdge(vertex1, vertex2) {
    this.addVertex(vertex1);
    this.addVertex(vertex2);
    
    this.adjacencyList.get(vertex1).add(vertex2);
    this.adjacencyList.get(vertex2).add(vertex1); // undirected
  }

  getNeighbors(vertex) {
    return this.adjacencyList.get(vertex) || new Set();
  }
}

const graph = new Graph();
graph.addEdge('A', 'B');
graph.addEdge('A', 'C');
graph.addEdge('B', 'C');

console.log(graph.getNeighbors('A')); // Set { 'B', 'C' }
```

---

## Summary: Comparison Table

| Feature | Object | Map | Set | Array | WeakMap | WeakSet |
|---------|--------|-----|-----|-------|---------|---------|
| **Key/Value** | string/Symbol keys | Any type keys | — | — | Object keys only | — |
| **Value** | Any | Any | Any unique | Any | Any | Objects only |
| **Ordered** | No | ✅ Yes | ✅ Yes | ✅ Yes | ✅ Yes (order) | ✅ Yes (order) |
| **Iterable** | ✅ Yes | ✅ Yes | ✅ Yes | ✅ Yes | ❌ No | ❌ No |
| **size/length** | No `.size` | ✅ `.size` | ✅ `.size` | ✅ `.length` | ❌ No | ❌ No |
| **Weak refs** | ❌ No | ❌ No | ❌ No | ❌ No | ✅ Yes | ✅ Yes |
| **Performance** | O(n) lookups | O(1) lookups | O(1) lookups | O(n) lookups | O(1) | O(1) |

---

## Best Practices

✅ **Use Map for non-string keys** — Objects only support string/Symbol keys

✅ **Use Set to remove duplicates** — More efficient than manual filtering

✅ **Use Map's `.size` property** — Better than `Object.keys().length`

✅ **Chain Map operations** — `map.set(...).set(...)`

✅ **Cache results in WeakMap** — Automatically garbage collected

✅ **Use ES2024 Set methods** — `union()`, `intersection()`, etc. for set algebra

✅ **Convert Map/Set to array when needed** — `[...map]`, `[...set]`

---

## Common Gotchas

❌ **Map keys are compared by identity, not value**
```javascript
const map = new Map();
map.set({ id: 1 }, 'value');
map.get({ id: 1 }); // undefined — different object!
```

❌ **Object keys always coerce to strings**
```javascript
const obj = {};
obj[1] = 'one';
obj['1'] = 'two';
obj[1]; // 'two' — same key!

const map = new Map();
map.set(1, 'one');
map.set('1', 'two');
map.size; // 2 — different keys
```

❌ **Set.prototype.keys() returns iterator, not array**
```javascript
const set = new Set([1, 2, 3]);
const keys = set.keys(); // Iterator, not array
// Convert: [...set.keys()] or [...set]
```

❌ **WeakMap/WeakSet not iterable**
```javascript
const weakMap = new WeakMap();
// Can't do: for (const [k, v] of weakMap)
// Can't do: [...weakMap]
// No .size, .keys(), .values(), .forEach()
```

❌ **Comparing Sets/Maps for equality**
```javascript
new Set([1, 2]) === new Set([1, 2]); // false — different objects
new Map([['a', 1]]) === new Map([['a', 1]]); // false

// Must manually compare
function setsEqual(set1, set2) {
  if (set1.size !== set2.size) return false;
  for (const item of set1) {
    if (!set2.has(item)) return false;
  }
  return true;
}
```

❌ **Map.get() with undefined value**
```javascript
const map = new Map();
map.set('key', undefined);

map.get('key'); // undefined
map.has('key'); // true — key exists!

// To distinguish: always use .has()
```

❌ **Mutating during iteration**
```javascript
const set = new Set([1, 2, 3]);

// Safe in most modern engines, but risky
for (const item of set) {
  set.delete(item); // May skip elements
}

// Better: collect first
const toDelete = [...set];
toDelete.forEach(item => set.delete(item));
```
