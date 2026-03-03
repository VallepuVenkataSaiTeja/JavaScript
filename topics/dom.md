Absolutely! Let’s go **deep into DOM & Events in JavaScript**, with clear explanations, examples, and best practices. This will cover everything from the basics to event delegation and advanced handling.

---

# 🔹 1️⃣ What is the DOM?

> **DOM (Document Object Model)** is a tree-like representation of the HTML document.

* JavaScript can **read and manipulate** the DOM.
* Each element, attribute, and text node is an **object**.

### Example HTML

```html
<!DOCTYPE html>
<html>
  <body>
    <h1 id="title">Hello World</h1>
    <p class="text">Welcome to JS DOM!</p>
    <button id="btn">Click Me</button>
  </body>
</html>
```

---

# 🔹 2️⃣ Accessing DOM Elements

### 2.1 By ID

```js
const title = document.getElementById("title");
console.log(title.textContent); // "Hello World"
```

### 2.2 By Class Name

```js
const paragraphs = document.getElementsByClassName("text");
console.log(paragraphs[0].textContent); // "Welcome to JS DOM!"
```

### 2.3 By Tag Name

```js
const buttons = document.getElementsByTagName("button");
console.log(buttons[0].textContent); // "Click Me"
```

### 2.4 Modern: querySelector & querySelectorAll

```js
const title = document.querySelector("#title"); // first match
const texts = document.querySelectorAll(".text"); // all matches
```

---

# 🔹 3️⃣ Modifying the DOM

### 3.1 Change Text Content

```js
title.textContent = "Hello JS";
```

### 3.2 Change HTML Content

```js
const p = document.querySelector(".text");
p.innerHTML = "Welcome <strong>JavaScript</strong>!";
```

### 3.3 Change Attributes

```js
const btn = document.getElementById("btn");
btn.setAttribute("disabled", true);
btn.removeAttribute("disabled");
```

### 3.4 Change Styles

```js
title.style.color = "red";
title.style.fontSize = "30px";
```

---

# 🔹 4️⃣ Creating and Adding Elements

```js
const div = document.createElement("div");
div.textContent = "New Element";
div.style.color = "blue";

document.body.appendChild(div); // Add to DOM
```

* `appendChild()` → adds at the end
* `prepend()` → adds at the beginning
* `insertBefore()` → insert at specific position

---

# 🔹 5️⃣ Removing Elements

```js
const oldDiv = document.querySelector("div");
oldDiv.remove(); // modern
```

Or:

```js
oldDiv.parentNode.removeChild(oldDiv); // older method
```

---

# 🔹 6️⃣ Event Handling

> Events are **actions** performed by users or the browser (click, input, load, etc.).

### 6.1 Inline Event (not recommended)

```html
<button onclick="alert('Clicked!')">Click</button>
```

### 6.2 DOM Property

```js
btn.onclick = function() {
  alert("Clicked!");
};
```

* Overwrites previous handlers

### 6.3 addEventListener (Recommended)

```js
btn.addEventListener("click", function() {
  alert("Clicked!");
});
```

* Can attach **multiple handlers**
* Can remove handler later using `removeEventListener`

---

# 🔹 7️⃣ Event Object

When an event occurs, JS passes an **event object**.

```js
btn.addEventListener("click", function(event) {
  console.log(event.type);   // "click"
  console.log(event.target); // the clicked element
});
```

---

# 🔹 8️⃣ Event Types

1. **Mouse Events** → click, dblclick, mouseover, mouseout
2. **Keyboard Events** → keydown, keyup, keypress
3. **Form Events** → submit, input, change
4. **Window Events** → load, resize, scroll

---

# 🔹 9️⃣ Event Bubbling & Capturing

### 9.1 Bubbling (Default)

Event starts from **target → parent → top**.

```js
document.body.addEventListener("click", () => console.log("Body clicked"));
btn.addEventListener("click", () => console.log("Button clicked"));
```

Clicking button outputs:

```
Button clicked
Body clicked
```

### 9.2 Capturing

```js
btn.addEventListener("click", () => console.log("Button clicked"), true);
```

* `true` → capture phase (parent → child)
* `false` (default) → bubble phase (child → parent)

---

# 🔹 10️⃣ Event Delegation

* Use a **single handler** for multiple child elements.
* Works by **checking event.target**.

```js
document.querySelector("#list").addEventListener("click", function(event) {
  if (event.target.tagName === "LI") {
    console.log("Clicked:", event.target.textContent);
  }
});
```

> Efficient for dynamic lists

---

# 🔹 11️⃣ Prevent Default & Stop Propagation

```js
const link = document.querySelector("a");

link.addEventListener("click", function(event) {
  event.preventDefault(); // stops navigation
  console.log("Link clicked!");
});

btn.addEventListener("click", function(event) {
  event.stopPropagation(); // stops bubbling
});
```

---

# 🔹 12️⃣ Common DOM Methods

| Method                     | Description              |
| -------------------------- | ------------------------ |
| `getElementById()`         | Select element by ID     |
| `getElementsByClassName()` | Select elements by class |
| `getElementsByTagName()`   | Select elements by tag   |
| `querySelector()`          | Select first match       |
| `querySelectorAll()`       | Select all matches       |
| `createElement()`          | Create new element       |
| `appendChild()`            | Add element at end       |
| `prepend()`                | Add element at start     |
| `remove()`                 | Remove element           |
| `setAttribute()`           | Set attribute            |
| `getAttribute()`           | Get attribute            |

---

# 🔹 13️⃣ Dynamic Example

```js
const list = document.createElement("ul");

["Apple","Banana","Cherry"].forEach(fruit => {
  const li = document.createElement("li");
  li.textContent = fruit;
  list.appendChild(li);
});

document.body.appendChild(list);

list.addEventListener("click", function(event) {
  if (event.target.tagName === "LI") {
    alert(`You clicked ${event.target.textContent}`);
  }
});
```

* Dynamically adds a list
* Handles clicks on all items via **event delegation**

---

# 🔹 14️⃣ Summary

* **DOM** → represents HTML as JS objects
* **Access elements** → getElementById, querySelector, etc.
* **Modify elements** → textContent, innerHTML, styles, attributes
* **Create & remove elements** → createElement, appendChild, remove
* **Events** → click, input, submit, etc.
* **Event handling** → addEventListener preferred
* **Event phases** → bubbling & capturing
* **Event delegation** → efficient for dynamic elements

---

Absolutely! Let’s go **deep into the BOM (Browser Object Model) in JavaScript**, explaining what it is, its components, and practical usage with examples.

---

# 🔹 1️⃣ What is BOM?

> **BOM (Browser Object Model)** is the part of JavaScript that allows you to **interact with the browser** itself, outside the document.

* Unlike the **DOM** which deals with **HTML content**, BOM deals with **browser windows, frames, navigation, and timing**.
* BOM objects are **global objects** in the browser environment.

---

# 🔹 2️⃣ The Global `window` Object

* The `window` object is the **root of BOM**.
* It represents the **browser window/tab**.
* All global objects and functions belong to `window`.

```js id="bom1"
console.log(window); // entire browser window object
console.log(window.document); // access the DOM
console.log(window.innerWidth, window.innerHeight); // viewport size
```

* You can omit `window`:

```js id="bom2"
alert("Hello");       // same as window.alert("Hello")
console.log(innerWidth); // same as window.innerWidth
```

---

# 🔹 3️⃣ Common BOM Objects

1. **window** → represents browser window
2. **navigator** → browser info
3. **screen** → screen info
4. **location** → URL & navigation
5. **history** → session history
6. **console** → debug/logging
7. **setTimeout / setInterval** → timers

---

# 🔹 4️⃣ window Methods

### 4.1 Alerts, Prompts, Confirms

```js id="bom3"
// Alert
window.alert("Hello World");

// Prompt
let name = window.prompt("Enter your name:");
console.log(name);

// Confirm
let proceed = window.confirm("Do you want to continue?");
console.log(proceed); // true/false
```

---

### 4.2 window.open() & window.close()

```js id="bom4"
let newWin = window.open("https://example.com", "_blank", "width=500,height=500");

// Close window after 3 seconds
setTimeout(() => newWin.close(), 3000);
```

---

### 4.3 window.scrollTo / scrollBy

```js id="bom5"
// Scroll to top-left
window.scrollTo(0,0);

// Scroll down 100px from current position
window.scrollBy(0,100);
```

---

# 🔹 5️⃣ navigator Object

* Contains **browser information**:

```js id="bom6"
console.log(navigator.userAgent); // Browser details
console.log(navigator.platform);  // OS
console.log(navigator.language);  // Browser language
console.log(navigator.onLine);    // true if online
```

---

# 🔹 6️⃣ screen Object

* Contains **screen/monitor info**:

```js id="bom7"
console.log(screen.width, screen.height); // screen resolution
console.log(screen.availWidth, screen.availHeight); // available screen space
```

---

# 🔹 7️⃣ location Object

* Controls **current URL and navigation**:

```js id="bom8"
console.log(location.href);      // full URL
console.log(location.hostname);  // domain
console.log(location.pathname);  // path

// Navigate
// location.href = "https://google.com";

// Reload page
// location.reload();
```

---

# 🔹 8️⃣ history Object

* Controls **browser history**:

```js id="bom9"
history.back();     // go back
history.forward();  // go forward
history.go(-2);     // go back 2 steps
```

* You cannot see the URLs in history due to security.

---

# 🔹 9️⃣ Timers: setTimeout & setInterval

### setTimeout

```js id="bom10"
setTimeout(() => {
  console.log("Executed after 2 seconds");
}, 2000);
```

### setInterval

```js id="bom11"
let count = 0;
const interval = setInterval(() => {
  console.log("Tick", ++count);
  if(count === 5) clearInterval(interval);
}, 1000);
```

---

# 🔹 10️⃣ BOM vs DOM

| Feature    | DOM                       | BOM                                          |
| ---------- | ------------------------- | -------------------------------------------- |
| Represents | HTML document             | Browser window/environment                   |
| Objects    | document, element nodes   | window, navigator, location, history, screen |
| Purpose    | Manipulate content        | Control browser & environment                |
| Example    | document.getElementById() | window.alert(), location.href                |

---

# 🔹 11️⃣ Modern Browser Notes

* `window` is **global**, so you can call methods without prefix.
* Some BOM features (like `alert` or `confirm`) **block UI**, avoid in production.
* Use `navigator`, `location`, `screen`, and `history` **for info or navigation**, not content.

---

# 🔹 12️⃣ Real-World Example

```js id="bom12"
// Check browser and alert user
if(navigator.userAgent.includes("Chrome")) {
  alert("You are using Chrome!");
}

// Auto-refresh page every 10 seconds
setInterval(() => location.reload(), 10000);
```

---

# 🔹 13️⃣ Summary

* **BOM = Browser Object Model** → control browser window & environment
* **window** → root object
* **navigator** → browser info
* **screen** → screen size
* **location** → URL & navigation
* **history** → browser history
* **Timers** → setTimeout, setInterval
* **Alerts, Prompts, Confirms** → simple UI dialogs

---


