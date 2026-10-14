In the PureScript library, there are 2 functions, foldMapDefaultR and foldMapDefaultL which effectively is the above code.

And as it turns out, the authors of the Array Foldable Typeclass chose to be Right-Associative, while the authors of List chose Left-Associative.

While this is unfortunate, it’s possible to convert between a List and an Array, so we can choose which one we want. We also can explicitly call foldMapDefaultR on Lists. But these non-default solutions cannot benefit from Typeclasses.

So, let’s pick Left-Associative to match the library author’s choice:

```
instance foldableList :: Foldable List where
  foldr _ acc Nil      = acc
  foldr f acc (x : xs) = f x (foldr f acc xs)
  foldl _ acc Nil      = acc
  foldl f acc (x : xs) = foldl f (f acc x) xs
  foldMap _ Nil        = mempty
  foldMap f l          = foldl (\acc x -> acc <> f x) mempty l ①
```

① We cannot write in Point-free when using Pattern Matching.

# 10.5. Rewriting length with Folds

Since foldl and foldr pass State, we can recode the Tail Recursive version of length using Fold. Before we do, let’s revisit that version of length:

```
length :: ∀ a. List a -> Int
length l = go 0 l where ①
  go :: ∀ a. Int -> List a -> Int ①
  go acc Nil      = acc
  go acc (x : xs) = go (acc + 1) xs ②
```

① The first Parameter is our State, which is the current count and it starts at 0.

② Each iteration we add 1 to our count.

We have to determine 2 things to use foldl or foldr. First, what’s the State and its initial value. In this case, it’s a count of the number of elements in the List and its Initial Value is 0.

And the second thing to determine is what operation will we do each iteration. In this case, we’ll simply add 1 to our count.

The last thing to determine is if Associativity matters to us. Since our operation is +, which is Commutative, i.e. order does NOT matter, we do not care about Associativity.