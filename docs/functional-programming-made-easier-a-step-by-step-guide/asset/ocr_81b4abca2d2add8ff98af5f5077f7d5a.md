④ We use the Monoid’s EMPTY value for the value in the first position.

Now, let’s see our newly minted Applicative in action:

```
Tuple "abc" (_ * 10) <*> Tuple "123" 42 -- Tuple "abc123" 420
pure (_ * 10) <*> Tuple "abc" 42 -- Tuple "abc" 420 ①
Tuple "abc" (_ * 10) <*> pure 42 -- Tuple "abc" 420 ①
```

① Notice that when we apply with a Pure Function or a Pure Value, that the first value of the Tuple remains untouched. That’s because of the mempty that pure uses.

Now that we’ve solved the problem with Tuple, we should be able to use that experience to extrapolate to Threeple:

```
data Threeple a b c = Threeple a b c
```

We now have to worry about combining 2 Types, a and b. Can you think of the solution?

More Monoid Constraints:

```
instance applyThreeple ::
  (Monoid a, Monoid b) => Apply (Threeple a b) where ①
    apply (Threeple v w f) (Threeple x y z) =
      Threeple (v <> x) (w <> y) (f z) ②

instance applicativeThreeple ::
  (Monoid a, Monoid b) => Applicative (Threeple a b) where ①
    pure x = Threeple mempty mempty x ③
```

① We hold a and b constant.

② We combine the a values and the b values.

③ We have 2 empty values.

# 16.7. Applicative Instance for Sum Types

With Sum Types, we had none of the problems we encountered writing Applicative Instances for Product Types.

Here’s our implementation for Maybe again: