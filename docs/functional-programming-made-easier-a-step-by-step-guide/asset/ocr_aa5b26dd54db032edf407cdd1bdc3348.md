```
-- ABOVE CODE REDACTED
where
handleAction :: Action -> H.HalogenM State Action Slots Output m Unit
handleAction = case _ of
  Input f -> H.modify_ f
  Logon -> do
    { userName, password } <- H.get ①
    pure unit
```

① Get State destructuring to get userName and password.

Next, make the Ajax call to the server to attempt to Logon. If you forget how to do this, refresh your memory by looking at the test Function in Ch25b.purs.

Return here when that's complete.

Here's that addition:

```
import Affjax as Ajax ①
import Affjax.ResponseFormat as ResponseFormat
import Affjax.RequestBody as RequestBody
import Data.Api.Logon (LogonRequest(..)
                     , LogonResponse(..), LogonResults(..)) ②
import Foreign.Generic (encodeJSON)

-- ABOVE CODE REDACTED
where
handleAction :: Action -> H.HalogenM State Action Slots Output m Unit
handleAction = case _ of
  Input f -> H.modify_ f
  Logon -> do
    { userName, password } <- H.get
    ajaxResult <- H.liftAff $ Ajax.post ResponseFormat.string ③ ④
      "http://localhost:3000/"
      $ Just $ RequestBody.String ⑤
      $ encodeJSON $ LogonRequest { userName, password } ⑥
    pure unit
```

① Added these imports.

② There's more imported here than we need at the moment, but we'll need them eventually.

③ Note that ajaxResult is an Either.

④ The ResponseFormat is a String since we're going to use decodeJSON on it. This is unlike test in