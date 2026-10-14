```
import Utils (apiCall) ①

handleAction :: Action -> H.HalogenM State Action Slots Output m Unit
handleAction = case _ of
  Input f -> H.modify_ f
  Logon -> do
    { userName, password } <- H.get
    logonResponse <-
      apiCall (LogonRequest { userName, password }) ②
    case logonResponse of
      Left err -> alertError err
      Right (LogonResponse LogonResultsFailure) ->
        alertError "Invalid Logon Credentials"
      Right (LogonResponse (LogonResultsSuccess
        { authToken, admin, mustChangePassword })) -> do
        log <<< logEntry Info "User logged on"
        { userRef } <- ask
        H.liftEffect $ Ref.write (Just { admin, authToken }) userRef
        navigate <<< logonRoute
          $ if mustChangePassword then PasswordTemporary
            else PasswordPermanent
```

① Import apiCall.

② Using apiCall. Removed code that’s duplicated in apiCall.

And don’t forget to remove the following imports:

```
import Affjax as Ajax
import Affjax.ResponseFormat as ResponseFormat
import Affjax.RequestBody as RequestBody
import Data.Bifunctor (lmap)
import Control.Monad.Except (runExcept)
import Foreign.Generic (encodeJSON, decodeJSON)
```

Step back for a moment and notice how much nicer handleAction looks with apiCall. Refactoring is a pain in the moment but it always leave our codebase looking so much better.

This will also make calling other APIs on other Pages so much easier.

Before we can start coding the render Function for the Users Page, I’d like to make some changes to our Page Component that’ll give us some more control over styling.

When we originally created the Page Component, we centered the content: