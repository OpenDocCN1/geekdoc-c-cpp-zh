Now, we’re going to have to use a case expression, but at least it’ll be only one.

In the error case, we’re going to pop-up the standard Browser alert dialog box for now. Eventually, we’ll build a Dialog Component and we’ll use that instead.

But for now, add the following to your code:

```
import Web.HTML.Window (alert) ①
import Web.HTML (window)

-- ABOVE CODE REDACTED
where
handleAction :: Action -> H.HalogenM State Action Slots Output m Unit
handleAction = case _ of
  Input f -> H.modify_ f
  Logon -> do
    { userName, password } <- H.get
    ajaxResult <- H.liftAff $ Ajax.post ResponseFormat.string "http://localhost:3000/" $ Just $ RequestBody.String $ encodeJSON $ LogonRequest { userName, password }
    let logonResponse = do
          { body } <- lmap Ajax.printError ajaxResult
          lmap show $ runExcept $ decodeJSON body :: _ LogonResponse
    ???
    pure unit
where ②
alertError :: String -> H.HalogenM State Action Slots Output m Unit
alertError msg = H.liftEffect $ window >>= alert msg ③
```

① Add these imports.

② Add this where and the alertError Function. Make sure you indent it properly. It’s supposed to be the where for handleAction.

③ Since alert runs in Effect, we use H.liftEffect to lift it into HalogenM.

Now, add the case expression and just the Left case code that calls alertError before reading any further.

Here’s that addition: