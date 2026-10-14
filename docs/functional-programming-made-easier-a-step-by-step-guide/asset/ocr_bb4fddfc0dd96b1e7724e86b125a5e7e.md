definition:

```
newtype ReaderT r m a = ReaderT (r -> m a)
```

From this, we can see that it has to return a Value of Type `a` in a Context, `m`. We have exactly that in `mx`, so we can just return that:

```
instance monadTransReaderT :: MonadTrans (ReaderT r) where
  lift mx = ReaderT \\r -> mx
```

Now, since we’re not using `r`, we can eliminate it:

```
instance monadTransReaderT :: MonadTrans (ReaderT r) where
  lift mx = ReaderT \\_ -> mx
```

And now we can replace `\\_ -> mx` with `const mx`:

```
instance monadTransReaderT :: MonadTrans (ReaderT r) where
  lift mx = ReaderT $ const mx
```

And now we can compose the Data Constructor, `ReaderT`, with `const`:

```
instance monadTransReaderT :: MonadTrans (ReaderT r) where
  lift mx = (ReaderT <<< const) mx
```

And finally, ETA-reduce, i.e. cancel `mx` on the right-hand side on both sides of the equal sign:

```
instance monadTransReaderT :: MonadTrans (ReaderT r) where
  lift = ReaderT <<< const
```

And we’re done.

But wait. The right-hand side of the equal sign seems awfully familiar. Didn’t we have something like that when we wrote `pure`?

Let’s look at `pure`: