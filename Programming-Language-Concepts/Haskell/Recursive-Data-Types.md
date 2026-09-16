---
title: Recursive Data Types
date: 2026-09-10
course: Programming Language Concepts
tags: [haskell, recursive-types, data-types]
related:
  - "[[Haskell-MOC]]"
  - "[[Recursion-in-Haskell]]"
  - "[[Data-Types-&-Values]]"
---

# Recursive Data Types

## Types Can Also Be Recursive

The structure of data is frequently self-referential:

- A natural number is either 0 or the successor of a natural: `data Nat = Zero | Succ Nat`
- A list is either empty or a first value followed by a list: `data List a = Nil | Cons a (List a)`
- A tree is either a leaf or branches to two trees: `data Tree a = Leaf a | Branch (Tree a) (Tree a)`

Recursion in types implies recursion in terms:

```Haskell
data List a = Nil | Cons a (List a)

someInts = Cons 1 (Cons 2 Nil)

sum :: List Int -> Int
sum Nil = 0
sum (Cons x xs) = x + sum xs
```

**Summary:** Recursive types (`Nat`, `List`, `Tree`) are defined in terms of themselves, and functions over them (like `sum`) recurse to match — one equation per alternative.

## Recursion and Efficiency

> Lecture notes cut off here — not yet covered.

## Key Terms

|Term|Definition|
|---|---|
|**Recursive type**|A type defined in terms of itself, e.g. `data List a = Nil \| Cons a (List a)`.|
|**`Nat`**|`data Nat = Zero \| Succ Nat` — a natural number is 0 or the successor of a natural.|
|**`List a`**|`data List a = Nil \| Cons a (List a)` — empty, or a value consed onto a list.|
|**`Tree a`**|`data Tree a = Leaf a \| Branch (Tree a) (Tree a)` — a leaf or two subtrees.|
