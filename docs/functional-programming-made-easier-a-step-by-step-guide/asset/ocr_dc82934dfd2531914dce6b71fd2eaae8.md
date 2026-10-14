# # MonadEffect

```
class (Monad m) <= MonadEffect m where
```

The `MonadEffect` class captures those monads which support native effects.

Instances are provided for `Effect` itself, and the standard monad transformers.

`liftEffect` can be used in any appropriate monad transformer stack to lift an action of type `Effect a` into the monad.

# Members

+   - `liftEffect :: forall a. Effect a -> m a`

# Instances

+   - `MonadEffect Effect`

Search Pursuit for Aff and see what Instances Aff supports then continue reading.

When you do this, you will see that Aff indeed does support liftEffect: