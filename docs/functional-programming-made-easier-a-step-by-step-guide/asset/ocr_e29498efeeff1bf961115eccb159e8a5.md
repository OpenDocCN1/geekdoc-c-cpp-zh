```
```haskell
Just $ RequestBody.String
  $ encodeJSON { userId:1, title:"title", completed:false }
```
```

Now, we have to deal with the results of the `POST` call, i.e. `postResult`. Processing this result will be similar to what we wrote for the `get` one.

So, let’s factor that code out first, because that code is ugly.

We’ll call our factored-out Function, `processAjaxResult`:

```
```haskell
import Effect.Class (class MonadEffect)

processAjaxResult
  :: ∀ m. MonadEffect m
  => Either Ajax.Error (Ajax.Response String)
  -> m Unit
processAjaxResult = case _ of
  Left err -> log $ "ERROR: " <> Ajax.printError err
  Right { body } ->
    case runExcept (decodeJSON body :: F GetPostRes) of
      Left err -> log $ "ERROR: " <> show err <> " (" <> body <> ")"
      Right v -> log $ show v
```
```

❶ Import `MonadEffect` class.

The body of this code is just a copy/paste of the `case` expression from our `test` code. The Type Signature is the only thing new here, so let’s examine it:

```
```haskell
processAjaxResult
  :: ∀ m. MonadEffect m
  => Either Ajax.Error (Ajax.Response String)
  -> m Unit
```
```

This is written to work in `MonadEffect`. This allows this Function to be called in any Monad that can log to the console, which also has the same requirement:

```
```haskell
log :: ∀ m. MonadEffect m => String -> m Unit
```
```

Note that we could have hardcoded the `Monad` to be `Aff`, but it’s always best to not hardcode `Monads` when it’s not required. It keeps our code flexible.

The first Parameter to `processAjaxResult` is the result from our Ajax call, i.e. a Value of Type `Either`