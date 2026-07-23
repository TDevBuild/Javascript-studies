# JavaScript — switch, null & undefined

> Complete study log — the `switch` control structure as an organised alternative to `if` / `else`, and the behaviour of `null` and `undefined` in comparisons.
> Study source: freeCodeCamp · July 22

## Table of Contents
1. [What is switch](#1-what-is-switch)
2. [What each part does](#2-what-each-part-does)
3. [break and the fall-through effect](#3-break-and-the-fall-through-effect)
4. [switch vs if / else](#4-switch-vs-if--else)
5. [What each one means](#5-what-each-one-means)
6. [Comparing null with undefined](#6-comparing-null-with-undefined)
7. [null with numbers — the confusing part](#7-null-with-numbers--the-confusing-part)
8. [undefined with numbers](#8-undefined-with-numbers)
9. [Cross-cutting rules](#9-cross-cutting-rules)
10. [Quick recap](#10-quick-recap)

---

## 1. What is switch

`switch` is a control structure, just like `if` / `else if` / `else`. It's especially useful when we want to compare a variable or expression against several possible values.

```js
let day = 3;

switch (day) {
  case 1:
    console.log("Monday");
    break;
  case 2:
    console.log("Tuesday");
    break;
  case 3:
    console.log("Wednesday");
    break;
  default:
    console.log("Invalid day");
}
```

```
What JavaScript checks:
day = 3

  is day 1 ?  ✗ no match → moves to the next
  is day 2 ?  ✗ no match → moves to the next
  is day 3 ?  ✓ MATCH → runs this block
                 ▲
                 └─ and the break exits the switch
```

```
Console output:
Wednesday
```

## 2. What each part does

| Part | What it does |
|---|---|
| `switch (day)` | States the value we want to check. It's evaluated once and compared against each `case`. |
| `case 1:` `case 2:` `case 3:` | The different possible values. Each `case` holds the block of code to run if there's a match. |
| `break;` | Exits the `switch` as soon as the correct block finishes. Without it, execution carries on through the following cases. |
| `default:` | Runs when no `case` matches. Works like the final `else`. It's optional. |

> **Technical note — the comparison is strict:** `switch` compares with `===`, not `==`. So the type counts too: if `day` were the string `"3"`, the `case 3` (a number) wouldn't match and execution would fall through to `default`.

## 3. break and the fall-through effect

`break` tells JavaScript: "you found the right case, now leave the `switch`".

```js
case 3:
  console.log("Wednesday");
  break; // ← exits here
```

Without `break`, once a case matches, execution carries on through the following cases even though their values don't match. This is called **fall-through**.

```
What happens without break:
day = 2

WITH break                WITHOUT break
─────────────────         ─────────────────
case 1  ✗                 case 1  ✗
case 2  ✓ → "Tuesday"     case 2  ✓ → "Tuesday"
        └─ EXITS                  │ continues ↓
                          case 3    → "Wednesday"
                                   │ continues ↓
                          default   → "Invalid day"

console: Tuesday          console: Tuesday
                                   Wednesday
                                   Invalid day
```

> ⚠️ **Common mistake — forgetting the break:** forgetting `break` throws no error and no warning — the code still runs, it just executes extra blocks. It's one of the hardest slips to spot, because the first printed result is correct and only the following ones are surplus.

> **Tip — the last block:** in `default` (or in the last `case`) the `break` is unnecessary, since there's nothing after it. Many programmers write it anyway, so they don't forget it when they add another `case` underneath.

## 4. switch vs if / else

| Structure | When to use it |
|---|---|
| `switch` | Very useful for comparing one value against several fixed options. It reads more clearly and stays more organised than a long `else if` chain. |
| `if` / `else` | More flexible for complex conditions — ranges, combinations with `&&` and `\|\|`, or comparisons between different variables. |

```js
// A case only if can handle
if (age >= 18 && hasLicense === true) {
  console.log("Can drive");
}
```

> **Main idea:** `switch` is an organised alternative to `if` / `else` when we're checking several possibilities **for the same value**. If the conditions involve ranges or multiple variables, `if` / `else` is the way to go.

## 5. What each one means

`null` and `undefined` both represent "absence of a value", but for different reasons.

| Value | What it means |
|---|---|
| `null` | Represents an **intentional** absence of value. Someone decided to put "empty" there. |
| `undefined` | Usually means a value hasn't been assigned yet. It wasn't a decision — nobody simply filled it in. |

> **Memory trick:** `null` is left empty **on purpose**. `undefined` is **forgotten**. The first is a choice, the second is the default state.

## 6. Comparing null with undefined

```js
console.log(null == undefined);  // true
console.log(null === undefined); // false
```

| Operator | Why |
|---|---|
| `==` loose equality | JavaScript treats `null` and `undefined` as equivalent. It's a rule of the language itself: they're the only two values considered equal to each other with `==`. |
| `===` strict equality | Also compares the type. Since `null` and `undefined` are different types, the result is `false`. |

> **Technical note — the rule is exclusive:** with `==`, `null` is only equal to `undefined` and to itself. It isn't equal to `0`, nor to `false`, nor to `""`. The same goes for `undefined`.

## 7. null with numbers — the confusing part

```js
console.log(null == 0); // false
console.log(null > 0);  // false
console.log(null >= 0); // true  ← the odd one
```

At first glance this is contradictory: if `null` isn't equal to `0` and isn't greater than `0`, how can it be greater **or equal** to `0`?

> **The explanation — these are two different rules:** `==` and the relational operators (`>`, `<`, `>=`, `<=`) follow different rules. `==` applies the exclusive rule from the previous section and never converts `null` to a number. The relational operators do convert `null` to `0`.

```
The two rules side by side:

null == 0  → == rule           → null is only equal to undefined
                               → FALSE (no conversion)

null >= 0  → relational rule   → null converts to 0
                               → 0 >= 0
                               → TRUE

null > 0   → relational rule   → null converts to 0
                               → 0 > 0
                               → FALSE
```

```
Console output:
false
false
true
```

## 8. undefined with numbers

With `undefined` there are no surprises: every numeric comparison returns `false`.

```js
console.log(undefined > 0);  // false
console.log(undefined < 0);  // false
console.log(undefined == 0); // false
console.log(undefined >= 0); // false
```

The reason, however, isn't the same on every line.

| Comparison | Why it's false |
|---|---|
| `undefined > 0` · `undefined < 0` · `undefined >= 0` | In the relational operators, `undefined` converts to `NaN`. Any comparison with `NaN` is always `false`. |
| `undefined == 0` | Here there's no conversion at all. The `==` rule applies: `undefined` is only equal to `null` and to itself. |

> ⚠️ **Careful — it isn't all NaN:** it's tempting to say "`undefined` turns into `NaN` in comparisons". That's only true for `>`, `<`, `>=` and `<=`. With `==` there's no conversion — the result is `false` for a different reason. The four results coincide; the reasons don't.

> **Technical note — what NaN is:** `NaN` stands for *Not a Number* and represents an impossible numeric result. It has one quirk: it isn't equal to anything, not even to itself — `NaN === NaN` gives `false`.

## 9. Cross-cutting rules

1. **switch compares with `===`** — case matching is always strict: the value **and** the type have to line up. A `case 3` never catches the string `"3"`.
2. **Without break, execution continues** — once a `case` matches, JavaScript runs everything that follows until it hits a `break` or the end of the `switch` — including `default`.
3. **`==` and the relational operators are separate rules** — `==` never converts `null` or `undefined` to a number. The operators `>`, `<`, `>=` and `<=` always do. That's where `null >= 0` being `true` while `null == 0` is `false` comes from.
4. **null becomes 0, undefined becomes NaN** — in the numeric conversions performed by the relational operators, `null` becomes `0` (a usable number) and `undefined` becomes `NaN` (which invalidates any comparison).

## 10. Quick recap

### Parts of a switch
| Part | Function | Required? |
|---|---|---|
| `switch (x)` | The value to check | Yes |
| `case` | One possible value | Yes (at least one) |
| `break` | Exits the switch | No, but almost always needed |
| `default` | When no `case` matches | No |

### Comparisons between null and undefined
| Comparison | Result | Why |
|---|---|---|
| `null == undefined` | `true` | A rule of `==` itself |
| `null === undefined` | `false` | Different types |

### Comparisons with numbers
| Comparison | Result | Why |
|---|---|---|
| `null == 0` | `false` | No conversion |
| `null > 0` | `false` | `0 > 0` |
| `null >= 0` | `true` | `0 >= 0` |
| `undefined > 0` | `false` | Becomes `NaN` |
| `undefined < 0` | `false` | Becomes `NaN` |
| `undefined >= 0` | `false` | Becomes `NaN` |
| `undefined == 0` | `false` | No conversion |

> **The sentence to keep:** `null == undefined` is `true`, `null === undefined` is `false`. And in relational comparisons, `null` converts to `0` while `undefined` converts to `NaN`.
