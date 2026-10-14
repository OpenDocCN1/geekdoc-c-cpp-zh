together.

Here’s `MonadError` for reference:

```
class MonadThrow e m <= MonadError e m | m -> e where
  catchError :: ∀ a. m a -> (e -> m a) -> m a
```

Let’s start with the instance definition:

```
import Control.Monad.Error.Class (class MonadThrow, class MonadError,
throwError) ❶

instance monadErrorStateT :: MonadError e (StateT s m) where
```

❶ Added `MonadError` to the import list.

At this point, I’m thinking about Constraints. Since `StateT` doesn’t handle errors, we have to delegate this call to our underlying `Monad`.

For this to work, our underlying `Monad` must support `MonadError`. We’ve seen this before with `MonadAsk` and `MonadTell`. We need to add this as a Constraint:

```
instance monadErrorStateT
    :: MonadError e m => MonadError e (StateT s m) where ❶
```

❶ The underlying `Monad` is constrained to be a `MonadError`.

Since this Method is so different from the others, we’re going add the Type Signature for `catchError` specialized for `StateT` to help us keep track of our Types:

```
instance monadErrorStateT
    :: MonadError e m => MonadError e (StateT s m) where
  catchError :: ∀ a. StateT s m a -> (e -> StateT s m a) -> StateT s m a
```

Next we’ll add the left-hand side of the implementation:

```
instance monadErrorStateT
    :: MonadError e m => MonadError e (StateT s m) where
  catchError :: ∀ a. StateT s m a -> (e -> StateT s m a) -> StateT s m a
  catchError (StateT fmx) f = ??? ❶ ❷
```

❶ The name `fmx` is to remind us that we have a Function that returns a Value in the underlying `Monad`.