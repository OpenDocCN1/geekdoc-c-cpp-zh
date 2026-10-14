
```
import Handler.Account as AH ①
import Manager.Account as AM

handler :: CreateUserRequest -> Handler
handler (CreateUserRequest { authToken, user: user' }) = do
    { accountsAVar, sessionsAVar } <- ask
    verifiedSession <- lift $ verifySession sessionsAVar authToken
    response <- case verifiedSession of
        Nothing -> CreateUserResponse
            $ CreateUserResultsFailure { reason: NotAuthenticated }
        Just (Session { userName }) -> do
            admin <- lift $ AM.findAccount accountsAVar userName ②
                <#> maybe false (\(Account a) -> a.admin)
            if not admin then pure CreateUserResponse
                $ CreateUserResultsFailure { reason: NotAuthorized }
            else do
                passwordHash <- lift
                    $ passwordHashHex user'.userName user'.password
                let user = delete (Proxy :: _ "password") user'
                    account = Account $
                        insert (Proxy :: _ "passwordHash") passwordHash user
                result <- lift $ AM.createAccount accountsAVar account ②
                case result of
                    AM.CreateAccountAlreadyExists -> CreateUserResponse ②
                        $ CreateUserResultsFailure { reason: AlreadyExists }
                    AM.CreateAccountSuccess -> do ②
                        result <- lift $ AH.createAccount account ③ ④
                        ???
```

① Had to change these to be imported qualified since we have 2 createAccounts.

② Change these lines of code to use qualified import of AM.

③ Use qualified import of AH.

④ Don’t forget lift.

Now, we can handle the error and success cases:

```
handler :: CreateUserRequest -> Handler
handler (CreateUserRequest { authToken, user: user' }) = do
  { accountsAVar, sessionsAVar } <- ask
  verifiedSession <- lift $ verifySession sessionsAVar authToken
  response <- case verifiedSession of
    Nothing -> CreateUserResponse
      $ CreateUserResultsFailure { reason: NotAuthenticated }
    Just (Session { userName }) -> do
      admin <- lift $ AM.findAccount accountsAVar userName
        <#> maybe false (\(Account a) -> a.admin)
      if not admin then pure CreateUserResponse
        $ CreateUserResultsFailure { reason: NotAuthorized }
      else do
        passwordHash <- lift
          $ passwordHashHex user'.userName user'.password
        let user = delete (Proxy :: _ "password") user'
            account = Account $
              insert (Proxy :: _ "passwordHash") passwordHash user
        result <- lift $ AM.createAccount accountsAVar account
        case result of
          AM.CreateAccountAlreadyExists -> CreateUserResponse
            $ CreateUserResultsFailure { reason: AlreadyExists }
          AM.CreateAccountSuccess -> do
            result <- lift $ AH.createAccount account
            pure $ case result of ①
              AH.CreateAccountFileError err -> CreateUserResponse
                $ CreateUserResultsFailure { reason: FileIOError err }
              AH.CreateAccountSuccess -> CreateUserResultsSuccess
    ???
```

① Handle both the success case and error case.

And finally, we can... Wait. Wait. Wait.

Before we go any further, just take a look at what we’ve written so far. How do you feel about this code?

My thoughts are that it’s too complex. Frankly, this is a hot mess.

There’s too much error checking. What happened to all that great Monadic Happy Path programming we did earlier in the book? I want that back!!

I want the whole case expression to run in ExceptT so I don’t have to check for errors.

Our natural inclination may be to just keep forging ahead telling ourselves that we’ll fix it later, but we won’t.

```
```haskell
handler :: CreateUserRequest -> Handler
handler (CreateUserRequest { authToken, user: user' }) = do
  { accountsAVar, sessionsAVar } <- ask
  verifiedSession <- lift $ verifySession sessionsAVar authToken
  response <- case verifiedSession of
    Nothing -> CreateUserResponse
      $ CreateUserResultsFailure { reason: NotAuthenticated }
    Just (Session { userName }) -> do
      admin <- lift $ AM.findAccount accountsAVar userName
        <#> maybe false (\(Account a) -> a.admin)
      if not admin then pure CreateUserResponse
        $ CreateUserResultsFailure { reason: NotAuthorized }
      else do
        passwordHash <- lift
          $ passwordHashHex user'.userName user'.password
        let user = delete (Proxy :: _ "password") user'
            account = Account $
              insert (Proxy :: _ "passwordHash") passwordHash user
        result <- lift $ AM.createAccount accountsAVar account
        case result of
          AM.CreateAccountAlreadyExists -> CreateUserResponse
            $ CreateUserResultsFailure { reason: AlreadyExists }
          AM.CreateAccountSuccess -> do
            result <- lift $ AH.createAccount account
            pure $ case result of
              AH.CreateAccountFileError err -> CreateUserResponse
                $ CreateUserResultsFailure { reason: FileIOError err }
              AH.CreateAccountSuccess -> CreateUserResultsSuccess
  ???
```
```

The only difference is the `CreateUserFailureReason`, e.g. `NotAuthenticated`, `NotAuthorized`, `AlreadyExists` and `FileIOError`.

All error conditions are simply setting a different `CreateUserFailureReason`. That means our `do` block Type Signature can be `ExceptT CreateUserFailureReason Aff Unit`.

The `a` is `Unit` since we only want the Side-effects of these Functions and at the end we’ll just look at the `Either` that is `result` and decide whether to build the error response or the success one.

Here’s our rewrite again so far:

```
handler :: CreateUserRequest -> Handler
handler (CreateUserRequest { authToken, user: user' }) = do
  { accountsAVar, sessionsAVar } <- ask
  result <- lift $ runExceptT do
    ???
```

The first thing we did in our old code was to call verifySession. Let’s incubate this line of code starting with the Function call and modify it until it has the correct Type for our do block, i.e. ExceptT CreateUserFailureReason Aff Session.

Here’s it’s Type Signature:

```
verifySession :: AVar Sessions -> UUID -> Aff (Maybe Session)
```

We know we can use note to convert the Maybe we get from verifySession to an Either. We’ll have to map since Maybe is in the Aff Context:

```
verifySession sessionsAVar authToken <#> note NotAuthenticated
  :: Aff (Either CreateUserFailureReason Session)
```

Now, all that we need is a way to convert Aff (Either CreateUserFailureReason Session) to ExceptT CreateUserFailureReason Aff Session so we can use it in our do block.

The first thing to notice is that we have an Either and that we should be able to convert that to an ExceptT since ExceptT contains an Either:

```
newtype ExceptT e m a = ExceptT (m (Either e a))
```

And it turns out there’s a Function for that, but it’s in Haskell and for some reason it’s not in PureScript. But we’re going to write it here together. We could just copy the code from Haskell, but then we wouldn’t learn as much.

Let’s call it what they did in Haskell, liftEither:

```
import Data.Either (Either) ①

liftEither :: ∀ e m a. Either e a -> ExceptT e m a
```

① Add this import.

This will take an Either and return an ExceptT.

Next, we’ll code the Left case:

```
import Data.Either (Either(..)) ①

liftEither :: ∀ e m a. Either e a -> ExceptT e m a
liftEither (Left err) = ???
```

① Include Either’s Data Constructors.

We need a way to take an e and turn it into an ExceptT e m a. If you search Pursuit directly for e -> ExceptT e m a, you’ll get a ton of Functions none of which look right.

But if your realize that ExceptT is a specialized case of MonadError, then that might help you.

MonadError has 2 Type Parameters, e then m. So search Pursuit for e -> m a and see if you can find something that will work. Then return here.

Did you find throwError? Here’s it’s definition:

```
throwError :: ∀ a m e. MonadThrow e m => e -> m a ①
```

① In our case, the m in throwError is ExceptT e m.

We can use this:

```
import Control.Monad.Error.Class (throwError) ①

liftEither :: ∀ e m a. Either e a -> ExceptT e m a
liftEither (Left err) = throwError err
???
```

① Add this import.

But, now I want to generalize our Type Signature like throwError’s:

```
import Control.Monad.Error.Class (class MonadError, throwError) ①

liftEither :: ∀ e m a. MonadError e m => Either e a -> m a ②
liftEither (Left err) = throwError err
???
```

① Added Typeclass MonadError to import list.

② Replaced ExceptT e m with m.
