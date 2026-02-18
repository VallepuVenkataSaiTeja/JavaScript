# 2.2 Objects

## What is an Object?

An **object** is a collection of key-value pairs (also called properties). Objects are the fundamental building block of JavaScript and are used to store related data and functionality together. Keys can be **strings** or **Symbols**, and values can be any data type (primitives, functions, other objects, etc.).

```javascript
const person = {
  name: 'Alice',
  age: 30,
  city: 'New York'
};
```

---

## 1. Creating Objects

### Object Literal (Most Common)
```javascript
const empty = {};

const person = {
  name: 'Alice',
  age: 30,
  email: 'alice@example.com'
};
```

### With String Keys
```javascript
const obj = {
  'first name': 'John',    // Keys with spaces need quotes
  'last-name': 'Doe',      // Keys with hyphens need quotes
  'special!key': 'value'   // Keys with special chars need quotes
};

console.log(obj['first name']); // 'John'
```

### With Computed Keys
```javascript
const key1 = 'user';
const key2 = 'age';

const obj = {
  [key1]: 'Alice',
  [key2]: 30,
  [`${key1}_id`]: 123      // Can use expressions
};

console.log(obj);          // { user: 'Alice', age: 30, user_id: 123 }
```

### Property Shorthand
When the key name matches the variable name, you can omit the key:
```javascript
const name = 'Alice';
const age = 30;
const email = 'alice@example.com';

// Without shorthand
const person1 = {
  name: name,
  age: age,
  email: email
};

// With shorthand (much cleaner!)
const person2 = {
  name,
  age,
  email
};

console.log(person2);
// { name: 'Alice', age: 30, email: 'alice@example.com' }
```

### Method Shorthand
```javascript
// Traditional syntax
const obj1 = {
  greet: function() {
    return 'Hello!';
  }
};

// Method shorthand
const obj2 = {
  greet() {
    return 'Hello!';
  }
};

console.log(obj2.greet()); // 'Hello!'
```

### Using `new Object()`
```javascript
const obj = new Object();
obj.name = 'Alice';
obj.age = 30;

console.log(obj);          // { name: 'Alice', age: 30 }
```

---

## 2. Accessing Properties

### Dot Notation
```javascript
const person = { name: 'Alice', age: 30 };

console.log(person.name);  // 'Alice'
console.log(person.age);   // 30
```

### Bracket Notation
```javascript
const person = { name: 'Alice', age: 30 };

console.log(person['name']); // 'Alice'
console.log(person['age']);  // 30
```

### When to Use Bracket Notation
Use bracket notation when:
1. **Key contains special characters or spaces**
   ```javascript
   const obj = { 'first name': 'John', 'user-id': 123 };
   console.log(obj['first name']); // 'John' — can't use dot
   console.log(obj['user-id']);    // 123
   ```

2. **Key is dynamic**
   ```javascript
   const person = { name: 'Alice', email: 'alice@ex.com', phone: '123' };
   const property = 'email';
   
   console.log(person[property]); // 'alice@ex.com' — uses variable
   console.log(person.property);  // undefined — looks for literal "property"
   ```

3. **Key is a number**
   ```javascript
   const obj = { 0: 'first', 1: 'second' };
   console.log(obj[0]);  // 'first'
   console.log(obj['0']); // 'first' — numbers auto-convert to strings
   ```

4. **Programmatic access**
   ```javascript
   const keys = ['firstName', 'lastName', 'email'];
   const user = { firstName: 'John', lastName: 'Doe', email: 'john@ex.com' };
   
   keys.forEach(key => {
     console.log(user[key]); // Dynamically access
   });
   ```

### Accessing Non-existent Properties
```javascript
const person = { name: 'Alice' };

console.log(person.age);       // undefined — property doesn't exist
console.log(person['address']); // undefined
console.log(person.toString);  // [Function: toString] — from prototype
```

---

## 3. Adding & Updating Properties

### Adding New Properties
```javascript
const person = {};

person.name = 'Alice';
person['age'] = 30;
person['email'] = 'alice@example.com';

console.log(person);
// { name: 'Alice', age: 30, email: 'alice@example.com' }
```

### Updating Existing Properties
```javascript
const person = { name: 'Alice', age: 25 };

person.age = 30;        // Update with dot
person['name'] = 'Bob'; // Update with bracket

console.log(person);    // { name: 'Bob', age: 30 }
```

### Adding Properties Dynamically
```javascript
const obj = {};
const key = 'dynamicKey';
const value = 'dynamicValue';

obj[key] = value;

console.log(obj);       // { dynamicKey: 'dynamicValue' }
```

---

## 4. Deleting Properties

### Using `delete` Operator
```javascript
const person = { name: 'Alice', age: 30, email: 'alice@ex.com' };

delete person.age;
console.log(person);    // { name: 'Alice', email: 'alice@ex.com' }

delete person['email'];
console.log(person);    // { name: 'Alice' }
```

### Delete Return Value
```javascript
const obj = { x: 1 };

const result = delete obj.x;
console.log(result);    // true
console.log(obj);       // {}

// Deleting non-existent property returns true
const result2 = delete obj.nonExistent;
console.log(result2);   // true

// Deleting non-configurable properties returns false
const obj2 = {};
Object.defineProperty(obj2, 'fixed', { value: 1, configurable: false });
console.log(delete obj2.fixed); // false
```

---

## 5. Checking If Properties Exist

### The `in` Operator
Checks if property exists **in object or its prototype chain**:
```javascript
const person = { name: 'Alice', age: 30 };

console.log('name' in person);     // true
console.log('age' in person);      // true
console.log('email' in person);    // false
console.log('toString' in person); // true — from prototype!

// Warning: includes prototype chain
const obj = Object.create({ inheritedProp: 'value' });
obj.ownProp = 'value';

console.log('ownProp' in obj);      // true
console.log('inheritedProp' in obj); // true — from prototype
```

### `hasOwnProperty()`
Checks if property exists **only in object, not prototype**:
```javascript
const person = { name: 'Alice', age: 30 };

console.log(person.hasOwnProperty('name')); // true
console.log(person.hasOwnProperty('age'));  // true
console.log(person.hasOwnProperty('email')); // false
console.log(person.hasOwnProperty('toString')); // false — not in object

// Better than 'in' for own properties
const obj = Object.create({ inheritedProp: 'value' });
obj.ownProp = 'value';

console.log(obj.hasOwnProperty('ownProp'));      // true
console.log(obj.hasOwnProperty('inheritedProp')); // false — not own property
```

### `Object.hasOwn()` (ES2022, Preferred)
Modern, safer alternative to `hasOwnProperty()`:
```javascript
const person = { name: 'Alice', age: 30 };

console.log(Object.hasOwn(person, 'name')); // true
console.log(Object.hasOwn(person, 'age'));  // true
console.log(Object.hasOwn(person, 'email')); // false

// Safer because doesn't depend on hasOwnProperty method
const obj = Object.create(null);
obj.key = 'value';

console.log(Object.hasOwn(obj, 'key')); // true — works even without prototype
// console.log(obj.hasOwnProperty('key')); // Error — no hasOwnProperty!
```

### Checking for Truthy Values
```javascript
const user = { name: 'Alice', email: null };

// Not ideal — 0, '', false are falsy
if (user.name) { console.log(user.name); } // Works

// Better for non-existent properties
if (user.age !== undefined) { console.log('age exists'); }

// Use hasOwn to distinguish null from non-existent
console.log(Object.hasOwn(user, 'email')); // true (value is null)
console.log(Object.hasOwn(user, 'age'));   // false (property doesn't exist)
```

---

## 6. Iteration Over Objects

### `for...in` Loop
Iterates over **enumerable properties** (own + prototype):
```javascript
const obj = { a: 1, b: 2, c: 3 };

for (const key in obj) {
  console.log(`${key}: ${obj[key]}`);
}
// Output:
// a: 1
// b: 2
// c: 3

// Includes inherited enumerable properties!
const child = Object.create({ inherited: 'value' });
child.own = 'value';

for (const key in child) {
  console.log(key);
}
// Output:
// own
// inherited

// Better: filter to own properties only
for (const key in obj) {
  if (Object.hasOwn(obj, key)) {
    console.log(`${key}: ${obj[key]}`);
  }
}
```

### `Object.keys()`
Returns array of **own enumerable** property names:
```javascript
const person = { name: 'Alice', age: 30, email: 'alice@ex.com' };

const keys = Object.keys(person);
console.log(keys); // ['name', 'age', 'email']

// Iterate using keys
keys.forEach(key => {
  console.log(`${key}: ${person[key]}`);
});

// With inherited properties
const obj = Object.create({ inherited: 'value' });
obj.own = 'value';

console.log(Object.keys(obj)); // ['own'] — doesn't include inherited
```

### `Object.values()`
Returns array of **own enumerable** property values:
```javascript
const person = { name: 'Alice', age: 30, email: 'alice@ex.com' };

const values = Object.values(person);
console.log(values); // ['Alice', 30, 'alice@ex.com']

// Finding values
const hasAlice = Object.values(person).includes('Alice');
console.log(hasAlice); // true
```

### `Object.entries()`
Returns array of **own enumerable** [key, value] pairs:
```javascript
const person = { name: 'Alice', age: 30, email: 'alice@ex.com' };

const entries = Object.entries(person);
console.log(entries);
// [['name', 'Alice'], ['age', 30], ['email', 'alice@ex.com']]

// Iterate using entries
Object.entries(person).forEach(([key, value]) => {
  console.log(`${key}: ${value}`);
});

// Convert to object from entries
const pairs = [['x', 10], ['y', 20], ['z', 30]];
const obj = Object.fromEntries(pairs);
console.log(obj); // { x: 10, y: 20, z: 30 }
```

### Comparison of Iteration Methods

| Method | Includes Own | Includes Inherited | Includes Non-enumerable | Returns |
|--------|--------------|-------------------|------------------------|---------|
| `for...in` | ✅ | ✅ | ❌ | — |
| `Object.keys()` | ✅ | ❌ | ❌ | Array of keys |
| `Object.values()` | ✅ | ❌ | ❌ | Array of values |
| `Object.entries()` | ✅ | ❌ | ❌ | Array of [key, value] |
| `Object.getOwnPropertyNames()` | ✅ | ❌ | ✅ | Array of keys |

---

## 7. Static Methods on `Object`

### `Object.assign(target, source1, source2, ...)`
Copies own enumerable properties from sources to target (shallow copy):
```javascript
const target = { a: 1, b: 2 };
const source1 = { b: 3, c: 4 };
const source2 = { c: 5, d: 6 };

Object.assign(target, source1, source2);
console.log(target); // { a: 1, b: 3, c: 5, d: 6 }

// Create shallow copy
const original = { name: 'Alice', age: 30 };
const copy = Object.assign({}, original);
console.log(copy);   // { name: 'Alice', age: 30 }
console.log(copy === original); // false — different objects

// Merge multiple objects
const obj1 = { a: 1 };
const obj2 = { b: 2 };
const obj3 = { c: 3 };
const merged = Object.assign({}, obj1, obj2, obj3);
console.log(merged); // { a: 1, b: 2, c: 3 }

// WARNING: shallow copy only!
const obj = { user: { name: 'Alice' } };
const shallowCopy = Object.assign({}, obj);
shallowCopy.user.name = 'Bob';
console.log(obj.user.name); // 'Bob' — nested object shared!
```

### `Object.create(proto, propertiesObject?)`
Creates new object with specified prototype:
```javascript
// Create object with null prototype
const obj1 = Object.create(null);
console.log(Object.getPrototypeOf(obj1)); // null
console.log(obj1.toString); // undefined — no prototype

// Create object inheriting from another
const parent = {
  greet() { return 'Hello!'; }
};
const child = Object.create(parent);
child.name = 'Alice';

console.log(child.name);      // 'Alice' — own property
console.log(child.greet());   // 'Hello!' — inherited property

// With property descriptors
const obj2 = Object.create(null, {
  x: {
    value: 10,
    writable: true,
    enumerable: true,
    configurable: true
  }
});
console.log(obj2.x); // 10
```

### `Object.freeze()`
Makes object immutable (can't add, delete, or modify properties):
```javascript
const person = { name: 'Alice', age: 30 };

Object.freeze(person);

person.age = 25;        // Fails silently in non-strict mode
console.log(person.age); // 30 — unchanged

person.email = 'alice@ex.com'; // Fails silently
console.log(person);    // { name: 'Alice', age: 30 } — unchanged

delete person.name;     // Fails silently
console.log(person);    // { name: 'Alice', age: 30 }

// Check if frozen
console.log(Object.isFrozen(person)); // true

// Shallow freeze only!
const obj = { user: { name: 'Alice' } };
Object.freeze(obj);
obj.user.name = 'Bob';
console.log(obj.user.name); // 'Bob' — nested object not frozen!
```

### `Object.seal()`
Allows modifying existing properties but prevents adding/deleting:
```javascript
const person = { name: 'Alice', age: 30 };

Object.seal(person);

person.age = 25;        // Works — modify existing property
console.log(person.age); // 25 — changed

person.email = 'alice@ex.com'; // Fails silently
console.log(person.email); // undefined — can't add

delete person.name;     // Fails silently
console.log(person);    // { name: 'Alice', age: 25 } — can't delete

// Check if sealed
console.log(Object.isSealed(person)); // true
```

### `Object.prevent Extensions()`
Prevents adding new properties but allows modification/deletion:
```javascript
const obj = { x: 1 };

Object.preventExtensions(obj);

obj.x = 10;         // Works
console.log(obj.x); // 10

obj.y = 20;         // Fails silently
console.log(obj.y); // undefined

delete obj.x;       // Works
console.log(obj);   // {}

// Check
console.log(Object.isExtensible(obj)); // false
```

### `Object.defineProperty()`
Defines or modifies a single property with detailed control:
```javascript
const obj = {};

Object.defineProperty(obj, 'x', {
  value: 10,
  writable: false,      // Can't change value
  enumerable: true,     // Shows in Object.keys()
  configurable: false   // Can't delete or reconfigure
});

console.log(obj.x);     // 10
obj.x = 20;             // Fails silently
console.log(obj.x);     // 10 — unchanged

// With getter/setter
const obj2 = {};

Object.defineProperty(obj2, 'name', {
  get() {
    return this._name || 'Unknown';
  },
  set(value) {
    this._name = value;
  },
  enumerable: true,
  configurable: true
});

obj2.name = 'Alice';
console.log(obj2.name); // 'Alice'
console.log(obj2._name); // 'Alice' — stored in _name
```

### `Object.getOwnPropertyDescriptor()`
Returns property descriptor object:
```javascript
const obj = { x: 10 };

const descriptor = Object.getOwnPropertyDescriptor(obj, 'x');
console.log(descriptor);
// {
//   value: 10,
//   writable: true,
//   enumerable: true,
//   configurable: true
// }

// Non-existent property
const missing = Object.getOwnPropertyDescriptor(obj, 'y');
console.log(missing); // undefined
```

### `Object.getOwnPropertyDescriptors()`
Returns all property descriptors:
```javascript
const obj = { x: 10, y: 20 };

const descriptors = Object.getOwnPropertyDescriptors(obj);
console.log(descriptors);
// {
//   x: { value: 10, writable: true, enumerable: true, configurable: true },
//   y: { value: 20, writable: true, enumerable: true, configurable: true }
// }
```

### `Object.fromEntries()`
Creates object from [key, value] pairs:
```javascript
const entries = [
  ['name', 'Alice'],
  ['age', 30],
  ['email', 'alice@ex.com']
];

const obj = Object.fromEntries(entries);
console.log(obj);
// { name: 'Alice', age: 30, email: 'alice@ex.com' }

// Reverse Object.entries()
const original = { x: 1, y: 2, z: 3 };
const entries2 = Object.entries(original);
const copy = Object.fromEntries(entries2);
console.log(copy); // { x: 1, y: 2, z: 3 }

// From Map
const map = new Map([['a', 1], ['b', 2]]);
const fromMap = Object.fromEntries(map);
console.log(fromMap); // { a: 1, b: 2 }
```

---

## 8. Destructuring Objects

### Basic Destructuring
```javascript
const person = { name: 'Alice', age: 30, email: 'alice@ex.com' };

const { name, age, email } = person;
console.log(name); // 'Alice'
console.log(age);  // 30

// Order doesn't matter
const { email, name } = person;
console.log(name, email); // 'Alice alice@ex.com'
```

### Partial Destructuring
```javascript
const person = { name: 'Alice', age: 30, email: 'alice@ex.com', phone: '123' };

const { name, age } = person;
console.log(name, age); // 'Alice' 30
```

### Renaming Properties
```javascript
const person = { name: 'Alice', age: 30 };

const { name: firstName, age: years } = person;
console.log(firstName); // 'Alice'
console.log(years);     // 30
console.log(name);      // ReferenceError — 'name' doesn't exist
```

### Default Values
```javascript
const person = { name: 'Alice', age: 30 };

const { name, age, email = 'unknown@ex.com' } = person;
console.log(name);  // 'Alice'
console.log(email); // 'unknown@ex.com'

// With undefined
const obj = { x: undefined, y: 10 };
const { x = 0, y = 0 } = obj;
console.log(x); // 0 — applies default because value is undefined
console.log(y); // 10
```

### Rest Properties (`...`)
```javascript
const person = { name: 'Alice', age: 30, email: 'alice@ex.com', phone: '123' };

const { name, age, ...rest } = person;
console.log(name);  // 'Alice'
console.log(age);   // 30
console.log(rest);  // { email: 'alice@ex.com', phone: '123' }
```

### Nested Destructuring
```javascript
const user = {
  name: 'Alice',
  address: {
    city: 'New York',
    zip: '10001'
  },
  hobbies: ['reading', 'coding']
};

// Nested object
const { name, address: { city, zip } } = user;
console.log(city); // 'New York'

// With renaming
const { address: { city: userCity } } = user;
console.log(userCity); // 'New York'

// Nested array
const { hobbies: [hobby1, hobby2] } = user;
console.log(hobby1); // 'reading'
console.log(hobby2); // 'coding'

// Nested with rest
const { address: { city, ...otherAddress }, ...otherUser } = user;
console.log(city);           // 'New York'
console.log(otherAddress);   // { zip: '10001' }
console.log(otherUser);      // { name: 'Alice', hobbies: [...] }
```

### Destructuring in Function Parameters
```javascript
const person = { name: 'Alice', age: 30 };

function greet({ name, age }) {
  console.log(`Hello ${name}, you are ${age} years old`);
}

greet(person); // 'Hello Alice, you are 30 years old'

// With defaults
function info({ name = 'Unknown', age = 0, email = 'N/A' } = {}) {
  console.log(`${name}, ${age}, ${email}`);
}

info(); // 'Unknown, 0, N/A'
info({ name: 'Bob' }); // 'Bob, 0, N/A'

// Rest in parameters
function printUser({ name, ...details }) {
  console.log(name);
  console.log(details);
}

printUser({ name: 'Alice', age: 30, email: 'alice@ex.com' });
// 'Alice'
// { age: 30, email: 'alice@ex.com' }
```

---

## 9. Copying Objects

### Shallow Copy
Objects are referenced, not copied:
```javascript
const original = { name: 'Alice', age: 30 };
const ref = original;

ref.age = 25;
console.log(original.age); // 25 — same object!

// Shallow copy with spread
const copy1 = { ...original };
console.log(copy1 === original); // false — different object
console.log(copy1); // { name: 'Alice', age: 25 }

// Shallow copy with Object.assign()
const copy2 = Object.assign({}, original);
console.log(copy2 === original); // false

// WARNING: shallow copy doesn't copy nested objects
const nested = {
  user: { name: 'Alice' },
  score: 100
};
const shallowCopy = { ...nested };

shallowCopy.user.name = 'Bob';
console.log(nested.user.name); // 'Bob' — nested object shared!

shallowCopy.score = 200;
console.log(nested.score); // 100 — primitives not affected
```

### Deep Copy
Copies everything including nested objects:
```javascript
const nested = {
  user: { name: 'Alice', age: 30 },
  hobbies: ['reading', 'coding']
};

// Using structuredClone() (ES2022 — recommended)
const deepCopy = structuredClone(nested);

deepCopy.user.name = 'Bob';
deepCopy.hobbies[0] = 'gaming';

console.log(nested.user.name);    // 'Alice' — unchanged
console.log(nested.hobbies[0]);   // 'reading' — unchanged

// Using JSON (works for JSON-serializable objects)
const jsonCopy = JSON.parse(JSON.stringify(nested));
jsonCopy.user.name = 'Charlie';
console.log(nested.user.name); // 'Alice' — unchanged

// WARNING: JSON method loses functions, undefined, Symbols, Dates
const obj = {
  name: 'Alice',
  date: new Date(),
  method: function() {},
  undef: undefined
};
const copy = JSON.parse(JSON.stringify(obj));
console.log(copy);
// { name: 'Alice', date: '2026-02-18T...' } — date is string, method/undef lost!

// Recursive deep copy (for complex cases)
function deepClone(obj) {
  if (obj === null || typeof obj !== 'object') return obj;
  if (obj instanceof Date) return new Date(obj);
  if (obj instanceof Array) return obj.map(item => deepClone(item));
  
  const cloned = {};
  for (const key in obj) {
    if (Object.hasOwn(obj, key)) {
      cloned[key] = deepClone(obj[key]);
    }
  }
  return cloned;
}

const customCopy = deepClone(nested);
customCopy.user.name = 'David';
console.log(nested.user.name); // 'Alice' — unchanged
```

---

## 10. Optional Chaining

### Optional Chaining for Properties (`?.`)
Safely access properties that might not exist:
```javascript
const user = {
  name: 'Alice',
  address: {
    city: 'New York'
  }
};

// Without optional chaining — dangerous!
console.log(user.address.zip); // undefined
// console.log(user.phone.number); // Error! phone is undefined

// With optional chaining
console.log(user.address?.zip); // undefined — safe!
console.log(user.phone?.number); // undefined — safe!

// Chaining multiple levels
console.log(user.address?.street?.name); // undefined — safe!

// Nullish coalescing with optional chaining
const city = user.address?.city ?? 'Unknown';
console.log(city); // 'New York'

const zip = user.address?.zip ?? 'N/A';
console.log(zip); // 'N/A'
```

### Optional Chaining for Methods (`?.`)
```javascript
const obj = {
  method: function() {
    return 'Hello!';
  }
};

console.log(obj.method?.()); // 'Hello!'
console.log(obj.other?.());  // undefined — method doesn't exist

// In event handlers
const button = document.querySelector('button');
button?.addEventListener('click', () => {
  console.log('Clicked!');
});

// With potentially missing methods
const response = {
  data: {
    items: [1, 2, 3]
  }
};

console.log(response.data?.getItems?.()); // undefined — method doesn't exist
```

### Optional Chaining for Arrays (`?.[]`)
```javascript
const arrays = {
  list: [1, 2, 3]
};

console.log(arrays.list?.[0]); // 1
console.log(arrays.missing?.[0]); // undefined — safe!

// With dynamic index
const index = 1;
console.log(arrays.list?.[index]); // 2
```

---

## 11. Property Descriptors

Every property has a descriptor object with metadata:

### Property Descriptor Attributes

```javascript
const obj = { x: 10 };

const descriptor = Object.getOwnPropertyDescriptor(obj, 'x');
console.log(descriptor);
// {
//   value: 10,              // The property value
//   writable: true,         // Can the value be changed?
//   enumerable: true,       // Shows in Object.keys()?
//   configurable: true      // Can descriptor be changed/deleted?
// }
```

### `value` Attribute
```javascript
const obj = {};
Object.defineProperty(obj, 'x', {
  value: 10
});

console.log(obj.x); // 10
```

### `writable` Attribute
Controls if the property value can be modified:
```javascript
const obj = {};

Object.defineProperty(obj, 'constant', {
  value: 42,
  writable: false
});

console.log(obj.constant); // 42
obj.constant = 100;        // Fails silently (or Error in strict mode)
console.log(obj.constant); // 42 — unchanged
```

### `enumerable` Attribute
Controls if property appears in `Object.keys()`, `for...in`, etc.:
```javascript
const obj = { visible: 1 };

Object.defineProperty(obj, 'hidden', {
  value: 2,
  enumerable: false
});

console.log(Object.keys(obj)); // ['visible'] — hidden not included
for (const key in obj) {
  console.log(key);
}
// Output: 'visible' — hidden not included

console.log(obj.hidden); // 2 — still accessible!
console.log(Object.getOwnPropertyNames(obj)); // ['visible', 'hidden']
```

### `configurable` Attribute
Controls if descriptor can be modified or property deleted:
```javascript
const obj = {};

Object.defineProperty(obj, 'locked', {
  value: 10,
  configurable: false
});

// Can't delete
delete obj.locked;
console.log(obj.locked); // 10 — still there

// Can't reconfigure (with rare exceptions)
Object.defineProperty(obj, 'locked', {
  enumerable: true
}); // TypeError

// Can change 'writable' if currently true and configurable false
const obj2 = {};
Object.defineProperty(obj2, 'x', {
  value: 10,
  writable: true,
  configurable: false
});

Object.defineProperty(obj2, 'x', {
  writable: false // Allowed
});

obj2.x = 20;
console.log(obj2.x); // 10 — now not writable
```

### Getters and Setters

Define custom get/set behavior:
```javascript
const obj = {};

Object.defineProperty(obj, 'name', {
  get() {
    console.log('Getting name');
    return this._name || 'Unknown';
  },
  set(value) {
    console.log(`Setting name to ${value}`);
    this._name = value;
  },
  enumerable: true,
  configurable: true
});

console.log(obj.name); // 'Unknown'
obj.name = 'Alice';    // Calls setter
console.log(obj.name); // 'Alice'

// Or with object literal syntax
const person = {
  _age: 0,
  get age() {
    return this._age;
  },
  set age(value) {
    if (value < 0) {
      console.log('Age cannot be negative');
      return;
    }
    this._age = value;
  }
};

console.log(person.age); // 0
person.age = 30;
console.log(person.age); // 30
person.age = -5;         // Validation failed
console.log(person.age); // 30 — unchanged
```

### Getters and Setters with Classes
```javascript
class Rectangle {
  constructor(width, height) {
    this._width = width;
    this._height = height;
  }

  get width() {
    return this._width;
  }

  set width(value) {
    if (value <= 0) throw new Error('Width must be positive');
    this._width = value;
  }

  get height() {
    return this._height;
  }

  set height(value) {
    if (value <= 0) throw new Error('Height must be positive');
    this._height = value;
  }

  get area() {
    return this._width * this._height;
  }
}

const rect = new Rectangle(10, 20);
console.log(rect.area); // 200
rect.width = 15;
console.log(rect.area); // 300
```

---

## 12. Prototype Chain

Every object has an internal `[[Prototype]]` property that links it to another object (its prototype):

```javascript
const parent = {
  greet() { return 'Hello!'; }
};

const child = Object.create(parent);
child.name = 'Alice';

// Own property
console.log(child.name); // 'Alice'
console.log(Object.hasOwn(child, 'name')); // true

// Inherited property (via prototype)
console.log(child.greet()); // 'Hello!'
console.log(Object.hasOwn(child, 'greet')); // false

// Get prototype
console.log(Object.getPrototypeOf(child) === parent); // true

// Check if value is in prototype chain
console.log('greet' in child); // true — includes inherited
```

### Prototype Chain Walk-through
```javascript
const obj = { x: 1 };

// Property lookup:
// 1. Check own properties
console.log(obj.x); // 1 — found

// 2. Check prototype
console.log(obj.toString); // [Function: toString] — inherited from Object.prototype

// 3. Continue up chain
console.log(Object.getPrototypeOf(obj) === Object.prototype); // true
console.log(Object.getPrototypeOf(Object.prototype)); // null — end of chain
```

---

## Summary: Object Methods Quick Reference

| Method | Purpose |
|--------|---------|
| `Object.assign()` | Shallow copy/merge objects |
| `Object.create()` | Create object with specific prototype |
| `Object.freeze()` | Make object immutable |
| `Object.seal()` | Prevent adding/deleting properties |
| `Object.preventExtensions()` | Prevent adding new properties |
| `Object.keys()` | Get own enumerable property names |
| `Object.values()` | Get own enumerable property values |
| `Object.entries()` | Get own enumerable [key, value] pairs |
| `Object.fromEntries()` | Create object from [key, value] pairs |
| `Object.defineProperty()` | Define property with detailed control |
| `Object.getOwnPropertyDescriptor()` | Get property descriptor |
| `Object.hasOwn()` | Check if own property exists |
| `Object.getPrototypeOf()` | Get object's prototype |

---

## Best Practices

✅ **Use `Object.hasOwn()` over `hasOwnProperty()`** — More reliable

✅ **Use `Object.keys()`, `Object.values()`, `Object.entries()` instead of `for...in`** — More predictable

✅ **Use spread `{...obj}` for shallow copies** — Clear and concise

✅ **Use `structuredClone()` for deep copies** — Modern standard

✅ **Use optional chaining `?.` for safe property access** — Prevents errors

✅ **Use object destructuring in function parameters** — More readable

✅ **Use `Object.freeze()` for immutable data** — Prevents accidental mutation

✅ **Prefer getter/setter for validation** — Centralized logic

---

## Common Gotchas

❌ **`for...in` includes inherited enumerable properties**
```javascript
const obj = Object.create({ inherited: 'value' });
obj.own = 'value';

for (const key in obj) {
  console.log(key); // 'own', 'inherited' — both!
}

// Use hasOwn to filter
for (const key in obj) {
  if (Object.hasOwn(obj, key)) {
    console.log(key); // 'own' — only own property
  }
}
```

❌ **Spread and Object.assign() create shallow copies**
```javascript
const obj = { user: { name: 'Alice' } };
const copy = { ...obj };

copy.user.name = 'Bob';
console.log(obj.user.name); // 'Bob' — nested object shared!
```

❌ **Property descriptors have different defaults**
```javascript
// Literal properties: all true
const obj1 = { x: 1 };
let desc = Object.getOwnPropertyDescriptor(obj1, 'x');
console.log(desc.enumerable); // true

// Defined with defineProperty: all false by default
const obj2 = {};
Object.defineProperty(obj2, 'x', { value: 1 });
desc = Object.getOwnPropertyDescriptor(obj2, 'x');
console.log(desc.enumerable); // false!
```

❌ **delete doesn't return value to variable**
```javascript
const obj = { x: 1 };
const deleted = delete obj.x;

console.log(deleted); // true (was deletion successful)
console.log(obj.x);   // undefined (property is gone)
```

❌ **Optional chaining returns `undefined`, not falsy**
```javascript
const obj = null;
console.log(obj?.x); // undefined (not false, not null, not 0)

// Use nullish coalescing for defaults
const value = obj?.x ?? 'default';
console.log(value); // 'default'
```
