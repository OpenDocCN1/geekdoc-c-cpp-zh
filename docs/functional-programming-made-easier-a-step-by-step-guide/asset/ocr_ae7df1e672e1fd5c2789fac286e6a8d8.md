Next, let’s look at the Homomorphism Law. But before we do, let’s remind ourselves of what a Homomorphism is:

```
h (x · y) = h(x) ⋆ h(y)
```

Here h is the Homomorphic Function that preserves structure. With Monoid Homomorphisms, we saw how it preserved the Monoidal Structure, i.e. after we apply h, we expect the new Binary Operator to behave like a proper Monoid.

With Applicative, we expect the Function Application Operator, $, to behave similarly.

So, let’s rewrite the law to see that better:

```
pure (f x) = pure f <*> pure x        [Homomorphism]
pure (f $ x) = pure f <*> pure x        -- Added redundant $
```

Hopefully, you can now see how this matches the Homomorphism formula:

```
pure (f $ x) = pure f <*> pure x
h   (x • y) = h   (x) ⋆  h   (y) ❶
```

> ❶ Remember that the Binary Operators do not have to be the same on both sides of the equal sign. And in this case, they are not. On the left side, the Function Application Operator is $ and it’s <*> on the right.

Here pure is our Homomorphism that preserves the operation of Function Application.

We can apply the function, f to x using $ and then pure the result, and that’s equivalent to using pure on both f and x first, then applying them using the Applicative apply function, <*>.

Finally, let’s look at the Interchange Law:

```
u <*> pure x = pure (_ $ x) <*> u        [Interchange]
```

By looking at this law, it should be clear that <*> is NOT Commutative. But we can interchange the function and value if we do a tiny bit of magic. That magic is the function (\_ $ x).

Looking at just the magic bit, we can see that it’s just higher-order function that expects a function and will pass x to it.

This isn’t special since this trick works with Pure Functions and Pure Values too: