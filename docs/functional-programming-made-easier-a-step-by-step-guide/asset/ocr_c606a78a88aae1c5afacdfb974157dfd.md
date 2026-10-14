Our Bind Instance has a Constraint of Semigroup, but it's our Applicative Instance that has a Constraint of Monoid that's causing us grief.

For us to use ap, we'll have to tighten our requirements on Apply, by changing the Constraint from Semigroup to Monoid:

```
instance applyWriter :: Monoid w => Apply (Writer w) where
  apply = ap
```

And, to no one's surprise, a brand new compiler error. This time on our Bind Instance implementation:

![](bbox=[0.235, 0.291, 0.765, 0.539])

Again, it now wants our w to have a Monoid Constraint, but this time on Bind. That's because Bind is an Apply and since we just changed Apply's Constraint to Monoid, we'll need to change Bind's Constraint to match:

```
instance bindWriter :: Monoid w => Bind (Writer w) where
  bind (Writer (Tuple x l1)) f =
    f x # \(Writer (Tuple y l2)) -> Writer (Tuple y (l1 <> l2))
```

And finally, the compiler is happy. But, notice that's there's no such thing as a free lunch. We cheated by not writing Apply and relied on our Monad implementation instead. This came at the cost of forcing the log to be a Monoid instead of a Semigroup.

But, this cost is fairly low, since we're probably going to use the Monad instance for Writer, which already had a Monoid Constraint. The use case of using Writer as ONLY an Apply, where we'd only require a Semigroup, is probably an edge case.