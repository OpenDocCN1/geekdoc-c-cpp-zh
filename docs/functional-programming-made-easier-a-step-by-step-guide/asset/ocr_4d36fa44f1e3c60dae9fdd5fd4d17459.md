```
class Apply m <= Bind m where
  bind :: ∀ a b. m a -> (a -> m b) -> m b

infixl 1 bind as >>=

class (Applicative m, Bind m) <= Monad m
```

And here are the helper Functions:

```
composeKleisli
  :: ∀ a b c m
    . Monad m
  => (b -> m c)
  -> (a -> m b)
  -> (a -> m c)
composeKleisli g f x = f x >>= g

infixr 5 composeKleisli as >=>

join :: ∀ a m. Bind m => m (m a) -> m a
join x = x >>= identity
```

And here are the flipped version of the operators:

```
composeKleisliFlipped
  :: ∀ a b c m
    . Monad m
  => (a -> m b)
  -> (b -> m c)
  -> (a -> m c)
composeKleisliFlipped = flip composeKleisli

infixr 1 composeKleisliFlipped as <=< ①

bindFlipped :: ∀ a b m. Bind m => (a -> m b) -> m a -> m b
bindFlipped = flip bind

infixr 1 bindFlipped as =<< ②
```

① Flipped Fish Operator.

② Flipped bind.