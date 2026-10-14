```
```haskell
foldl :: ∀ a b. (b -> a -> b) -> b -> f a -> b
```
```

It is identical to `foldr` except for the First Parameter. The First Parameter is a function whose Parameters are `flipped` when compared with `foldr`. We’ll see why this is important soon.

And finally, `foldMap`:

```
```haskell
foldMap :: ∀ a m. Monoid m => (a -> m) -> f a -> m
```
```

Let’s break down each of its Parameters:

```
```text
(a -> m)    -- function to convert the element to a Monoid
f a         -- Foldable type `f`, e.g. `List` or `Array`
```
```

This function returns an `m`, which is a `Monoid`.

Can you think of why it’s a `Monoid` and not a `Semigroup`? It could’ve been a `Semigroup` but then we’d burden the user with having to pass an Initial Value, which if is possible, means that the Type is probably already a `Monoid`.

Notice how `foldMap` doesn’t require an Initial Value like `foldl` and `foldr`. That’s because `foldMap` works with `Monoids` and can use the Type’s `mempty` as its Initial Value.

Also, notice that the variable `f` is being used here as the collection or structure that we’re folding over. Once again, that’s because it stands for `Functor` since most `Functors` are also `Foldable`. Don’t worry, we will spend plenty of time on `Functors` soon enough.

# ## 10.3. Fold Associativity

`foldr` is Right-Associative and `foldl` is Left-Associative meaning:

```
```haskell
foldr (-) 99 [1, 2, 3] == 1 - (2 - (3 - 99)) == -97
foldl (-) 99 [1, 2, 3] == ((99 - 1) - 2) - 3 == 93
```
```

Notice where the Initial Value, `99`, is. It’s on the Far Right for `foldr` and the Far Left for `foldl`.

To better understand the differences, let’s rewrite the `(-)` to show the moving parts:

```
```haskell
foldr (\n acc -> n - acc) 99 [1, 2, 3] == -97
foldl (\acc n -> acc - n) 99 [1, 2, 3] == 93
```
```