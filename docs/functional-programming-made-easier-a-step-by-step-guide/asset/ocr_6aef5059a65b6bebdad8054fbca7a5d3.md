```
import Data.NonEmpty (NonEmpty, (:|))

foldl1 :: ∀ f a. Foldable f => (a -> a -> a) -> NonEmpty f a -> a
foldl1 f (x :| xs) = foldl f x xs
```

① Notice how we didn’t have to change our imports since we already import our Operator.

② Removed (..) since we’re not using Pattern Matching in this version.

The point of this exercise was do demystify foldl1. I hate when things appear to be magic. Nothing is magic once you understand it. And coding the function yourself is the best way to understand it.

# 11.18. Writing sum

Let’s take a break and write an easy function, sum that takes a List of Ints and sums them up. First we’ll write it as a recursive function and then we’ll write it using foldl.

But why not foldr? That’s because foldl is Tail Recursive and therefore makes more efficient use of the Stack AND Addition is Associative which means that it produces the same results for Right or Left-Associative computations:

```
1 + (2 + 3) == (1 + 2) + 3
```

Here’s the test code that we’ll use:

```
log $ show $ sum (1 : 2 : 3 : Nil) ①
```

① Prints 6.

So first write sum as a regular old recursive function. Then continue on.

# 11.19. Code for sum as a Recursive Function

First we write the Type Signature:

```
sum :: List Int -> Int
```

Next, we write the base-case:

```
sum :: List Int -> Int
sum Nil = 0
```