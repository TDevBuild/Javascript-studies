# JavaScript — Strings and Methods

> String indexes, escape characters, template literals, indexOf(), prompt(), basic DOM, charCodeAt(), includes(), slice(), toUpperCase/toLowerCase, and trim().
> Study source: freeCodeCamp · July 2–7

## Table of Contents
1. [String indexes](#1-string-indexes)
2. [Escape characters](#2-escape-characters)
3. [Template literals](#3-template-literals)
4. [indexOf()](#4-indexof)
5. [prompt()](#5-prompt)
6. [document and getElementById()](#6-document-and-getelementbyid)
7. [ASCII, Unicode, and charCodeAt()](#7-ascii-unicode-and-charcodeat)
8. [includes()](#8-includes)
9. [slice()](#9-slice)
10. [Uppercase and lowercase](#10-uppercase-and-lowercase)
11. [trim(), trimStart(), and trimEnd()](#11-trim-trimstart-and-trimend)
12. [Quick recaps](#12-quick-recaps)

---

## 1. String indexes

Each character has a position. Counting always starts at index **0**.

```js
let name = "Portugal";
console.log(name[3]); // "t"
```

**Last letter** — `length` returns the total number of characters; since indexes start at 0, the last index is `length - 1`:

```js
let name = "Portugal";
console.log(name[name.length - 1]); // "l"  (8 characters, last index = 7)
```

**Joining letters from different indexes:**

```js
let name = "Portugal";
let selectedLetters = name[0] + name[5];
console.log(selectedLetters); // "Pg"
```

## 2. Escape characters

The backslash `\` allows special characters inside a string.

| Escape | Purpose |
|---|---|
| `\'` | Single quote inside a single-quoted string |
| `\"` | Double quote inside a double-quoted string |
| `\n` | New line |

```js
let a = 'It\'s a nice day';
let b = "Laura said \"Hello\"";
let c = "First line\nSecond line";
```

> ⚠️ Don't put a space after `\n` — that space would appear at the start of the next line.

## 3. Template literals

Structure: `` ` ${ } ` `` — opens and closes with a **backtick**; `${ }` inserts variables or expressions.

```js
let name = "Marco";
let age = 30;
let output = `${name} Costa is a ${age}-year-old man`;
console.log(output); // Marco Costa is a 30-year-old man
```

Expressions can also go inside `${ }`:

```js
const age = 30;
const score = 2;
console.log(`Result: ${age / score}`); // Result: 15
```

## 4. indexOf()

Searches for text inside a string and returns the position where it starts. Written with a lowercase `i` and uppercase `O`.

```js
const message = "I love Laura";
console.log(message.indexOf("Laura")); // 7
console.log(message.indexOf("white")); // -1
```

**Rules:**
1. It's case-sensitive (`"Laura"` ≠ `"laura"`)
2. Every character counts (including spaces) and counting starts at 0
3. When nothing is found → it always returns **-1**

**Searching from a given position:**

```js
const message = "I love Laura so I live with Laura";
console.log(message.indexOf("Laura", 15)); // 28 (skips the first one, at index 7)
```

## 5. prompt()

Asks the user a question in the browser and stores the answer.

```js
let user = prompt("What's your name?");
```

**With a default value:**

```js
let user = prompt("What's your name?", "Guest");
```

- `"Guest"` is just the value that appears pre-filled in the box
- If the user doesn't change it and clicks OK → `user = "Guest"`
- If they click Cancel → the result is `null`

## 6. document and getElementById()

```js
const score = document.getElementById("score");
```

| Part | Meaning |
|---|---|
| `document` | Represents the current HTML page |
| `getElementById("score")` | Finds the element with `id="score"` |

Each `id` must be **unique** in an HTML page.

## 7. ASCII, Unicode, and charCodeAt()

- **ASCII** is a table that assigns a number to each basic character — 128 codes, from 0 to 127
- Uppercase and lowercase letters have different codes: `A = 65` · `a = 97`

| Method | Direction |
|---|---|
| `charCodeAt(index)` | character → number |
| `String.fromCharCode(number)` | number → character |

```js
"A".charCodeAt(0);        // 65
String.fromCharCode(65);  // "A"

"Olá".charCodeAt(2);      // 225 → UTF-16/Unicode value of "á"
```

> ⚠️ The character `á` is **not** part of ASCII (which only goes up to 127). JavaScript uses UTF-16/Unicode. Also, you must write `String.fromCharCode()`, not just `fromCharCode()`.

## 8. includes()

Checks whether some text exists inside a string. Returns `true` or `false`. Case-sensitive.

```js
const sentence = "Marco is a strong man";
console.log(sentence.includes("strong")); // true
```

**With a starting position:**

```js
console.log(sentence.includes("strong", 7)); // true
// the search starts at index 7; "strong" starts at index 11, so it's still found
```

## 9. slice()

Extracts part of a string and returns it. **The original string is not changed.**

**1. With start and end** — includes the start, **excludes the end** (the last extracted character is `end - 1`):

```js
let message = "Hello, World!";
console.log(message.slice(0, 5)); // "Hello"
console.log(message.slice(0, 6)); // "Hello,"
```

**2. With start only** — goes to the end of the string:

```js
let name = "Marco is a big man";
console.log(name.slice(11)); // "big man"
```

**3. With a negative number** — counts from the end (`-1` = last character):

```js
console.log(name.slice(-3)); // "man"
```

## 10. Uppercase and lowercase

```js
const name = "marco costa";
console.log(name.toUpperCase()); // "MARCO COSTA"

const fullName = "LAURA DIAS";
console.log(fullName.toLowerCase()); // "laura dias"
```

The original string is not changed — each method returns a **new** string.

## 11. trim(), trimStart(), and trimEnd()

| Method | Removes spaces… |
|---|---|
| `trim()` | at the start **and** the end |
| `trimStart()` | only at the start |
| `trimEnd()` | only at the end |

```js
const name = "   Marco, Costa!   ";
console.log(name.trim());      // "Marco, Costa!"
console.log(name.trimStart()); // "Marco, Costa!   "
console.log(name.trimEnd());   // "   Marco, Costa!"
```

## 12. Quick recaps

### Strings and DOM
- Indexes start at **0**
- `length` counts letters, spaces, and symbols
- `name[name.length - 1]` → last letter
- `indexOf()` returns **-1** when nothing is found
- `prompt()` asks the user · `document.getElementById()` finds an element by `id`

### Search and extraction methods
| Concept | Purpose |
|---|---|
| `charCodeAt(i)` | Number associated with a character |
| `String.fromCharCode(n)` | Number → character |
| `includes(text)` | Checks existence (true/false) |
| `slice(start, end)` | Extracts a part without changing the original |
| `slice(-n)` | Counts from the end |

### Essential rule
> String methods **never change the original** — they always return a new string.
