
And finally, this Function returns that result in Aff.

Next, we’ll code the left-hand side of the equal sign:

```
withAVar :: ∀ a b. AVar a -> (a -> Aff (Tuple a b)) -> Aff b
withAVar aVar f = ??? ①
```

① We have the aVar and the Function, f.

Next, we’ll get the AVar Value:

```
withAVar :: ∀ a b. AVar a -> (a -> Aff (Tuple a b)) -> Aff b
withAVar aVar f = do ①
  value <- AVar.take aVar
  ???
```

① We start with a do block.

Now, we’ll call our callback Function:

```
withAVar :: ∀ a b. AVar a -> (a -> Aff (Tuple a b)) -> Aff b
withAVar aVar f = do
  value <- AVar.take aVar
  Tuple newValue result <- f value ① ②
  ???
```

① We destructure the Tuple to get the newValue of the AVar and the result of the computation.

② Since f runs in Aff, we use bind via the <- syntax. If it did not run in Aff, we’d have to use a let.

Now, we put the newValue back into the AVar:

```
withAVar :: ∀ a b. AVar a -> (a -> Aff (Tuple a b)) -> Aff b
withAVar aVar f = do
  value <- AVar.take aVar
  Tuple newValue result <- f value
  AVar.put newValue aVar ①
  ???
```

① We ALWAYS call this. That’s how we can guarantee that we’ll never leave the AVar empty.

And finally, we’ll return the result of the computation:

```
withAVar :: ∀ a b. AVar a -> (a -> Aff (Tuple a b)) -> Aff b
withAVar aVar f = do
  value <- AVar.take aVar
  Tuple newValue result <- f value
  AVar.put newValue aVar
  pure result
```

> Return the computation result of the callback.

Looking at this Function, can you see how we can generalize it? Take a minute and see if you can figure a way to do that before continuing.

The `Aff` can be generalized to any Monad, `m`, that has a `MonadAff` Instance. But, we’ll have to make sure we lift all `Aff` Functions into `m` using `liftAff`:

```
import Effect.Aff.Class (class MonadAff, liftAff)

withAVar :: ∀ a b m. MonadAff m => AVar a -> (a -> m (Tuple a b)) -> m b
withAVar aVar f = do
  value <- liftAff $ AVar.take aVar
  Tuple newValue result <- f value
  liftAff $ AVar.put newValue aVar
  pure result
```

> Added this import.

> Changed `Aff` to `m` and added the `MonadAff` Constraint on `m`.

> Lifted all `Aff` computations into `m` using `liftAff`.

Now, this Function can be used in `Aff` or any other Monad that can run in `Aff`, e.g. our `Handler`, which is a `ReaderT` Monad Stack with `Aff` on the bottom of the Stack. `ReaderT` delegates the `Aff` calls to its underlying Monad, which only works if `Aff` is in the Stack.

Add this to your code and then change `createAccount` to use it. When you’re finished, continue reading.

Here’s that change:

```
createAccount :: AVar Accounts -> Account -> Aff CreateAccountResult
createAccount accountsAVar account@(Account { userName }) = do
  withAVar accountsAVar ①
    \accounts -> pure $ ②
      if Map.member userName accounts then ③
        Tuple accounts CreateAccountAlreadyExists
      else
        Tuple (Map.insert userName account accounts) CreateAccountSuccess
```

① We call withAVar passing in the accountsAVar.

② The original logic was a Pure Computation so we wrap it in Aff using pure.

③ Our if logic doesn’t change.

It’s nice that we incubated withAVar in this module, but it really doesn’t belong here. Besides, it would be nice to use it in verifySession.

So, we’re going to move it to a File called Utils.purs. Create that File under the src Folder and move withAVar and the appropriate imports.

Then remove the following import from Manager.Account:

```
import Effect.Aff.Class (class MonadAff, liftAff)
```

And add:

```
import Utils (withAVar)
```

Return here when you’ve completed these tasks.

Here’s Utils.purs:

```haskell
module Utils where

import Prelude

import Data.Tuple (Tuple(..))
import Effect.Aff.AVar (AVar)
import Effect.Aff.AVar as AVar
import Effect.Aff.Class (class MonadAff, liftAff)

withAVar :: ∀ a b m. MonadAff m => AVar a -> (a -> m (Tuple a b)) -> m b
withAVar aVar f = do
  value <- liftAff $ AVar.take aVar
  Tuple newValue result <- f value
  liftAff $ AVar.put newValue aVar
  pure result
```

Now change `verifySession` to use `withAVar` and then return here.

Here’s that change:

```haskell
import Utils (withAVar) ❶

verifySession :: AVar Sessions -> UUID -> Aff (Maybe Session)
verifySession sessionsAVar authToken = do
  expireSessions sessionsAVar
  withAVar sessionsAVar ❶
    \sessions -> do ❷
      now <- getTime <$> liftEffect now
      pure $ case Map.lookup authToken sessions of ❸
        Nothing -> Tuple sessions Nothing
        Just (Session session) ->
          let newSession = Session $ session { lastTime = now }
              newSessions = Map.insert authToken newSession sessions in
          Tuple newSessions (Just newSession)
```

- ❶ We’re now using `withAVar` with `sessionsAVar`. It will do the `AVar.take` and `AVar.put` before and after calling our callback function.

- ❷ Here’s our callback. It runs in `Aff`, hence the `do` block.

- ❸ Our `case` expression is a `Pure` computation so we wrap it in `Aff` with `pure`.

Now by using `withAVar`, our code is much safer and we don’t have to remember to call `AVar.put` on every possible path through our logic.

Next, we’ll need to create an `Account` on disk. But, we already have `createAccount` in `Handler.Account`:

```
createAccount :: Account -> Aff (Either String Unit)
createAccount account = lmap show
  <$> (try $ appendTextFile ASCII accountsFile $ accountToCSV account)
```

Look at this Function and see if it will work for `CreateUserRequest`’s requirements. Then continue reading.

It looks like it does, but I see a problem with it that we fixed in `createAccount` in `Manager.Account`. Compare the two and see if you can see what’s wrong with this one. Then read on.

I can see that same Boolean Blindness we avoided in the Account Manager with the return Type `Either String Unit`. Technically, it’s not Boolean Blindness but the `String` in `Either String Unit` is an implied File I/O error.

This is a case of something being implicit when explicit is not only possible but easy to implement and far better.

To remove the implicit nature of the return Type, we’re going to make a Type like `CreateAccountResult` in `Manager.Account` for `Handler.Account` and modify `createAccount` to use it. Use the names `CreateAccountSuccess` and `CreateAccountFileError` for Data Constructors.

Once that’s done, modify `createAccount` in `Handler.Account` to use our new Type.

Return back here once you’ve finished.

Here’s that change:

```
data CreateAccountResult
  = CreateAccountSuccess
  | CreateAccountFileError String

createAccount :: Account -> Aff CreateAccountResult
createAccount account = lmap show
  <$> (try $ appendTextFile ASCII accountsFile $ accountToCSV account)
  <#> case _ of
    Left err -> CreateAccountFileError err
    Right _ -> CreateAccountSuccess
```

- 1. Created a Type for the result of calling `createAccount` that is far more informative than `Either String Unit`.
- 2. Changed `Either String Unit` to `CreateAccountResult`. This probably broke whoever calls this.
- 3. Using the flipped `map` via `<#>`.

Using a **case** with a wildcard to process the `Either` from `try`.

This is a minor improvement but still worth it. Maybe not today but a month from now, we’ll appreciate this.

Now, hunt down where `createAccount` was called and make it check the new return Type. Once that’s fixed return here and continue reading.

Turns out that no one’s calling this yet. That’s good since our change would have broken our calling code.

We’re now ready to work on `Handler.Api.CreateUser`.

Create a file called `CreateUser.purs` under `src/Handler/Api` and make sure you call the module `Handler.Api.CreateUser`.

Next, look at what we did with `Handler.Api.Logoff` and see what we can steal. Then return here.

The first thing I notice that we’ll need is the data Type:

```
data Logoff = Logoff
```

Remember this is used to help the `router` to distinguish which handler to call. So, add this for `CreateUser` and then continue reading on.

Here’s that Type:

```
module Handler.Api.CreateUser where

data CreateUser = CreateUser
```

The next thing we can copy from `Logoff` is the `ApiHandler` Instance code. So go ahead and write that next. Then return here to continue.

This is boilerplate code, but we’ve reduced it down to only 1 line of code:

```
instance apiHandlerCreateUser :: ApiHandler CreateUser where
  handle _ = handleApi handler
```

And now the compiler isn’t happy because we haven’t imported anything. Steal from imports from `Logoff` to make the errors disappear. Stop when you get the error regarding `handler` since we haven’t written it yet. Do this before advancing forward.

Here are my imports:
