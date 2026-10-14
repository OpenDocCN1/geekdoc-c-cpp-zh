We’ve used `g` and we’ve used `rws`. The only thing we haven’t done is to apply `f` to a Value of Type `a`, which in our case is `x`.

```
instance functorRWS :: Functor (RWS r w s) where
  map f (RWS g) =
    RWS \\ rws -> g rws # \\ (Tuple x rws') -> Tuple (f x) rws'
```

> After applying `f` to `x`, we wrap the return value in a `Tuple`.

Now, write the `Apply` Instance before moving on. Hint: we’re going to be making `RWS` a `Monad` so feel free to cheat.

Here’s the implementation:

```
instance applyRWS :: Apply (RWS r w s) where
  apply = ap    -- COMPILER ERROR!!
```

We have a compiler error because we haven’t written the `Monad` Instance yet. We’ll ignore this for now.

Next, write the `Applicative` Instance and then read on to see how you did.

First, we write the instance definition:

```
instance applicativeRWS :: Applicative (RWS r w s) where
```

Now we write the left-hand side of the implementation:

```
instance applicativeRWS :: Applicative (RWS r w s) where
  pure x = ???
```

And on the right-hand side we start with the usual:

```
instance applicativeRWS :: Applicative (RWS r w s) where
  pure x = RWS \\ rws -> ???
```

And we’re just going to wrap up `x` and `rws` in a `Tuple`:

```
instance applicativeRWS :: Applicative (RWS r w s) where
  pure x = RWS \\ rws -> Tuple x rws
```