# JavaScript Fundamentals Guide

## 🚀 1. DOM (Document Object Model)

### What is the DOM?

The DOM is the browser's **live version** of your page. It's **not** the HTML file itself—it's a tree of objects that JavaScript can modify in real-time.
```
HTML file → Browser reads it → Creates DOM → JavaScript modifies DOM → Page updates
```

### Key Properties

#### `textContent` vs `innerHTML` vs `value`
```javascript
// textContent → plain text only
title.textContent = "Hello World";

// innerHTML → can include HTML tags
box.innerHTML = "<b>Bold text</b>";

// value → for input fields
input.value = "";
```

### Important Concepts

#### Selecting Elements
```javascript
document.querySelector(".btn")   // by class
document.querySelector("#id")    // by id
document.querySelectorAll(".item")  // all elements with class
```

#### DOM Updates Are Manual

If you modify an array, the DOM doesn't automatically update:
```javascript
students.push("anas");
// You must manually re-render the DOM
```

---

## ⭐ 2. EVENTS

### Correct Event Listener Syntax
```javascript
// ✅ Correct 
btn.addEventListener("click", myFunction);

// ❌ Wrong 
btn.addEventListener("click", myFunction());
```

### Event Execution Order

JavaScript is **synchronous**, but event callbacks run **asynchronously** (when the event happens).

---

## 🎯 3. ARRAYS

### Array Methods: `filter()` vs `find()`
```javascript
const users = [
  {name: "anas", age: 20},
  {name: "brahim", age: 22},
  {name: "omar", age: 17}
];

// filter() → returns ARRAY of all matches
const adults = users.filter(u => u.age >= 18);
// Result: [{name: "anas", age: 20}, {name: "brahim", age: 22}]

// find() → returns FIRST match only
const user = users.find(u => u.name === "anas");
// Result: {name: "anas", age: 20}
```

### More Array Methods

#### `map()` - Transform Each Element
```javascript
const numbers = [1, 2, 3, 4];
const doubled = numbers.map(n => n * 2);
// Result: [2, 4, 6, 8]

const users = [{name: "anas", age: 20}, {name: "brahim", age: 22}];
const names = users.map(u => u.name);
// Result: ["anas", "brahim"]
```

#### `forEach()` - Loop Through Array
```javascript
const fruits = ["apple", "banana", "orange"];
fruits.forEach(fruit => {
  console.log(fruit);
});
// Prints each fruit
```

#### `reduce()` - Accumulate Values
```javascript
const numbers = [1, 2, 3, 4];
const sum = numbers.reduce((total, num) => total + num, 0);
// Result: 10

const cart = [
  {item: "book", price: 100},
  {item: "pen", price: 20}
];
const total = cart.reduce((sum, item) => sum + item.price, 0);
// Result: 120
```

#### `some()` and `every()`
```javascript
const numbers = [1, 2, 3, 4, 5];

// some() → checks if AT LEAST ONE element matches
const hasEven = numbers.some(n => n % 2 === 0);
// Result: true

// every() → checks if ALL elements match
const allPositive = numbers.every(n => n > 0);
// Result: true
```

#### `includes()` - Check if Element Exists
```javascript
const fruits = ["apple", "banana", "orange"];
fruits.includes("banana");  // true
fruits.includes("grape");   // false
```

#### `sort()` - Sort Array
```javascript
const numbers = [3, 1, 4, 1, 5];
numbers.sort((a, b) => a - b);  // ascending
// Result: [1, 1, 3, 4, 5]

numbers.sort((a, b) => b - a);  // descending
// Result: [5, 4, 3, 1, 1]

const users = [{name: "brahim"}, {name: "anas"}, {name: "omar"}];
users.sort((a, b) => a.name.localeCompare(b.name));
// Result: sorted alphabetically by name
```

### Working with Array of Objects
```javascript
const users = [
  {name: "anas", age: 20},
  {name: "brahim", age: 22}
];

// Loop through array of objects
users.forEach(u => console.log(u.name));
```

### `splice()` Method
```javascript
// splice(startIndex, howManyToDelete)
array.splice(2, 1);  // removes 1 element at index 2

// splice can also add elements
array.splice(2, 0, "newItem");  // adds "newItem" at index 2
```

### Arrays are References
```javascript
let a = [1, 2, 3];
let b = a;           // b points to same array
b.push(4);
console.log(a);      // [1, 2, 3, 4] ⚠️
```

---

## 🧱 4. OBJECTS

### Dot vs Bracket Notation
```javascript
const user = {name: "anas", age: 20};

// Dot notation
user.name

// Bracket notation (needed for dynamic keys)
user["age"]

let key = "name";
user[key]  // "anas"
```

### Modifying Objects

Objects are **mutable** (can be changed):
```javascript
user.age = 25;
user.city = "Marrakesh";
```

### Looping Through Objects

#### `for...in` Loop - Get Keys
```javascript
const user = {name: "anas", age: 20, city: "Marrakesh"};

for (let key in user) {
  console.log(key);         // prints: name, age, city
  console.log(user[key]);   // prints: anas, 20, Marrakesh
}
```

#### `Object.keys()` - Array of Keys
```javascript
const user = {name: "anas", age: 20, city: "Marrakesh"};

const keys = Object.keys(user);
// Result: ["name", "age", "city"]

keys.forEach(key => {
  console.log(`${key}: ${user[key]}`);
});
```

#### `Object.values()` - Array of Values
```javascript
const user = {name: "anas", age: 20, city: "Marrakesh"};

const values = Object.values(user);
// Result: ["anas", 20, "Marrakesh"]

values.forEach(value => console.log(value));
```

#### `Object.entries()` - Array of [Key, Value] Pairs
```javascript
const user = {name: "anas", age: 20, city: "Marrakesh"};

const entries = Object.entries(user);
// Result: [["name", "anas"], ["age", 20], ["city", "Marrakesh"]]

entries.forEach(([key, value]) => {
  console.log(`${key}: ${value}`);
});
```

### Object Methods

#### Check if Property Exists
```javascript
const user = {name: "anas", age: 20};

user.hasOwnProperty("name");     // true
user.hasOwnProperty("email");    // false

// or
"name" in user;                  // true
```

#### Merge Objects
```javascript
const user = {name: "anas"};
const details = {age: 20, city: "Marrakesh"};

const merged = {...user, ...details};
// Result: {name: "anas", age: 20, city: "Marrakesh"}

```

### Combining Arrays of Objects with DOM
```javascript
users.forEach(user => {
  list.innerHTML += `<li>${user.name}</li>`;
});
```

---

## 📦 5. LOCALSTORAGE

### Core Concept

**localStorage only stores strings.** Everything else must be converted.
```javascript
localStorage.setItem("age", 20);
localStorage.getItem("age");  // Returns "20" (string!)
```

### Storing Arrays/Objects

#### Step 1: Convert to JSON string
```javascript
localStorage.setItem("users", JSON.stringify(users));
```

#### Step 2: Parse when retrieving
```javascript
const users = JSON.parse(localStorage.getItem("users"));
```

### The Update Pattern

When modifying data in localStorage:
```javascript
// 1. Get data
let users = JSON.parse(localStorage.getItem("users"));

// 2. Modify it
users.push(newUser);

// 3. Save it back
localStorage.setItem("users", JSON.stringify(users));

// 4. Re-render the UI manually
renderUsers();
```

**Remember:** localStorage doesn't automatically update your UI—you must re-render manually.

---

## 🟥 6. VAR vs LET

### Key Differences

| Feature | var | let |
|---------|-----|-----|
| **Scope** | Function | Block |
| **Hoisting** | `undefined` | Error |
| **Redeclaration** | Allowed | Not allowed |

### Block Scope Example
```javascript
if (true) {
  let x = 10;
}
console.log(x);  // ❌ Error: x is not defined
```
```javascript
if (true) {
  var y = 10;
}
console.log(y);  // ✅ 10
```

### The `setTimeout` Loop Example

#### With `var`:
```javascript
for (var i = 1; i <= 3; i++) {
  setTimeout(() => console.log(i), 1000);
}

// Output after 1 second:
// 4
// 4
// 4
```

**Why?** There's only **one** `i` variable shared across all iterations.

#### With `let`:
```javascript
for (let i = 1; i <= 3; i++) {
  setTimeout(() => console.log(i), 1000);
}

// Output after 1 second:
// 1
// 2
// 3
```

**Why?** Each iteration gets its **own** `i` variable.

### Rule of Thumb

- `var` creates **one variable** for the whole scope
- `let` creates a **new variable** for each block


---

## 🌐 7. FETCH API - Working with APIs

### Complete Fetch Example
```javascript


async function loadUsers() {
  try {
    // Fetch data from API
    const response = await fetch("https://jsonplaceholder.typicode.com/users");
    
    // Check if request was successful
    if (!response.ok) {
      throw new Error("Failed to fetch users");
    }
    //  Convert response to JSON
    const users = await response.json();
    
  } catch (error) {
    // 6. Handle errors
    console.error("Error:", error);
    usersList.innerHTML = "Failed to load users!";
  }
}

```

### Key Points

- **`async`** - Makes the function asynchronous
- **`await`** - Waits for the fetch to complete
- **`try/catch`** - Handles any errors that occur
- **`response.ok`** - Checks if the request succeeded
- **`.json()`** - Converts the response to a JavaScript object

---

## 🌟 JavaScript Best Practices

### 1. Naming Conventions

#### Variables and Functions - Use camelCase
```javascript
// ✅ Good
let userName = "anas";
let totalPrice = 100;
function calculateTotal() { }
function getUserName() { }

// ❌ Bad
let user_name = "anas";
let UserName = "anas";
let TOTAL_PRICE = 100;
```

#### Constants - Use UPPERCASE_WITH_UNDERSCORES
```javascript
// ✅ Good
const MAX_USERS = 100;
const API_URL = "https://api.example.com";
const TAX_RATE = 0.15;

// ❌ Bad
const maxUsers = 100;
const apiUrl = "https://api.example.com";
```

#### Be Descriptive
```javascript
// ✅ Good
let userAge = 25;
let isLoggedIn = true;
let totalPrice = 150;
function calculateTotalPrice() { }

// ❌ Bad
let x = 25;
let flag = true;
let temp = 150;
function calc() { }
```

### 2. Semicolons

**Always use semicolons** to end statements:
```javascript
// ✅ Good
let name = "anas";
let age = 20;
console.log(name);

// ❌ Bad (can cause unexpected errors)
let name = "anas"
let age = 20
console.log(name)
```

### 3. Use `const` and `let`, Avoid `var`
```javascript
// ✅ Good
const PI = 3.14;           // won't change
let counter = 0;           // will change

// ❌ Bad
var PI = 3.14;
var counter = 0;
```

**Rule:** Use `const` by default. Use `let` only when you need to reassign.

### 4. Proper Indentation
```javascript
// ✅ Good
function calculateTotal(items) {
  let total = 0;
  items.forEach(item => {
    total += item.price;
  });
  return total;
}

// ❌ Bad
function calculateTotal(items) {
let total = 0;
items.forEach(item => {
total += item.price;
});
return total;
}
```

### 5. Meaningful Function Names

Functions should be **verbs** that describe what they do:
```javascript
// ✅ Good
function addUser() { }
function deleteTask() { }
function calculateTotal() { }
function renderItems() { }
function getUserById() { }

// ❌ Bad
function user() { }
function task() { }
function total() { }
function items() { }
```

### 6. Keep Functions Small and Focused

Each function should do **one thing**:
```javascript
// ✅ Good
function getUsers() {
  return JSON.parse(localStorage.getItem("users")) || [];
}

function saveUsers(users) {
  localStorage.setItem("users", JSON.stringify(users));
}

function renderUsers(users) {
  list.innerHTML = "";
  users.forEach(user => {
    list.innerHTML += `<li>${user.name}</li>`;
  });
}

// ❌ Bad - one function doing too much
function doEverything() {
  const users = JSON.parse(localStorage.getItem("users")) || [];
  users.push(newUser);
  localStorage.setItem("users", JSON.stringify(users));
  list.innerHTML = "";
  users.forEach(user => {
    list.innerHTML += `<li>${user.name}</li>`;
  });
}
```

### 7. Use Template Literals
```javascript
// ✅ Good
let message = `Hello, ${name}! You are ${age} years old.`;
let html = `<div class="user">${user.name}</div>`;

// ❌ Bad
let message = "Hello, " + name + "! You are " + age + " years old.";
let html = "<div class=\"user\">" + user.name + "</div>";
```

---

## 📌 Summary of Best Practices

✅ **DO:**
- Use `camelCase` for variables and functions
- Use `UPPERCASE_SNAKE_CASE` for constants
- Always use semicolons
- Use `const` by default, `let` when needed
- Write descriptive names
- Keep functions small and focused
- Use template literals for strings
- Check for null/undefined
- Add comments for complex logic
- Handle errors properly

❌ **DON'T:**
- Use `var`
- Write unclear variable names (`x`, `temp`, `data`)
- Create huge functions that do everything
- Forget to validate user input
- Mix quotes styles inconsistently
- Skip error handling