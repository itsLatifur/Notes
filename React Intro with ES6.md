# React Basics

I understand React as a **component-based JavaScript library** for building user interfaces.

* Component-based means we **break the UI into small reusable pieces** called components.
* The same component can be reused in multiple places.
* UI logic is grouped by **component**, not separated strictly into HTML, CSS, and JS files.
* Each component controls its own structure, logic, and behavior.

---

# Hooks

React uses the **`use`** prefix so React can **identify and track hooks internally**.
Hooks allow **function components** to:

* Store state
* Run side effects
* Use React features without using class components

Hooks **must**:

* Start with `use`
* Be called at the **top level** of a component (not inside loops or conditions)

---

## `useState`

* `useState` is used to **store and update state** inside a function component.

**Example:**

```js
const [count, setCount] = useState(0);
```

I understand this as:

* `const []` is **array destructuring**, not just a constant array.
* `count` holds the **current value** of the state.
* `setCount` is a function used to **update the state**.
* We should **never update state directly**, like `count = count + 1`, because:

  * React will not detect the change
  * The component will not re-render
* `useState(0)` creates a piece of state and sets its **initial value** to `0`

`useState` returns:

* A state variable
* A function to update that variable

When `setCount` is called:

* React updates the state internally
* React **re-renders the component**
* The UI updates automatically based on the new state

**Example:**

```js
setCount(count + 1);
```

---

## `useEffect`

`useEffect` is used to **run side effects** — code that runs **because something happened**, not directly during rendering.

Common use cases:

* Log something when a component loads or updates
* Fetch data from an API
* Run code after a state or prop changes
* Clean up tasks (like removing event listeners)

### Dependency Array Behavior

```js
useEffect(() => {}, []);
```

* Runs **only once** when the component mounts (first render)

```js
useEffect(() => {}, [state]);
```

* Runs:

  * Once on mount
  * Again **whenever `state` changes**

```js
useEffect(() => {});
```

* Runs **after every render**
* Can cause performance issues if used carelessly

---

# ES6 Essentials for React

These are **modern JavaScript features** that make React code cleaner and easier to read.

---

## `const` and Mutability

I understand that:

* `const` variables **cannot be reassigned**
* But **objects and arrays declared with `const` can have their internal values changed** in plain JavaScript

Example (JavaScript):

```js
const arr = [1, 2, 3];
arr.push(4); // allowed in JS
```

But in **React state**:

* We should **not mutate state directly**
* Even methods like `push()` should be avoided
* React relies on **new references** to detect changes

Correct way in React:

```js
setArr([...arr, 4]);
```

---

## Spread Operator (`...`)

The spread operator is used to **create a new copy** of arrays or objects and update only the values we want.

This helps React **detect state changes properly**.

### Array Example

```js
setId([1, ...nums, 6]);
```

Where:

```js
nums = [2, 3, 4, 5];
```

Result:

```js
[1, 2, 3, 4, 5, 6]
```

### Object Example

```js
const student = {
  id: 22103280,
  program: "BCSE",
  age: 22,
  sec: "A"
};

const student1 = {
  ...student,
  id: 22103281,
  age: 21
};
```

Here:

* Only `id` and `age` are changed
* All other properties remain the same

---

## Arrow Functions

Arrow functions are a **shorter way to write functions**.

```js
const add = (a, b) => a + b;
```

* They **do not have their own `this`**, which can help avoid confusion in callbacks.
* Commonly used in React for **event handlers** and **mapping arrays**.

---

## Template Literals

Template literals allow **easy string interpolation**.

```js
const name = "Alice";
console.log(`Hello, my name is ${name}`);
```

* Useful inside JSX:

```js
<h1>Hello, {`My name is ${name}`}</h1>
```

---

## Array Methods

Array methods like `map`, `filter`, `find`, and `reduce` are very useful in React, especially for rendering lists.

```js
const nums = [1, 2, 3];
const doubled = nums.map(n => n * 2); // [2, 4, 6]
```

---

## Optional Chaining and Nullish Coalescing

Useful when **data may be missing**, e.g., API responses:

```js
console.log(user?.address?.street ?? "No street");
```

* `?.` stops the code from crashing if a property is missing.
* `??` provides a default value if the left side is `null` or `undefined`.

---

## Destructuring Props

Destructuring allows **clean access to props** in components:

```js
const MyComponent = ({ name, age }) => <p>{name} is {age}</p>;
```

---

## Default Parameters

Functions can have **default values**:

```js
const greet = (name = "Guest") => console.log(`Hello ${name}`);
```

* Prevents `undefined` errors when arguments are missing.

---

# Export and Import

I understand that:

* I can export a function, variable, or component using `export`
* After exporting, I can use `import` in another file

### Named Export

```js
export const MyComponent = () => {};
```

Import using curly braces:

```js
import { MyComponent } from "./MyComponent";
```

### Default Export

```js
export default MyComponent;
```

Import **without** curly braces:

```js
import MyComponent from "./MyComponent";
```

---

# Event Handling in React

Event handling is slightly different from plain JavaScript.

* Use **camelCase** event names
* Pass a **function reference** or arrow function

```js
<button onClick={() => setCount(count + 1)}>Increment</button>
```

---

# Handling Lists and Keys in JSX

When rendering arrays, each element must have a **unique `key`**:

```js
{items.map(item => <li key={item.id}>{item.name}</li>)}
```

* Helps React **identify elements** during re-renders
* Prevents unnecessary re-rendering of unchanged items

---

# Fetch API and Async

* I have experience with `async` in **ASP.NET APIs**
* JavaScript is **single-threaded**, but it handles async tasks using:

  * Event loop
  * Promises
  * Async / Await

### Fetch in React

Fetch is usually called inside `useEffect`.

---

### GET Request

Steps:

* Pass the URL to `fetch()`
* Use `await` to wait for the response
* Convert JSON → JavaScript object using `response.json()`
* Store the result in state

Example:

```js
const response = await fetch(url);
const data = await response.json();
setData(data);
```

---

### POST Request

Steps:

* Provide the URL
* Set method to `POST`
* Add headers with `Content-Type: application/json`
* Convert JavaScript object → JSON using `JSON.stringify()`

Example:

```js
await fetch(url, {
  method: "POST",
  headers: {
    "Content-Type": "application/json"
  },
  body: JSON.stringify(user)
});
```

---

---

# React + ES6 **one-stop reference** Sheet (Quick Reference)

### **1. Components**

```js
// Function Component
const MyComponent = () => <h1>Hello World</h1>;

// Props
const Greeting = ({ name }) => <p>Hello, {name}</p>;
```

---

### **2. State with useState**

```js
const [count, setCount] = useState(0);

// Update state
setCount(count + 1);
```

---

### **3. Side Effects with useEffect**

```js
// Run once on mount
useEffect(() => {
  console.log("Mounted");
}, []);

// Run when 'count' changes
useEffect(() => {
  console.log(count);
}, [count]);

// Run after every render (use carefully)
useEffect(() => {
  console.log("Rendered");
});
```

---

### **4. Event Handling**

```js
<button onClick={() => setCount(count + 1)}>Increment</button>
```

---

### **5. Rendering Lists & Keys**

```js
const items = [{id: 1, name: "A"}, {id: 2, name: "B"}];
<ul>
  {items.map(item => <li key={item.id}>{item.name}</li>)}
</ul>
```

---

### **6. Export / Import**

```js
// Named export
export const MyComponent = () => {};
import { MyComponent } from "./MyComponent";

// Default export
export default MyComponent;
import MyComponent from "./MyComponent";
```

---

### **7. ES6 Essentials**

**Const / Let**

```js
const x = 5; // cannot reassign
let y = 10;  // can reassign
```

**Arrow Functions**

```js
const add = (a, b) => a + b;
```

**Template Literals**

```js
const name = "Alice";
console.log(`Hello ${name}`);
```

**Destructuring**

```js
const person = {name: "Bob", age: 25};
const {name, age} = person;
```

**Default Parameters**

```js
const greet = (name = "Guest") => console.log(`Hello ${name}`);
```

**Spread Operator**

```js
// Array
const arr = [1, 2];
const newArr = [0, ...arr, 3]; // [0,1,2,3]

// Object
const student = {id:1, name:"A"};
const updatedStudent = {...student, id:2};
```

**Optional Chaining & Nullish Coalescing**

```js
console.log(user?.address?.street ?? "No street");
```

**Array Methods**

```js
[1,2,3].map(n => n*2); // [2,4,6]
[1,2,3].filter(n => n>1); // [2,3]
[1,2,3].find(n => n===2); // 2
```

---

### **8. Fetch API (Async / Await)**

**GET**

```js
const response = await fetch(url);
const data = await response.json();
setData(data);
```

**POST**

```js
await fetch(url, {
  method: "POST",
  headers: {"Content-Type": "application/json"},
  body: JSON.stringify(user)
});
```