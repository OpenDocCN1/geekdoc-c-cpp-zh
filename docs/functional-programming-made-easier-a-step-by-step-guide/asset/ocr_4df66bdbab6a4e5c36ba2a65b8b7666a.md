I’ll give you a hint, we replaced `Int` with `Semiring` to make it work for ANY Element. How about now? Can you see any other hardcoded Type?

That’s right. The collection, i.e. the `List`, can also be Abstracted. What constraint can we put on the collection to make more general?

This Chapter is about `Foldable`, and we’ve been restricting our code to `List`, but there are many other `Foldable` Data Structures, e.g. `Array` or trees, etc.

Add the following lines to your test code in anticipation of being able to `sum` over `Arrays`:

```
log $ show $ sum [1, 2, 3] ❶
log $ show $ sum [1.0, 2.0, 3.0] ❷
```

+   ❶ Prints `6`.
+   ❷ Prints `6.0`.

So try to modify our Function to work with ANY `Foldable` Type. Then see how you did by advancing to the next section.

# 11.24. Code for `sum` using `Foldable`

```
sum :: ∀ f a. Foldable f => Semiring a => f a -> a
sum = foldl (+) zero
```

❶ We added the `Foldable f` Constraint where `f` is our foldable Type, e.g. `List`, `Array`, etc.

This final version of `sum` is as flexible as we can make it. We’ve abstracted both the Data Structure AND the Elements.

We could create a Tree and make it `Foldable` and then if the Tree holds a `Semiring`, we could call `sum` on it and it would just work with no additional effort on our part. This is the real power of Typeclasses.

And if we can, maybe we should.

# 11.25. Using `sum` with `Tree`