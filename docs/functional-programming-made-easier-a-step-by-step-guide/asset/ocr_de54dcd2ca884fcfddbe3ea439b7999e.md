```
```haskell
startup :: Array Account -> Aff (AVar Accounts)
startup accounts = do
  accountsAVar <- AVar.empty
  (accounts
    <#> \\account@(Account { userName }) -> Tuple userName account)
    # Map.fromFoldable
    # AVar.new

shutdown :: AVar Accounts -> Aff Unit
shutdown = void <<< AVar.take
```
```

Looks like we can steal all of `shutdown`, which reminds me that we never called Account Manager’s shutdown. We should add that now, before I forget again.

Go ahead and call `shutdown` in `main` BEFORE the server shuts down and then return here to compare your code with mine.

Here’s my implementation of that:

```
```haskell
main :: Effect Unit
main = launchAff_ do
  loadResults <- AccountHandler.loadAccounts
  case loadResults of
    Left err -> log $ "Cannot load accounts: " <> show err
    Right accounts -> do
      accountsAVar <- AccountManager.startup accounts
      liftEffect $ do
        shutdown <- HTTPure.serve port (router { accountsAVar })
        $ log $ "Server up running on port: " <> show port
        let shutdownServer = do
              log "Shutting down server..."
              AccountManager.shutdown accountsAVar
              -- COMPILER ERROR!!
              shutdown $ log "Server shutdown."
        onSignal SIGINT shutdownServer
        onSignal SIGTERM shutdownServer
```
```

❶ Add the call to `shutdown`.

The compiler error: