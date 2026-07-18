# JavaScript Fundamentals — Numbers, Operators & Conditionals

> Compilation of study logs: the `number` type and arithmetic, type coercion, compound assignment, increment/decrement, operator precedence, comparisons, and the first decision structure: `if`.
> Study source: freeCodeCamp · July 10–15

## Table of Contents

**Module 1 — Number, Arithmetic & Type Coercion**
1. [The number type](#11-the-number-type)
2. [Numeral systems](#12-numeral-systems)
3. [Infinity](#13-infinity)
4. [NaN](#14-nan)
5. [The six arithmetic operators](#15-the-six-arithmetic-operators)
6. [Order of operations](#16-order-of-operations)
7. [Type Coercion](#17-what-is-type-coercion)
8. [The + operator — the special case](#18-the--operator--the-special-case)
9. [The other operators](#19-the-other-operators)
10. [Full conversion table](#110-full-conversion-table)

**Module 2 — Operators**
1. [Compound assignment](#21-what-is-compound-assignment)
2. [Compound arithmetic operators](#22-compound-arithmetic-operators)
3. [Bitwise compound operators (&= and |=)](#23-bitwise-compound-operators)
4. [Increment (++) and decrement (--)](#24-increment-and-decrement)
5. [Prefix vs Postfix](#25-prefix-vs-postfix)
6. [Operator precedence](#26-operator-precedence)
7. [Associativity](#27-associativity)

**Module 3 — Comparison, Equality & if**
1. [Comparison operators](#31-comparison-operators)
2. [Equality: == vs ===](#32-equality--vs-)
3. [Inequality: != vs !==](#33-inequality--vs-)
4. [The if structure](#34-the-if-structure)
5. [The if/else structure](#35-the-ifelse-structure)

---

# Module 1 — Number, Arithmetic & Type Coercion

## 1.1 The number type

JavaScript has only one type for numbers: `number`. There are no separate types for integers and decimals — both belong to the same type.

```js
console.log(typeof 10);   // "number" (integer)
console.log(typeof 3.18); // "number" (decimal)
console.log(typeof -30);  // "number" (negative)
```

## 1.2 Numeral systems

JavaScript lets you write the same number in four different systems. All of them are of type `number`, and the console always shows them converted to decimal.

| System | Base | Allowed digits | How to write | Decimal value |
|---|---|---|---|---|
| Decimal | 10 | 0–9 | `10` | 10 |
| Binary | 2 | 0 and 1 | `0b1010` | 10 |
| Octal | 8 | 0–7 | `0o12` | 10 |
| Hexadecimal | 16 | 0–9 and A–F | `0xA` | 10 |

```js
console.log(10);            // 10 (decimal)
console.log(0b1010);        // 10 (binary)
console.log(0o12);          // 10 (octal)
console.log(0xA);           // 10 (hexadecimal)
console.log(typeof 0b1010); // "number"
```

> **Technical note — prefixes:** the prefix tells JavaScript which base to read the number in: `0b` → binary · `0o` → octal · `0x` → hexadecimal. Digits must respect the base: `0b1012` throws an error (binary only accepts 0 and 1); `0o19` too (octal only goes up to 7).

## 1.3 Infinity

`Infinity` represents an infinite numeric value. It happens when a result exceeds what JavaScript can represent — or, most commonly, when you divide by zero.

```js
const infiniteNumber = 1 / 0;
console.log(infiniteNumber);        // Infinity
console.log(typeof infiniteNumber); // "number"
console.log(-1 / 0);                // -Infinity
```

> `Infinity` is a value of type `number`, not an error. In math, dividing by zero is undefined; in JavaScript, it returns `Infinity`.

## 1.4 NaN

`NaN` means **Not a Number**. It appears when a mathematical operation cannot produce a valid number.

```js
console.log('abc' - 5);  // NaN
console.log(0 / 0);      // NaN
console.log(typeof NaN); // "number"
```

> **The NaN paradox:** `typeof NaN` returns `"number"`. It seems contradictory, but `NaN` is a special value *inside* the number type that represents "the result of a failed numeric operation".

## 1.5 The six arithmetic operators

| Operation | Operator | Example | Result |
|---|---|---|---|
| Addition | `+` | `5 + 2` | `7` |
| Subtraction | `-` | `5 - 2` | `3` |
| Multiplication | `*` | `5 * 2` | `10` |
| Division | `/` | `10 / 2` | `5` |
| Remainder | `%` | `9 % 2` | `1` |
| Exponentiation | `**` | `2 ** 3` | `8` |

### Remainder (%) — how it works

`%` doesn't give the result of the division. It gives **what's left** after the integer division:

```
9 % 2
How many times does 2 fit entirely into 9? → 4 times
2 × 4 = 8
9 − 8 = 1 ← this is the remainder
Result: 1
```

## 1.6 Order of operations

JavaScript follows math rules: `**` first, then `*`, `/`, `%`, and only at the end `+` and `-`. Parentheses `( )` change the order and run first.

```js
const result = 10 + 5 * 2 - 8 / 4;
console.log(result); // 18
// 5 * 2 = 10  ← multiplication first
// 8 / 4 = 2   ← division first
// 10 + 10 - 2 = 18
```

> **Tip:** with parentheses you can force another order: `(10 + 5) * 2` → `30`. In real code, use parentheses whenever the order isn't obvious.

## 1.7 What is Type Coercion

Type Coercion is the **automatic conversion** JavaScript performs from one data type to another, without you asking. It mainly happens when you mix types in one operation — e.g. a `number` with a `string`.

> **The rule that separates everything:** the `+` operator behaves differently from all the others. With `+`, JavaScript prefers to **join text**. With `-`, `*`, `/`, `%`, and `**`, JavaScript tries to **convert to number**.

## 1.8 The + operator — the special case

When you use `+` and one of the values is a string, JavaScript doesn't add. It **concatenates**:

```js
console.log(5 + '10'); // "510"
// 5 + '10' → "5" + "10" → "510"
```

The final type is `string`, not `number`.

## 1.9 The other operators

With `-`, `*`, `/`, `%`, or `**` and a numeric string, JavaScript converts the string to a number:

```js
console.log('10' - 5); // 5
console.log('10' * 2); // 20
console.log('20' / 2); // 10
console.log('9' % 2);  // 1
console.log('2' ** 3); // 8
```

## 1.10 Full conversion table

| Value | In math operations |
|---|---|
| `true` | becomes `1` |
| `false` | becomes `0` |
| `null` | becomes `0` |
| `undefined` | becomes `NaN` |
| `'abc'` | becomes `NaN` (not numeric) |
| `'10'` | becomes `10` (numeric string) |

```js
console.log('abc' - 5);      // NaN
console.log(true + 1);       // 2
console.log(false + 1);      // 1
console.log('Hello' + true); // "Hellotrue"
console.log(null + 5);       // 5
console.log(undefined + 5);  // NaN
```

**Cross-cutting rules:**
1. **The operator decides everything** — the same pair of values gives different results depending on the operator: `5 + '10'` = `"510"` (string) but `5 - '10'` = `-5` (number).
2. **NaN is of type number** — whenever a math operation fails, the result is `NaN`.
3. **One string is enough for + to join text** — with `+`, if at least one value is a string, the result is always a string.

---

# Module 2 — Operators

## 2.1 What is compound assignment

A compound assignment operator does two things at once: performs an operation **and** stores the result in the same variable.

```js
x += y;  // short form of: x = x + y;
```

> **Technical note:** the variable must already exist and have a value. You can't do `let total += 5;` — first create it (`let total = 10;`), then use `total += 5;`. Since the value changes, the variable must be declared with `let`, never `const`.

## 2.2 Compound arithmetic operators

| Operator | Equivalent to | Example |
|---|---|---|
| `+=` | `x = x + y` | `total += 5` |
| `-=` | `x = x - y` | `score -= 7` |
| `*=` | `x = x * y` | `points *= 3` |
| `/=` | `x = x / y` | `balance /= 4` |
| `%=` | `x = x % y` | `num %= 3` |
| `**=` | `x = x ** y` | `num **= 3` |

```js
let total = 10;
total += 5;
console.log(total); // 15

let balance = 100;
balance /= 4;
console.log(balance); // 25
```

## 2.3 Bitwise compound operators

`&=` and `|=` work with numbers in **binary**. Each number is broken into positions worth `32 16 8 4 2 1`. A `1` means that value counts; a `0` means it doesn't.

```
Values:  32 16 8 4 2 1
6  →      0  0 0 1 1 0   uses 4 and 2 (4 + 2 = 6)
3  →      0  0 0 0 1 1   uses 2 and 1 (2 + 1 = 3)

6 & 3 →   0  0 0 0 1 0   only what's in BOTH → 2
6 | 3 →   0  0 0 1 1 1   everything in EITHER → 7
```

```js
let num = 6;
num &= 3;
console.log(num); // 2

let other = 6;
other |= 3;
console.log(other); // 7
```

> **Memory trick:** `&` (AND) is demanding — only accepts what exists in both. `|` (OR) is generous — accepts anything that exists in at least one.

## 2.4 Increment and decrement

| Operator | Meaning |
|---|---|
| `x++` | equivalent to `x = x + 1` |
| `x--` | equivalent to `x = x - 1` |

## 2.5 Prefix vs Postfix

The position of `++` (or `--`) changes **which value is returned at that moment**:

```js
let x = 5;
console.log(++x); // 6  (prefix: increases FIRST, then uses the new value)
console.log(x);   // 6

let y = 5;
console.log(y++); // 5  (postfix: uses the current value FIRST, then increases)
console.log(y);   // 6
```

The difference becomes visible in an assignment:

```js
let a = 5;
let b = ++a;
console.log(a); // 6
console.log(b); // 6  ← a and b end up EQUAL

let c = 5;
let d = c++;
console.log(c); // 6
console.log(d); // 5  ← c and d end up DIFFERENT
```

> **Key point:** in both cases the variable ends up changed. The position only decides the returned value: prefix → new value · postfix → old value.

## 2.6 Operator precedence

| Order | Rule | Example |
|---|---|---|
| 1 | Parentheses `( )` run first | `(2 + 3) * 4` → `20` |
| 2 | Exponentiation `**` (right → left when chained) | `2 ** 3 ** 2` → `2 ** 9` = `512` |
| 3 | `*` `/` `%` before addition/subtraction | `2 + 3 * 4` → `14` |
| 4 | `+` `-` last | `10 - 2 + 3` → `11` |
| 5 | Same priority → left to right | `12 / 3 * 2` → `8` |
| 6 | Assignment `=` → right to left | `a = b = 5` |

## 2.7 Associativity

The rule that decides the **direction** of the calculation when operators have the same priority:

| Direction | Operators | Example |
|---|---|---|
| Left → right | `+ - * / %` | `12 / 3 * 2` → `(12 / 3) * 2` = `8` |
| Right → left | `**` · `=` `+=` `-=` … | `2 ** 3 ** 2` → `2 ** (3 ** 2)` = `512` |

> **Watch out — exponentiation is the exception:** `2 ** 3 ** 2` gives `512` (it's `2 ** 9`), not `64` (which would be `8 ** 2`). Want the other order? Use parentheses: `(2 ** 3) ** 2`.
>
> **Tip:** you don't need to memorize the whole table. When in doubt, use parentheses — they make the intention explicit and the code easier to read.

---

# Module 3 — Comparison, Equality & if

## 3.1 Comparison operators

A comparison operator checks the relationship between two values and **always returns a boolean**: `true` or `false`.

| Operator | Meaning | Example |
|---|---|---|
| `>` | Greater than | `9 > 6` → `true` |
| `>=` | Greater or equal | `6 >= 6` → `true` |
| `<` | Less than | `6 < 9` → `true` |
| `<=` | Less or equal | `6 <= 6` → `true` |

```js
let a = 6;
let b = 9;
console.log(a > b);  // false
console.log(a < b);  // true
console.log(a >= 6); // true
```

## 3.2 Equality: == vs ===

| Operator | Compares | Type conversion |
|---|---|---|
| `==` loose equality | Whether the **values** are equal | Allows automatic conversion before comparing |
| `===` strict equality | Whether the value **AND** the type are equal | No conversion. Different types → immediately `false` |

```js
// == (with conversion)
console.log(5 == "5"); // true  ("5" is converted to 5)
console.log(4 == "5"); // false

// === (strict, no conversion)
console.log(4 === 4);   // true
console.log(4 === "4"); // false (same value, different types)
```

> **The detail that matters:** `4 == "4"` is `true`, but `4 === "4"` is `false`. The value is the same; what changes is whether the type counts.

## 3.3 Inequality: != vs !==

The mirror of equality. The exclamation mark `!` means "not".

```js
// != (with conversion)
console.log(4 != "5"); // true
console.log(5 != "5"); // false ("5" becomes 5 → equal → not different)

// !== (strict)
console.log(4 !== 4);   // false
console.log(4 !== "4"); // true (different types → different)
```

> **Practical tip:** when in doubt, always use `===` and `!==`. Comparing value and type at the same time avoids surprises caused by automatic conversion.

## 3.4 The if structure

`if` runs a block of code **only if** a condition is `true`. If it's `false`, the block is skipped.

```js
if (condition) {
  // code that runs if true
}
```

```js
const hasDeveloperJob = true;

if (hasDeveloperJob) {
  console.log("Has a job as a developer.");
}
// → Has a job as a developer.
```

## 3.5 The if/else structure

`if/else` gives two paths: `if` runs when the condition is `true`; `else` runs when it's `false`. **Exactly one of the two always runs.**

```js
const age = 10;

if (age >= 16) {
  console.log("Can drive.");
} else {
  console.log("Cannot drive.");
}
// → Cannot drive.
```

```
age = 10
age >= 16 ?
 ├── true  → "Can drive."     (skipped)
 └── false → "Cannot drive."  ← this one runs
```

**Cross-cutting rules:**
1. **Comparisons always return a boolean** — that boolean is what `if` uses to decide.
2. **Three characters = type counts** — `==` and `!=` convert before comparing; `===` and `!==` don't. More characters = more strict.
3. **if only runs on true** — with `if/else`, exactly one of the two blocks always runs.
