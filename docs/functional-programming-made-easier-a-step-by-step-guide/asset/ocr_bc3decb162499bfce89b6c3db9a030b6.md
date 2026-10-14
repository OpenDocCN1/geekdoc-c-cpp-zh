It should be clear that we’re missing a crucial piece of information to complete the code for this Page.

Return to the `server` code and where we put `authToken` into the `LogonResponse`, let’s also add `admin`. Make this change before reading further.

First thing to do is to add an `admin` field to `LogonResponse`:

```
data LogonResults
  = LogonResultsSuccess
      { authToken :: UUID
      , admin :: Boolean
      , mustChangePassword :: Boolean
      }
  | LogonResultsFailure
```

❶ Added `admin` to Record.

Next, we’ll update the Logon API Handler in `Handler.Api.Logon`:

```
handler :: LogonRequest -> Handler
handler (LogonRequest { userName, password }) = do
  { accountsAVar, sessionsAVar } <- ask
  verification <- lift $ verifyLogon accountsAVar userName password
  response <- case verification of
    Nothing -> pure $ logonResponse LogonResultsFailure
    Just (Account { admin, temporaryPassword }) -> do
      authToken <- lift $ createSession sessionsAVar userName
      pure $ LogonResponse
        $ LogonResultsSuccess
          { authToken
          , admin
          , mustChangePassword: temporaryPassword
          }
  HTTPure.ok $ encodeJSON response
```

❶ Added `admin` to the destructuring from the `Account`.

❷ Added `admin` to the response.

Now, kill the server with `Ctrl-C` and rerun it with:

```
npx spago run
```

Once the server is running, return to the `client` project and build it so the editor will see the changes we