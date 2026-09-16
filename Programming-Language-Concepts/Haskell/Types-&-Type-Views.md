---
title: Types & Type Views
date: 2026-09-03
course: Programming Language Concepts
tags: [haskell, types]
related:
  - "[[Haskell-MOC]]"
  - "[[Haskell-Language-Overview]]"
  - "[[Data-Types-&-Values]]"
---

# Types & Type Views

## How Haskell Programs are Structured

- **Types structure values** — every value belongs to exactly one type.
- **Types structure expressions**:
	- An expression has a type if it reduces to a value of that type.
	- Every expression belongs to exactly one most general type.

**Summary:** In Haskell, every value and every expression belongs to exactly one (most general) type.

## Two Views of Types

- **Types as classifiers (extrinsic)**
	- The meaning of programs is independent of their typing.
	- Types describe program behavior.
	- Example languages: Python, C.
- **Types as structure (intrinsic)**
	- Programs have no meaning outside of typing.
	- Types prescribe program behavior.

**Summary:** Types can either just *describe* behavior after the fact (extrinsic, e.g. Python/C) or *prescribe* it as part of the program's meaning (intrinsic).

## Key Terms

|Term|Definition|
|---|---|
|**Types as classifiers (extrinsic)**|Typing that describes behavior without being part of a program's meaning (e.g. Python, C).|
|**Types as structure (intrinsic)**|Typing that prescribes behavior; the program has no meaning outside its typing.|
