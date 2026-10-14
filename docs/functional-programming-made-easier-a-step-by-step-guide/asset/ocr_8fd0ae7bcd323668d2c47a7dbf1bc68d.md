# 28.10. Coding the API

Along the way, we’ve coded the API for the `LogonRequest` to get all of our server parts working. But now, it’s time to finish the API.

We have the following API requests left to code:

+   - Create User
+   - Query Users
+   - Logoff

Let’s start with the easiest one, `LogoffRequest`. This is a good time to do this since we just finished `LogonRequest`.

# 28.10.1. Coding `LogoffRequest` API Handler

Before we code this, we should look back at what we did for `Logon` to see what we can steal:

```
data Logon = Logon

handler :: LogonRequest -> Handler
handler (LogonRequest { userName, password }) = do
  { accountsAVar } <- ask
  verifiedAccount <- lift $ verifyLogon accountsAVar userName password
  HTTPure.ok $ encodeJSON $ case verifiedAccount of
    Nothing -> LogonResponse LogonResultsFailure
    Just (Account { temporaryPassword }) -> LogonResponse
      $ LogonResultsSuccess
        { authToken: emptyUUID -- TODO get from Session Mgr
        , mustChangePassword: temporaryPassword
        }

instance apiHandlerLogon :: ApiHandler Logon where
  handle request _ = do
    logonReq <- runExcept (decodeJSON request :: _ LogonRequest)
    pure $ handler logonReq
```

Take a look at the `ApiHandler` Instance. And see what we’ll have to change to implement Logoff’s instance. Make a mental list of the changes you’d make before reading on.

I could only see 3: