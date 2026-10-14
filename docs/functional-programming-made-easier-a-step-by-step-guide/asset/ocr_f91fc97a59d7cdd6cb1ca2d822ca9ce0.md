```
import Control.Monad.Except (runExcept, withExceptT) ①
import Manager.Account (findAccount, createAccount) ②

handler :: CreateUserRequest -> Handler
handler (CreateUserRequest { authToken, user: user' }) = do
    { accountsAVar, sessionsAVar } <- ask
    result <- lift $ runExceptT do
        Session { userName } <- verifySession sessionsAVar authToken
            <#> note NotAuthenticated # lift >>= liftEither
        Account { admin } <- AM.findAccount accountsAVar userName
            <#> note NotAuthorized # lift >>= liftEither
        unless admin $ throwError NotAuthorized
        passwordHash <- lift $ passwordHashHex user'.userName user'.password
        let user = delete (Proxy :: _ "password") user'
            account = Account $
                insert (Proxy :: _ "passwordHash") passwordHash user
        AM.createAccount accountsAVar account
            # lift >>= liftEither
            # (withExceptT $ const AlreadyExists)
        ???
        pure unit
    HTTPure.notFound
```

① Add withExceptT to import list.

② Removed CreateAccountResult(..) from import list.

Now that we’ve created a new Account in memory via AM.createAccount, we need to call AH.createAccount to create the Account on disk. But before we do, let’s work on the line outside of the code like before:

```
AH.createAccount account
:: Aff (Either CreateAccountError Unit)
```

Now, we’ll lift it and bind it to liftEither:

```
AH.createAccount account
# lift >>= liftEither
:: ExceptT CreateAccountError Aff Unit
```

Now, we’ll map CreateAccountError to CreateUserFailureReason using withExceptT: