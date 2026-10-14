```
class MonadThrow e m <= MonadError e m | m -> e where
  catchError :: ∀ a. m a -> (e -> m a) -> m a ①
```

① Notice that the Type Signature is very different from ask or tell. This should be a clue that we’re going to need to take a different approach than we did with those instances.

Before we move on to the code MonadError, we should understand catchError. Here’s our AppM code from the previous Chapter that has been modified to catch the error:

```
validate :: Int -> AppM
validate n = when (n == 0) $ void $ throwError "WE CANNOT HAVE A 0 STATE!"

app :: AppM
app = do
  log "Starting App..."
  n <- get
  -- when (n == 0) $ void $ throwError "WE CANNOT HAVE A 0 STATE!" ①
  catchError (validate n) (\err -> do ②
    log $ "We encountered an error: " <> err
    put 1
  )
  put $ n + 1
  log "Incremented State"
  pure unit
```

① Our old code threw the error and Short-circuited the computation. It’s been commented out.

② In this new version, we catch the error thrown by validate and handle it by writing to the log and making the State non-zero. This does NOT Short-circuit the computation, but, instead, provides an alternative computation that never fails.

Notice how the Lambda is running in the AppM Monad. This matches the second Parameter to catchError, i.e. e -> m a, where m in our case is ExceptT String (WriterT String (StateT Int Effect)) Unit, or AppM as we like to refer to it:

```
type AppStack e w s a = ExceptT e (WriterT w (StateT s Effect)) a

type AppM = AppStack String String Int Unit
```

Since catchError’s Type Signature is very different from ask and tell we cannot simply lift the underlying Monad’s implementations.

Since this instance is complex and fraught with caveats, which we will soon see, we’re going to code this