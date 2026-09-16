---
title: Data Types & Values
date: 2026-09-03
course: Programming Language Concepts
tags: [haskell, data-types]
related:
  - "[[Haskell-MOC]]"
  - "[[Types-&-Type-Views]]"
  - "[[Recursive-Data-Types]]"
---

# Data Types & Values

## New Values Come From New Types

Most types are introduced by data type declarations:

```Haskell
data Bool = False | True
```

- This simultaneously introduces the new type `Bool` and the values `False`, `True` of that type.
- Remaining types are primitive: functions, pointers, integers.
- Haskell's data types follow a **sum of products** construction:
	- Alternatives (sum, coproduct) — different ways to build values of a type.
	- Read `|` as "or": a `Bool` can be either `False` or `True`.

**Summary:** A `data` declaration introduces both a new type and the values that belong to it; alternatives are separated by `|`, read as "or".

### Ingredients of a Data Type

> Lecture notes cut off here — not yet covered.

## Key Terms

|Term|Definition|
|---|---|
|**Data type declaration**|A declaration (`data ... = ...`) that introduces a new type together with its values.|
|**Sum of products**|The construction Haskell's data types follow: a sum (`\|`, alternatives) of products (the arguments bundled into each alternative).|
