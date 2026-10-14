That's better.

Next, we’ll do the Right case:

```
liftEither :: ∀ e m a. MonadError e m => Either e a -> m a
liftEither (Left err) = throwError err
liftEither (Right x) = ???
```

We just want to wrap x up in the MonadError, in our case, ExceptT. We’ll use pure for that since we generalized this Function:

```
liftEither :: ∀ e m a. MonadError e m => Either e a -> m a
liftEither (Left err) = throwError err
liftEither (Right x) = pure x
```

Now, this may seem done and quite terse. But, there’s a very useful helper that will make this far terser. It’s called either:

```
either :: ∀ a b c. (a -> c) -> (b -> c) -> Either a b -> c ① ②
```

+   ① a -> c maps the Left to c.
+   ② b -> c maps the Right to c.

Both throwError and pure are Functions that can be passed to either:

```
import Data.Either (Either(..), either) ①

liftEither :: ∀ e m a. MonadError e m => Either e a -> m a
liftEither = either throwError pure
```

① Added either to import list.

That reads nicely. To me it says that liftEither will throwError on the Left and pure on the Right.

Add this Function to your module.

Now, returning to line of code we’re incubating:

```
verifySession sessionsAVar authToken <?> note NotAuthenticated
  :: Aff (Either CreateUserFailureReason Session)
```