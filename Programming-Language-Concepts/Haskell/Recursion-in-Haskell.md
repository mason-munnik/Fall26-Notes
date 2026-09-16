---
title: Recursion in Haskell
date: 2026-09-10
course: Programming Language Concepts
tags: [haskell, recursion]
related:
  - "[[Haskell-MOC]]"
  - "[[Recursive-Data-Types]]"
---

# Recursion in Haskell

## Recursion

> "Recursion is about self-similarity."

Recursion is expressed in Haskell by self-referential definitions:

```Haskell
fact n
	n <= 1 = 1
	otherwise = n * fact (n - 1)
```

Evaluating `fact 1`:

```
fact 1
= let n = 1 in 1
= 1
```

Evaluating `fact 3`:

```
fact 3
= let n = 3 in n * fact (n - 1)
= 3 * fact (3 - 1)
= 3 * fact 2
= 3 * (let n = 2 in n * fact (n - 1))
= 3 * (2 * fact (2 - 1))
...
```

**Summary:** Recursive functions in Haskell are self-referential definitions; evaluating a call substitutes the argument and unfolds the definition until a base case is reached.

## Key Terms

|Term|Definition|
|---|---|
|**Recursion**|Self-similarity; in Haskell, expressed through self-referential definitions.|
|**Base case**|The non-recursive equation that stops the unfolding (e.g. `n <= 1 = 1`).|
