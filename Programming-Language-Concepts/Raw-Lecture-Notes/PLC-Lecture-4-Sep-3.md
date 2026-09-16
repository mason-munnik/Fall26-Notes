
## How Haskell Programs are Structured

Types structure values
- Every value belongs to exactly one type
Types structure expressions:
- an expression has a type if it reduces to a value of that type
- every expression belongs to exactly one most general type

## Two Views of Types
- types as classifiers (extrinsic)
	- meaning of programs are independent of their typing
	- types describe program behavior
	- python, C
- types as structure(instrinsic)
	- programs have no meaning outside typing
	- types prescribe program behavior

## New values come from new types
Most types are introduced by data type declarations:

`data Bool = False | True`

- simultaneously introduces new type Bool and values False, True of that type
- remaining types are primitive: functions, pointers, integers

Haskell's data types follow sum of products construction
- alternatives (sum, coproduct): different ways to build values of a type

Read | as "or": a Bool can be either False or True

### Ingredients of a data type

