and continue reading.

Our final step is to send the response to the client:

```
import Foreign.Generic (encodeJSON) ①
import HTTPure as HTTPure

handler :: LogoffRequest -> Handler
handler (LogoffRequest { authToken }) = do
    { sessionsAVar } <- ask
    verifiedSession <- lift $ verifySession sessionsAVar authToken
    response <- case verifiedSession of
        Nothing -> pure $ LogoffResponse LogoffResultsFailure
        Just _ -> do
            lift $ deleteSession sessionsAVar authToken
            pure $ LogoffResponse LogoffResultsSuccess
    HTTPure.ok $ encodeJSON response ②
```

① Import encodeJSON and HTTPure qualified.

② We encode the response and reply with HTTPure.ok.

Now you can test this code using Postman. But first, we’ll need to run the server:

```
npx spago run
```

Before we can send a Logoff, we’ll have to first send a Logon Request. Use the same settings from earlier:

![](bbox=[0.145, 0.617, 0.854, 0.957])