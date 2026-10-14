And we’ll also write ap without the do:

```
ap :: ∀ a b m. Monad m => m (a -> b) -> m a -> m b
ap ff fx = ff >>= (\f -> fx >>= (\x -> pure $ f x))
```

① Redundant Parentheses have been added to segregate the Functions passed to m’s bind, i.e. >>=.

And we’re going to need pure from our Parser:

```
instance applicativeParser :: Applicative (Parser e) where
  pure x = Parser \s -> pure $ Tuple s x
```

We’ll start with ap and replace the bind implementation from Parser one step at a time to see the final computation.

This is going to be a daunting task. Not because it’s difficult, but because there’s so many symbols. So, go through this slowly: