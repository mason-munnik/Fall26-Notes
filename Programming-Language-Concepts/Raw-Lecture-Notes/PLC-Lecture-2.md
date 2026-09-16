## What is Haskell About?

Functional Language
- Haskell is a language of expressions, not commands
- Meaning of a Haskell program is given by evaluation, not execution
- Functions are first-class values 
	- (functions can use functions as parameters or return values)

Pure
- Result of a function depends only on its input
- Side-effects (i/o, randomness, &c) explicitly captured

Non-strict
- Expressions are only evaluated when needed

Strongly Typed
- Types are the foundation of understanding Haskell programs
- Types automatically calcuatled by the compiler
- "generic" types enable reuse, overloading

## What do Haskell Programs Look Like?

A Haskell file is a list of definitions
- evaluation not execution starts with main, or with an expression we provide
Each definition contains:
- A type signature (optional)
- A list of equations (not optional)
