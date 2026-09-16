# Programming Language Concepts Lecture Notes 9-10-26

## Recursion - IMPORTANT
"Recursion is about self-similarity"

Recursion is expressed in Haskell by self-referential definitions
```Haskell
fact n
	n <= 1 = 1
	otherwise = n * fact (n - 1)


fact 1
= let n = 1 in 1
= 1


fact 3
= let n = 3 in n * fact (n - 1)
= 3 * fact (3 - 1)
= 3 * fact 2
= 3 * (let n = 2 in n * fact (n - 1))
= 3 * (2 * fact (2 - 1))
.
..
```

### Recursion in Types

#### Types can also be recursive
The structure of data is frequently self-referential
- A natural number is either 0 or the successor of a natural
	- `data Nat = Zero | Succ Nat`
- A list is either empty or consists of a first value and a following list
	- `data List a = Nil | Cons a (List a)`
- A tree is either a leaf or branches to two trees
	- `data Tree a = Leaf a | Branch (Tree a) (Tree a)`

- Recursion in types implies recursion in terms

```Haskell
data List a = Nil | Cons a (List a)

someInts = Cons 1 (Cons 2 Nil)

sum :: List Int -> Int
sum Nil = 0
sum (Cons x xs) = x + sum xs 
```

### Recursion and Efficiency

