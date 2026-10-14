```
```haskell
import Data.Either (note, either)
import Foreign.Generic (encodeJSON)

handler :: QueryUsersRequest -> Handler
handler (QueryUsersRequest { authToken }) = do
  { accountsAVar, sessionsAVar } <- ask
  result <- lift $ runExceptT do
    Session { userName } <- verifySession sessionsAVar authToken
      <#> note NotAuthenticated # liftSuccess
    Account { admin } <- AM.findAccount accountsAVar userName
      <#> note NotAuthorized # liftSuccess
    if not admin then throwError NotAuthorized
    else do
      accounts <- lift $ AM.getAccounts accountsAVar
      let users = accounts <#> \(Account r) ->
            User $ delete (Proxy :: _ "passwordHash") r
      pure $ QueryUsersResultsSuccess { users }
  let ok = HTTPure.ok <<< encodeJSON <<< QueryUsersResponse
  result # either
    (ok <<< \reason -> QueryUsersResultsFailure { reason })
    (ok <<< const QueryUsersResultsSuccess)
```
```

+   1. Added `either` to the import list.
+   2. Added this import.
+   3. Copied this code from `CreateUser`’s implementation and changed `CreateUser` to `QueryUsers` in these 3 places.

Here’s our compiler error:

![](bbox=[0.323, 0.682, 0.679, 0.906])

Can you see where I’ve gone wrong?