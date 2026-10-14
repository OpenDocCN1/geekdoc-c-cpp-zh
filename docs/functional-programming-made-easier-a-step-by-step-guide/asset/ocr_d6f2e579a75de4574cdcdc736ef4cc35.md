And this is usually where we have to stop and think.

Since the Types here are more complex than for `map`, let’s write the specialized Type Signature for `apply`. Go ahead and write out the Type Signature specialized for `StateT` before reading on.

Here’s the Type Signature specialized for `StateT`:

```
instance applyStateT :: Functor m => Apply (StateT s m) where
  apply :: ∀ a b. StateT s m (a -> b) -> StateT s m a -> StateT s m b
  apply (StateT fmf) (StateT fmx) = StateT \\s -> ???
```

Now, write out the Types for `fmf` and `fmx` before reading on.

Here are the Types:

```
fmf :: s -> m (Tuple (a -> b) s)
fmx :: s -> m (Tuple a s)
```

❶ Don’t forget that `fmf`, once called, will return a Function, albeit inside of a `Tuple` that’s inside of a `Monad`.

In `apply`, we always work with the lefthand Parameter first, i.e. `fmf` and then work with the right-hand side next.

Keeping that in mind along with all the Types, go ahead and see if you can finish this before reading the solution.

The next step is to call `fmf` and destructure the `Tuple` to get at the mapping Function:

```
instance applyStateT :: Functor m => Apply (StateT s m) where
  apply (StateT fmf) (StateT fmx) = StateT \\s -> fmf s ???
```

And now we’ll need to `map` to a `Lambda` like we did in our `map` implementation:

```
instance applyStateT :: Functor m => Apply (StateT s m) where
  apply (StateT fmf) (StateT fmx) = StateT \\s ->
    fmf s <#> \\(Tuple f s') -> ???
```

And now we do the same thing for `fmx`: