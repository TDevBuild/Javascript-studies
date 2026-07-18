# JavaScript — Unary & Bitwise Operators

> Complete study log — operators that act on a single value (`+`, `-`, `!`, `~`, `void`, `typeof`) and operators that work directly with the bits of a number.
> Study source: freeCodeCamp · July 18

## Table of Contents
1. [What is a unary operator](#1-what-is-a-unary-operator)
2. [Unary operators table](#2-unary-operators-table)
3. [How to read a number in binary](#3-how-to-read-a-number-in-binary)
4. [& AND, | OR, and ^ XOR](#4--and--or-and--xor)
5. [~ Bitwise NOT](#5--bitwise-not)
6. [<< Left shift](#6--left-shift)
7. [>> Right shift](#7--right-shift)
8. [Cross-cutting rules](#8-cross-cutting-rules)
9. [Quick recap](#9-quick-recap)

---

## 1. What is a unary operator

A **unary** operator acts on a **single value**. That's the difference from binary operators (`+`, `-`, `*` between two values), which need one value on each side.

```
BINARY   5 + 3       two values, one on each side
UNARY    -5          one single value
         !online
         typeof x
```

## 2. Unary operators table

| Operator | What it does | Example |
|---|---|---|
| `+` unary plus | Converts the value to a number. If it's already a number, keeps it. | `+"42"` → `42` |
| `-` unary minus | Converts to number and **inverts the sign**. | `-5` → `-5` · `-(-5)` → `5` |
| `!` logical NOT | Converts to boolean and **inverts it**: `true` → `false`. | `!true` → `false` |
| `~` bitwise NOT | Converts to a 32-bit integer and inverts **all bits**. | `~5` → `-6` |
| `void` | Runs an expression, ignores the result, always returns `undefined`. | `void (2 + 2)` → `undefined` |
| `typeof` | Returns the type of the value as a string. | `typeof "Hi"` → `"string"` |

```js
const text = "42";
const number = +text;
console.log(number);        // 42
console.log(typeof number); // "number"

const online = true;
console.log(!online); // false
```

> **Technical note — unary + vs binary +:** the same symbol does different things depending on position. With one value (`+text`) it converts to number. With two values (`5 + 3`) it adds or joins text. What decides is how many values are involved.

## 3. How to read a number in binary

Bitwise operators work with the number written in **binary**. Each position is worth **double** the one to its right, and you read from left to right, largest to smallest.

```
Values: 128 64 32 16 8 4 2 1
                          ▲
                          └─ smallest position (right)
```

`1` means the position's value **counts** · `0` means it **doesn't**.

```
The number 5:
Values: 8 4 2 1
Bits:   0 1 0 1     uses 4 and 1 → 4 + 1 = 5
Short form: 5 = 101

The number 3:
Values: 8 4 2 1
Bits:   0 0 1 1     uses 2 and 1 → 2 + 1 = 3
Short form: 3 = 011
```

> ⚠️ **Order matters:** positions are always written largest → smallest, left → right (`32 16 8 4 2 1`). Writing `1 2 4 8 16 32` is inverted and leads to reading numbers backwards.

## 4. & AND, | OR, and ^ XOR

These three operators compare the bits **at the same position** of two numbers and produce a new number.

| Operator | Rule | Example (5 and 3) |
|---|---|---|
| `&` AND | Result bit is `1` only when **both** bits are `1` | `5 & 3` → `1` |
| `\|` OR | Result bit is `1` when **at least one** bit is `1` | `5 \| 3` → `7` |
| `^` XOR | Result bit is `1` only when the bits are **different** | `5 ^ 3` → `6` |

```
Values:  4 2 1
5   →    1 0 1
3   →    0 1 1
        ─────────
5 & 3 →  0 0 1   only where BOTH have 1     → 1
5 | 3 →  1 1 1   where AT LEAST ONE has 1   → 7
5 ^ 3 →  1 1 0   only where they DIFFER     → 6
```

```js
const a = 5; // 101
const b = 3; // 011
console.log(a & b); // 1
console.log(a | b); // 7
console.log(a ^ b); // 6
```

> **Memory trick:** `&` is demanding — needs both. `|` is generous — one is enough. `^` is picky — only accepts when they're different.

## 5. ~ Bitwise NOT

`~` inverts **all** bits of the number: each `0` becomes `1` and each `1` becomes `0`.

```
Simplified 8-bit representation:
 5 = 00000101
~5 = 11111010
```

> **The practical rule:** you don't need to do the binary math. The result of `~` always follows this formula:
>
> **`~n = -(n + 1)`**
>
> Example: `~5 = -(5 + 1) = -6`

```js
console.log(~5);  // -6
console.log(~0);  // -1
console.log(~10); // -11
```

## 6. << Left shift

`<<` moves all bits to the **left**. The number after `<<` says how many positions to shift. Zeros come in from the right.

```js
const number = 5;          // 101 in binary
console.log(number << 1);  // 10 (binary 1010)
console.log(number << 2);  // 20 (binary 10100)
```

```
5 << 1 step by step:
Values:  8 4 2 1
Before:  0 1 0 1   → 4 + 1 = 5
After:   1 0 1 0   → 8 + 2 = 10
         ▲
         └─ every bit moved ONE position left,
            and a 0 came in from the right
```

> ⚠️ **Don't confuse binary with decimal:** in `5 << 1`, the binary goes from `101` to `1010`. The decimal value goes from `5` to `10`. `1010` (binary) and `10` (decimal) are the same number in different bases.

> **The practical rule:** each left shift **multiplies by 2**.
> `5 << 1` → 5 × 2 = 10 · `5 << 2` → 5 × 4 = 20 · `5 << 3` → 5 × 8 = 40

## 7. >> Right shift

`>>` moves all bits to the **right**. Bits that fall off the right side are **discarded**.

```js
const number = 5;          // 101 in binary
console.log(number >> 1);  // 2 (binary 10)
console.log(number >> 2);  // 1 (binary 1)
```

```
5 >> 1 step by step:
Values:  4 2 1
Before:  1 0 1   → 4 + 1 = 5
After:   0 1 0   → 2
             ▲
             └─ the last bit (1) fell off the right and was DISCARDED
```

> **The practical rule:** each right shift **divides by 2**, discarding the decimal part.
> `5 >> 1` → 5 ÷ 2 = 2.5 → `2` · `5 >> 2` → 5 ÷ 4 = 1.25 → `1`

> **Technical note — >> preserves the sign:** a negative number stays negative after the shift. There's also a third operator, `>>>`, which shifts right **without** preserving the sign. For positive numbers, `>>` and `>>>` give the same result.

## 8. Cross-cutting rules

1. **Binary position order** — positions are always written largest → smallest, left → right: `32 16 8 4 2 1`.
2. **Bitwise works with 32 bits** — all bitwise operators (`&`, `|`, `^`, `~`, `<<`, `>>`) convert the number to a 32-bit integer before operating. Examples use 3 or 8 bits just for readability.
3. **Unary acts on a single value** — the same symbol can be unary or binary depending on position: `-5` is unary (inverts the sign), `8 - 5` is binary (subtracts).

## 9. Quick recap

### Unary operators
| Operator | Function | Example |
|---|---|---|
| `+` | Converts to number | `+"42"` → `42` |
| `-` | Converts and inverts the sign | `-5` → `-5` |
| `!` | Converts to boolean and inverts | `!true` → `false` |
| `~` | Inverts all bits · `~n = -(n+1)` | `~5` → `-6` |
| `void` | Always returns `undefined` | `void(2+2)` → `undefined` |
| `typeof` | Returns the type as a string | `typeof "Hi"` → `"string"` |

### Bitwise operators
| Operator | Function | Example (5 and 3) |
|---|---|---|
| `&` AND | `1` only if both are `1` | `5 & 3` → `1` |
| `\|` OR | `1` if at least one is `1` | `5 \| 3` → `7` |
| `^` XOR | `1` only if they differ | `5 ^ 3` → `6` |
| `~` NOT | Inverts all bits | `~5` → `-6` |

### Shifts
| Operator | Function | Example |
|---|---|---|
| `<<` | Moves left · multiplies by 2 per position | `5 << 1` → `10` |
| `>>` | Moves right · divides by 2 per position | `5 >> 1` → `2` |
