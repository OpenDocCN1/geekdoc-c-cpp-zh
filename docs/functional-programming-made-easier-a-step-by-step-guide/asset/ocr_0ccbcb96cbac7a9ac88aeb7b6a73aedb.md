If you’re thinking like I’m thinking then you’re thinking about `>>=`:

```
instance bindStateT :: Monad m => Bind (StateT s m) where
  bind :: ∀ a b. StateT s m a -> (a -> StateT s m b) -> StateT s m b
  bind (StateT fmx) f = StateT \\s -> fmx s >>= \\(Tuple x s') -> ???
```

> Remember that the contained Function in `StateT` returns `Tuple a s`.

Now that we have access to a Value of Type of `a`, i.e. `x`, we can finally pass it to `f`:

```
instance bindStateT :: Monad m => Bind (StateT s m) where
  bind :: ∀ a b. StateT s m a -> (a -> StateT s m b) -> StateT s m b
  bind (StateT fmx) f = StateT \\s -> fmx s >>= \\(Tuple x s') -> f x ???
```

So what Type is `f x`?

Looking back at the Types we wrote down, we can see that `f` is of Type `a → StateT s m b`. That means `f x` is Type `StateT s m b`.

But remember that `StateT`’s contained Function returns an `m (Tuple a s)`. So, we have `StateT s m b` with `f x`, but we want to return `m (Tuple a s)`.

How can we get from one to the other?

Remember `runStateT`? If not, here it is again:

```
runStateT :: ∀ s m a. StateT s m a -> s -> m (Tuple a s)
runStateT (StateT f) = f
```

> Removed redundant Parentheses we had earlier.

This is the perfect function to consume our `StateT s m b` and produce what we need, i.e. `m (Tuple b s)`.

We just need to provide the current State as the second Parameter, which we can get from the `Tuple` we destructured to extract `s'`:

```
instance bindStateT :: Monad m => Bind (StateT s m) where
  bind :: ∀ a b. StateT s m a -> (a -> StateT s m b) -> StateT s m b
  bind (StateT fmx) f =
    StateT \\s -> fmx s >>= \\(Tuple x s') -> runStateT (f x) s'
```

And it compiles.