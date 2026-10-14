```
randomGenerator :: (Number -> Boolean) -> FiberM Unit
randomGenerator pred = do
  { count } <- get
  unless (count <= 0) do
    n <- liftAffToFiberM delayRandom
    ???
```

Now we can write it to the Bus. But wait. We don’t have a Bus. We’re going to have to get the Bus first from the read-only data ReaderT provides us:

```
randomGenerator :: (Number -> Boolean) -> FiberM Unit
randomGenerator pred = do
  { count } <- get
  unless (count <= 0) do
    n <- liftAffToFiberM delayRandom
    { bus } <- ask ①
    ???
```

① We’re destructuring the Config Record to get at the Bus.

Now, we can write to it, but if and only if the pred returns true:

```
randomGenerator :: (Number -> Boolean) -> FiberM Unit
randomGenerator pred = do
  { count } <- get
  unless (count <= 0) do
    n <- liftAffToFiberM delayRandom
    { bus } <- ask
    when (pred n) $ Bus.write (show n) bus ①
    ???
```

① This too runs in Aff.

We need to lift Bus.write: