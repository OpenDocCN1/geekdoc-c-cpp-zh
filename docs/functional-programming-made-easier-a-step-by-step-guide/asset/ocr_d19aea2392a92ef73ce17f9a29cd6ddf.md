perform the function (in our example, Subtraction) and return the result to the previous call, which in turn will perform the function with the previous value and so on and so on:

```
```haskell
instance foldableList :: Foldable List where
  foldr _ acc Nil      = acc
  foldr f acc (x : xs) = f x (foldr f acc xs)
```
```

❶ Base case returns the Initial Value.

❷ Here we can see that we defer the function call `f` until `(foldr f acc xs)` is computed. And each subsequent recursion will do the same until the last element is computed with the Initial Value (the value returned from the base-case).

To get a different perspective on how this works, let’s look at executing this step by step by doing Algebraic Substitution:

```
```haskell
foldr (-) 99 [1, 2, 3] =                 -- initial call
(-) 1 (foldr (-) 99 [2, 3]) =             -- substitution into ❷
(-) 1 ((-) 2 (foldr (-) 99 [3])) =        -- substitution into ❷
(-) 1 ((-) 2 ((-) 3 (foldr (-) 99 []))) = -- substitution into ❷
(-) 1 ((-) 2 ((-) 3 99)) =                -- substitution into ❶
(-) 1 ((-) 2 (3 - 99)) =                  -- rewrite prefixed as infixed
(-) 1 (2 - (3 - 99)) =                    -- rewrite prefixed as infixed
1 - (2 - (3 - 99)) =                      -- rewrite prefixed as infixed
```
```

Notice how 99, our Initial Value, got passed all the way down until it was needed in the computation with our last element, 3.

Next, we write the base-case for `foldl`:

```
```haskell
instance foldableList :: Foldable List where
  foldr _ acc Nil      = acc
  foldr f acc (x : xs) = f x (foldr f acc xs)
  foldl _ acc Nil      = acc
```
```

And then the recursive case:

```
```haskell
instance foldableList :: Foldable List where
  foldr _ acc Nil      = acc
  foldr f acc (x : xs) = f x (foldr f acc xs)
  foldl _ acc Nil      = acc
  foldl f acc (x : xs) = ???
```
```