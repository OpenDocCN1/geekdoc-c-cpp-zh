① Added encodeJSON to the import list.

② First encode the response and then sent it to the client.

The compiler error is:

![](bbox=[0.32, 0.16, 0.68, 0.38])

It’s trying to Pattern Match a Maybe with an Aff. Can you see my mistake?

I forgot that verifyLogon runs in Aff. It’s possible that you didn’t forget this. If so, then good on you.

Let’s fix my mistake:

```
import Control.Monad.Trans.Class (lift) ①

handler :: LogonRequest -> Handler
handler (LogonRequest { userName, password }) = do
  { accountsAVar } <- ask
  verifiedAccount <- lift $ verifyLogon accountsAVar userName password ②
  HTTPure.ok $ encodeJSON $ case verifiedAccount of ③
    Nothing -> LogonResponse LogonResultsFailure
    Just (Account { temporaryPassword }) -> LogonResponse
      $ LogonResultsSuccess
        { authToken: emptyUUID -- TODO get from Session Mgr
        , mustChangePassword: temporaryPassword
        }
```

① Import lift.

② We need to lift here because verifyLogon runs in the base of our Monad Stack, i.e. in Aff. We only need to lift once since we only have 2 layers.

③ case on the extracted results of verifiedAccount.

And now this compiles.

To be able to test this, we’re going to need to go from the main Function to handler. That will mean that