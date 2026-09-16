---
title: Haskell Language Overview
date: 2026-08-27
course: Programming Language Concepts
tags: [haskell, functional-programming]
related:
  - "[[Haskell MOC]]"
  - "[[Types & Type Views]]"
---

# Haskell Language Overview

## What is Haskell About?

- **Functional** — Haskell is a language of expressions, not commands.
	- The meaning of a Haskell program is given by evaluation, not execution.
	- Functions are first-class values (they can be used as parameters or return values).
- **Pure** — the result of a function depends only on its input.
	- Side effects (I/O, randomness, etc.) are explicitly captured.
- **Non-strict** — expressions are only evaluated when needed.
- **Strongly typed** — types are the foundation of understanding Haskell programs.
	- Types are automatically calculated by the compiler.
	- "Generic" types enable reuse and overloading.

**Summary:** Haskell is a pure, non-strict, strongly typed functional language — programs are evaluated as expressions rather than executed as commands.

## What do Haskell Programs Look Like?

- A Haskell file is a list of definitions.
	- Evaluation (not execution) starts with `main`, or with an expression the user provides.
- Each definition contains:
	- A type signature (optional)
	- A list of equations (not optional)

**Summary:** A Haskell file is a list of definitions, each with an optional type signature and a required list of equations.

## Key Terms

|Term|Definition|
|---|---|
|**Functional**|Haskell is a language of expressions; meaning comes from evaluation, not execution.|
|**Pure**|A function's result depends only on its input; side effects are explicit.|
|**Non-strict**|Expressions are evaluated only when needed.|
|**Definition**|A named piece of a Haskell file: an optional type signature plus a required list of equations.|
