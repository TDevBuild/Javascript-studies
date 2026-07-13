# JavaScript Introduction

> Complete fundamentals: variables, data types, strings, concatenation, comments, and execution.
> Study source: freeCodeCamp · June 24–29

## Table of Contents
1. [What is JavaScript](#1-what-is-javascript)
2. [console.log()](#2-consolelog)
3. [Variables: let and const](#3-variables-let-and-const)
4. [Variable names](#4-variable-names)
5. [Data types and typeof](#5-data-types-and-typeof)
6. [Strings in detail](#6-strings-in-detail)
7. [String concatenation](#7-string-concatenation)
8. [Comments](#8-comments)
9. [How JavaScript is executed](#9-how-javascript-is-executed)

---

## 1. What is JavaScript

Each technology has a role on a website:

- **HTML** → structure (headings, text, images, buttons, sections)
- **CSS** → visual appearance (colors, sizes, margins, fonts, animations)
- **JavaScript** → behavior and logic

With JavaScript you can: respond to clicks, change text/images, validate forms, perform calculations, show/hide elements, and store information during execution. Its main purpose is to make a page **interactive**.

## 2. console.log()

Displays information in the developer console.

```js
console.log("I love to code!");
```

**Clean-writing rules:**
- No space between `log` and `(`
- No space before `)`
- Normally ends with `;`

Inside `console.log()`, commas separate values:

```js
let profession = "hacker";
let age = 30;
console.log("Work:", profession, "Age:", age);
// Work: hacker Age: 30
```

## 3. Variables: let and const

A variable stores information to use later.

```js
let age = 25;
```

- `let` → creates the variable
- `age` → variable name
- `=` → assigns the value
- `25` → stored value

### let — the value can change

```js
let score = 10;
score = 20; // correct (don't repeat let)
```

Code runs from top to bottom:

```js
let age = 25;
console.log(age); // 25
age = 30;
console.log(age); // 30
```

A variable declared with `let` can also start without a value (it becomes `undefined`) and receive one later.

### const — the value cannot change

```js
const score = 10;
score = 20;      // ❌ error
const age;       // ❌ error: const needs an initial value
```

**Summary:** `let` → can change · `const` → cannot be reassigned.

## 4. Variable names

Descriptive names make the code easier to understand:

```js
// Good
let userName = "Marco";
let userAge = 30;

// Avoid
let x = "Marco";
let y = 30;
```

### Syntax rules

A name can contain letters, numbers, `_`, and `$`. It can start with a letter, `_`, or `$` — **never with a number**.

| Rule | ❌ Wrong | ✅ Correct |
|---|---|---|
| Cannot start with a number | `let 123user;` | `let user123;` |
| No spaces | `let first name;` | `let firstName;` |
| No hyphens | `let user-name;` | `let userName;` |
| No `!` or `@` | `let user!Name;` | `let userName;` |
| No reserved words | `let let = 30;` | `let userAge = 30;` |

```js
// valid
let _score;
let $total;
let _1;
let $2;

// invalid
let 1stPlace;  // starts with a number
let user!Name; // ! is not allowed
```

### camelCase

Naming convention for multi-word names: first word lowercase, each following word starts with a capital letter.

```js
let userName = "Marco";
let isDarkModeEnabled = true;
```

## 5. Data types and typeof

The `typeof` operator identifies the data type of a value.

| typeof | Type | Example |
|---|---|---|
| `"number"` | Number (integer, decimal, negative) | `42`, `3.18` |
| `"string"` | Text between quotes | `"Marco"` |
| `"boolean"` | `true` or `false` | `true` |
| `"undefined"` | Declared but no value yet | `let x;` |
| `"object"` | Groups related data | `{ name: "Marco" }` |
| `"symbol"` | Unique primitive value | `Symbol("id")` |
| `"bigint"` | Very large integers | `9007199254740992n` |

```js
const age = 42;
const isLoggedIn = true;
const user = { name: "Marco" };

console.log(typeof age);        // "number"
console.log(typeof isLoggedIn); // "boolean"
console.log(typeof user);       // "object"
```

### Number

Integers and decimals belong to the **same type**: `number`.

```js
console.log(typeof 10);   // "number"
console.log(typeof 3.18); // "number"
```

### Boolean

Only two possible values, always lowercase: `true` and `false`. Mainly used in conditions and decisions.

### Undefined vs Null

```js
let score;
console.log(score); // undefined (no value yet)

let selectedUser = null; // intentionally empty
```

- `0` is a number
- `null` = **intentional** absence of value
- `undefined` = no value has been assigned yet

> ⚠️ Technical note: `typeof null` returns `"object"` due to a historical quirk of JavaScript, but `null` is not a real object.

### Object

Groups several pieces of data in one variable. Each piece is a property (key + value).

```js
let pet = {
  name: "Marco",
  age: 30,
  type: "Human"
};
console.log(typeof pet); // "object"
```

### Symbol

Creates unique values — even with the same description, two `Symbol()` calls are always different.

```js
const key1 = Symbol("saltNpepper");
const key2 = Symbol("saltNpepper");
console.log(key1 === key2); // false
```

Practical use: creating object keys that never collide with others.

### BigInt

Very large integers with exact precision. Ends with `n`. Does not accept decimals.

```js
const normalNumber = 9007199254740991;  // safe limit for number
const bigNumber = 9007199254740992n;    // from here on, use bigint

console.log(typeof bigNumber); // "bigint"
```

## 6. Strings in detail

Text between single or double quotes — **the opening and closing quotes must match**.

```js
let name = "Marco"; // ✅
// "Marco' ❌ mixed quotes
```

### Indexes

Each letter has a position. Counting starts at **0**.

| Letter | M | a | r | c | o |
|---|---|---|---|---|---|
| Index | 0 | 1 | 2 | 3 | 4 |

```js
name[0]; // "M"
name[2]; // "r"
```

You cannot change a single letter of a string — you replace the whole string instead.

## 7. String concatenation

| Operator/Method | Purpose |
|---|---|
| `+` | Joins strings into a new string |
| `+=` | Appends to the existing value and updates the variable |
| `.concat()` | Joins strings and returns a new one (doesn't change the original) |

```js
let firstName = "Marco";
let lastName = "Costa";
let fullName = firstName + " " + lastName;
console.log(fullName); // "Marco Costa"

let info = "Here is a nice place";
info += " Portugal";
console.log(info); // "Here is a nice place Portugal"

const name = firstName.concat(" ", lastName);
console.log(name); // "Marco Costa"
```

## 8. Comments

Text that JavaScript ignores during execution.

```js
// Single-line comment

/*
  Multi-line
  comment
*/
```

## 9. How JavaScript is executed

### Semicolon (;)

Marks the end of a **statement**. Recommended to always use it.

### ASI — Automatic Semicolon Insertion

A mechanism that automatically inserts `;` in certain situations. It's already active in Chrome and Node.js — but it's better to write your own `;` to avoid unexpected errors.

### JIT — Just-In-Time

The JIT compiles JavaScript directly into **machine code (0s and 1s)** that the processor executes. It's part of the JavaScript engine (e.g., V8 in Chrome and Node.js).

```
You write JS → Engine (V8) analyzes → JIT compiles to 0s and 1s → Processor executes
```

> Assembly is **not** a step in this process — it's just a human-readable representation of machine code.

**Where to write and test:** Chrome Console · a `.js` file in VS Code · `node example.js`

