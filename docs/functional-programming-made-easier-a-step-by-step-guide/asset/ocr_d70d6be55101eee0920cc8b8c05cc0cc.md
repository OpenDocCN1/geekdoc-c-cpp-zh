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