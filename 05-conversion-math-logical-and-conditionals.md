# JavaScript — Conversion, Math, Logical Operators & Conditionals

> Complete study log — how to turn text into numbers (`parseInt`, `parseFloat`), what `NaN` is and how to detect it, the mathematical methods of the `Math` object, the logical operators that produce `true`/`false`, and the `if` / `else if` / `else` structures that consume them.
> Study source: freeCodeCamp · July 20

## Table of Contents
1. [Why text has to be converted into numbers](#1-why-text-has-to-be-converted-into-numbers)
2. [Table — parseFloat() and parseInt()](#2-table--parsefloat-and-parseint)
3. [Main difference between the two](#3-main-difference-between-the-two)
4. [What is NaN](#4-what-is-nan)
5. [Table — isNaN() and Number.isNaN()](#5-table--isnan-and-numberisnan)
6. [Solved exercises](#6-solved-exercises)
7. [What is the Math object](#7-what-is-the-math-object)
8. [Table of mathematical methods](#8-table-of-mathematical-methods)
9. [Generating a random integer in a range](#9-generating-a-random-integer-in-a-range)
10. [Table — &&, || and ??](#10-table----and-)
11. [Truth tables](#11-truth-tables)
12. [Table — if, else if and else](#12-table--if-else-if-and-else)
13. [Full commented example](#13-full-commented-example)
14. [Cross-cutting rules](#14-cross-cutting-rules)
15. [Quick recap](#15-quick-recap)

---

## 1. Why text has to be converted into numbers

Many values arrive in the code as text — a form field, a value read from a file, a parameter in an address. That text looks like a number, but to JavaScript it's still a string. Before doing math with it, you have to convert it.

```
TEXT IS NOT A NUMBER
const text = "10";           // string
console.log(text + 5);       // "105" → joined text

const number = parseInt(text);
console.log(number + 5);     // 15 → actually added
```

## 2. Table — parseFloat() and parseInt()

Both functions read the number from the **start** of the string and stop as soon as they find something that isn't part of a number.

| Rule / Function | What it does | Example |
|---|---|---|
| `parseFloat()` | Reads a decimal number from the start of the string and stops at the first invalid character. | `parseFloat("3.95.8")` → `3.95` |
| `parseInt()` | Reads only the integer part from the start of the string and ignores the decimal part. | `parseInt("45.5")` → `45` |
| Number at the start | The number must appear at the start of the string. If it starts with letters, the result is `NaN`. | `parseFloat("abc 3.95")` → `NaN` |
| Leading spaces | Spaces before the number are ignored. | `parseInt("  42")` → `42` |
| Positive or negative sign | Both recognise `+` and `-` before the number. | `parseInt("-42")` → `-42` |

```js
console.log(parseFloat("3.95.8"));  // 3.95
console.log(parseInt("45.5"));      // 45
console.log(parseFloat("abc 3.95")); // NaN
console.log(parseInt("  42"));      // 42
console.log(parseInt("-42"));       // -42
```

## 3. Main difference between the two

> **Summary:**
> `parseFloat()` keeps the decimal part.
> `parseInt()` returns only the whole number.

> **Memory trick:** *Float* comes from "floating point" — it keeps the decimals. *Int* comes from "integer" — it cuts off everything after the decimal point.

> **Technical note — stopping at the first invalid character:** in `parseFloat("3.95.8")` the result is `3.95`, not `3.958`. The function accepts the first decimal point, but the second one is already invalid, so it stops there. Whatever comes after is simply discarded.

## 4. What is NaN

`NaN` stands for **Not a Number**. It shows up when JavaScript tried to produce a number but the result isn't a valid one — exactly what happens when a conversion fails.

```js
console.log(Number("abc"));   // NaN
console.log(parseInt("hi"));  // NaN
console.log(0 / 0);           // NaN
```

> ⚠️ **NaN is a number (as far as `typeof` is concerned):** despite the name, `typeof NaN` returns `"number"`. `NaN` belongs to the number type; it's just the value that represents an invalid numeric result.

## 5. Table — isNaN() and Number.isNaN()

Since `NaN` can't be compared normally, there are dedicated functions to detect it.

| Rule / Function | What it does | Example |
|---|---|---|
| `NaN` | Means JavaScript tried to produce a number, but the result isn't a valid number. | `Number("abc")` → `NaN` |
| `isNaN(value)` | Tries to convert the value to a number. If it can't, returns `true`. | `isNaN("abc")` → `true` |
| `Number.isNaN(value)` | Checks whether the value already **is** exactly `NaN`, without converting. | `Number.isNaN(NaN)` → `true` |

```js
console.log(isNaN("abc"));          // true
console.log(Number.isNaN(NaN));     // true
console.log(Number.isNaN("abc"));   // false (it's a string, not NaN)
```

> **Technical note — which one to use:** `isNaN()` converts before checking, which is why `isNaN("abc")` is `true` even though `"abc"` is a string and not `NaN`. `Number.isNaN()` converts nothing: it only returns `true` if the value really is `NaN`. When in doubt, `Number.isNaN()` is the more predictable version.

## 6. Solved exercises

### Exercise 1

```js
console.log(isNaN("123"));
```

```
Console output:
false
```

`"123"` is a string, but it can be converted into the number `123`. So it doesn't result in `NaN`.

### Exercise 2

Which one checks whether a value is exactly `NaN`?

```js
Number.isNaN(value);
```

This is the correct answer because it doesn't try to convert the value. It only checks whether it already **is** `NaN`.

### Exercise 3

```js
console.log(NaN === NaN);
```

```
Console output:
false
```

`NaN` has a special characteristic: it isn't equal to any value, not even to itself. That's precisely why the functions `isNaN()` and `Number.isNaN()` exist.

## 7. What is the Math object

`Math` is an object already built into JavaScript that gathers ready-to-use mathematical functions. You don't have to create anything: just write `Math.` followed by the method name.

> **Memory trick:** `ceil` is the ceiling — rounds up. `floor` is the floor — rounds down. `round` goes to the nearest one. `trunc` cuts and rounds nothing at all.

## 8. Table of mathematical methods

| Method | What it does | Example |
|---|---|---|
| `Math.random()` | Generates a random decimal between `0` (inclusive) and `1` (exclusive). | `Math.random()` → e.g. `0.426` |
| `Math.min()` | Returns the smallest of the given numbers. | `Math.min(1, 5, 3, 9)` → `1` |
| `Math.max()` | Returns the largest of the given numbers. | `Math.max(1, 5, 3, 9)` → `9` |
| `Math.ceil()` | Always rounds up to the next integer. | `Math.ceil(4.3)` → `5` |
| `Math.floor()` | Always rounds down to the previous integer. | `Math.floor(4.7)` → `4` |
| `Math.round()` | Rounds to the nearest integer. From `.5` upwards, rounds up. | `Math.round(4.5)` → `5` |
| `Math.trunc()` | Removes the decimal part without rounding. | `Math.trunc(2.9)` → `2` |
| `Math.sqrt()` | Calculates the square root. | `Math.sqrt(81)` → `9` |
| `Math.cbrt()` | Calculates the cube root. | `Math.cbrt(27)` → `3` |
| `Math.abs()` | Returns the absolute value — the distance from zero, without a negative sign. | `Math.abs(-5)` → `5` |
| `Math.pow()` | Raises the first number to the power of the second. | `Math.pow(2, 3)` → `8` |

```js
console.log(Math.round(2.3)); // 2
console.log(Math.round(4.5)); // 5
console.log(Math.round(4.8)); // 5

console.log(Math.trunc(2.9)); // 2
console.log(Math.trunc(9.1)); // 9

console.log(Math.abs(-5));    // 5
console.log(Math.abs(5));     // 5

console.log(Math.pow(2, 3));  // 8
console.log(2 ** 3);          // 8 — equivalent form
```

> ⚠️ **Careful — ceil, floor and trunc with negative numbers:** with positive numbers, `Math.floor()` and `Math.trunc()` give the same result. With negatives they don't: `Math.floor(-4.7)` gives `-5` (goes down), while `Math.trunc(-4.7)` gives `-4` (only cuts the decimal part).

## 9. Generating a random integer in a range

On its own, `Math.random()` only returns decimals between 0 and 1. To get an integer inside a range, combine it with `Math.floor()`.

```js
const min = 5;
const max = 10;
const number = Math.floor(Math.random() * (max - min + 1)) + min;
console.log(number); // Between 5 and 10, both included
```

> **Technical note — why the `+ 1`:** since `Math.random()` never quite reaches 1, the range `max - min` would always stay one value below the maximum. The `+ 1` widens the range just enough for `max` to be able to come out. The `+ min` at the end shifts the result so it starts at the intended minimum.

## 10. Table — &&, || and ??

After `!`, which inverts a single boolean, come the operators that **combine** conditions and produce `true` or `false`. They're the ones that generate the value an `if` structure will then evaluate — which is why they come first in the study order.

| Operator | What it does | Example |
|---|---|---|
| `&&` AND | Both conditions must be `true`. If one is `false`, the code doesn't run. | `true && true` → runs |
| `\|\|` OR | Just one of the conditions needs to be `true`. Only `false` when both are `false`. | `false \|\| true` → runs |
| `??` Nullish Coalescing | Uses the second value only when the first is `null` or `undefined`. | `null ?? "Marco"` → `"Marco"` |

```js
const age = 25;
const hasLicense = true;

if (age >= 18 && hasLicense) {
  console.log("You can drive");
}
// true && true → runs
// Output: You can drive
```

```js
const age = 16;
const hasPermission = true;

if (age >= 18 || hasPermission) {
  console.log("You can enter");
}
// false || true → runs
// Output: You can enter
```

```js
const chosenName = null;
const defaultName = "Marco";
const name = chosenName ?? defaultName;
console.log(name); // "Marco"
```

> **General rule:** `&&` requires every condition to be true, `||` requires only one, and `??` looks for a fallback value for `null` or `undefined`.

## 11. Truth tables

The fastest way to lock in the behaviour of the two operators is to see every possible combination at once.

```
  A       B       A && B    A || B
 ─────────────────────────────────────
  true    true    true      true
  true    false   false     true
  false   true    false     true
  false   false   false     false
                    ▲         ▲
                    │         └─ only one FALSE out of four
                    └─────────── only one TRUE out of four
```

> **Memory trick:** `&&` is demanding — it needs both. `||` is generous — one is enough. `??` is absent-minded — it only wakes up for `null` and `undefined`.

> **Technical note — `??` is not the same as `||`:** `||` replaces any value considered falsy, including `0` and `""`. `??` only replaces `null` and `undefined`. With `const total = 0;`, `total || 10` gives `10`, but `total ?? 10` gives `0` — which is usually what you actually want.

## 12. Table — if, else if and else

Conditional structures decide which block of code runs, depending on whether the conditions come out `true` or `false`.

| Structure | What it does | Example |
|---|---|---|
| `if` | Tests the first condition. If it's `true`, runs the code and skips the rest. | `if (age >= 35) { ... }` |
| `else if` | Only checked when the previous `if` was `false`. There can be more than one. | `} else if (age >= 30) { ... }` |
| `else` | Runs when every previous condition was `false`. Takes no condition. | `} else { ... }` |

```js
const age = 40;

if (age >= 35) {                        // true
  console.log("Age is 35 or more");
}
// Output: Age is 35 or more
```

```js
const age = 32;

if (age >= 35) {                        // false
  console.log("Age is 35 or more");
} else if (age >= 30) {                 // true
  console.log("Age is 30 or more");
}
// Output: Age is 30 or more
```

```js
const age = 25;

if (age >= 30) {                        // false
  console.log("Age is 30 or more");
} else {
  console.log("Age is less than 30");
}
// Output: Age is less than 30
```

> ⚠️ **Common mistake — commenting the wrong line:** the `true` or `false` belongs to the **condition**, not to the `console.log` line. Writing `console.log("...") // false` suggests that line produced `false` — when in reality it never even ran. The correct comment goes on the `if` line.

## 13. Full commented example

A chain with `if`, `else if` and `else`, with the comments placed on the condition — which is where the `true`/`false` actually happens.

```js
const age = 25;

if (age >= 35) {          // false → skipped
  console.log("I have permission to drive");
} else if (age >= 30) {   // false → skipped
  console.log("I have permission to drive");
} else {                  // none was true → runs
  console.log("I am less than 30 years old");
}
```

```
Console output:
I am less than 30 years old
```

> **General rule:** JavaScript checks from top to bottom and stops at the first condition that's `true`. All the remaining ones are ignored, even if they would also be true.

## 14. Cross-cutting rules

1. **The number must be at the start** — `parseInt()` and `parseFloat()` read from the beginning of the string. If the first character isn't part of a number (ignoring spaces), the result is `NaN`.
2. **NaN isn't equal to anything** — `NaN === NaN` gives `false`. To detect it, use `Number.isNaN()`, which checks the value without trying to convert it.
3. **Math is an object, you don't create it** — `Math` already exists in JavaScript. Its methods are called directly (`Math.floor(4.7)`) — you never write `new Math()`.
4. **First produce, then decide** — logical operators produce `true` or `false`; the `if` consumes that value. A condition like `age >= 18 && hasLicense` is resolved first, and only the final result reaches the `if`.
5. **The chain stops at the first true** — in an `if` / `else if` / `else` chain, as soon as one condition is `true` its block runs and all the rest are ignored. The order of the conditions matters.

## 15. Quick recap

### Conversion and checking
| Function | What it does | Example |
|---|---|---|
| `parseFloat()` | Reads the number with decimals | `parseFloat("3.95.8")` → `3.95` |
| `parseInt()` | Reads only the integer part | `parseInt("45.5")` → `45` |
| `isNaN()` | Converts, then checks | `isNaN("abc")` → `true` |
| `Number.isNaN()` | Checks without converting | `Number.isNaN(NaN)` → `true` |

### Math object
| Method | What it does | Example |
|---|---|---|
| `Math.random()` | Decimal between 0 and 1 | `Math.random()` → `0.426` |
| `Math.min()` | The smallest value | `Math.min(1,5,3,9)` → `1` |
| `Math.max()` | The largest value | `Math.max(1,5,3,9)` → `9` |
| `Math.ceil()` | Rounds up | `Math.ceil(4.3)` → `5` |
| `Math.floor()` | Rounds down | `Math.floor(4.7)` → `4` |
| `Math.round()` | To the nearest integer | `Math.round(4.5)` → `5` |
| `Math.trunc()` | Cuts the decimal part | `Math.trunc(2.9)` → `2` |
| `Math.sqrt()` | Square root | `Math.sqrt(81)` → `9` |
| `Math.cbrt()` | Cube root | `Math.cbrt(27)` → `3` |
| `Math.abs()` | Absolute value | `Math.abs(-5)` → `5` |
| `Math.pow()` | Power | `Math.pow(2,3)` → `8` |

### Logical operators and conditionals
| Element | What it does | Example |
|---|---|---|
| `&&` | `true` only if both are `true` | `true && false` → `false` |
| `\|\|` | `true` if at least one is `true` | `false \|\| true` → `true` |
| `??` | Fallback for `null`/`undefined` | `null ?? "Marco"` → `"Marco"` |
| `if` | Tests the first condition | `if (age >= 35) { ... }` |
| `else if` | Only if the previous was `false` | `} else if (age >= 30) { ... }` |
| `else` | When none was `true` | `} else { ... }` |
