```
import Manager.Account (findAccount, createAccount) ①

handler :: CreateUserRequest -> Handler
handler (CreateUserRequest { authToken, user: user' }) = do
    { accountsAVar, sessionsAVar } <- ask ②
    verifiedSession <- lift $ verifySession sessionsAVar authToken
    response <- case verifiedSession of
        Nothing -> CreateUserResponse
            $ CreateUserResultsFailure { reason: NotAuthenticated }
        Just (Session { userName }) -> do
            admin <- lift $ findAccount accountsAVar userName
                <#> maybe false (\(Account a) -> a.admin)
            if not admin then pure CreateUserResponse
                $ CreateUserResultsFailure { reason: NotAuthorized }
            else do
                passwordHash <- lift
                    $ passwordHashHex user'.userName user'.password
                let user = delete (Proxy :: _ "password") user'
                    account = Account $
                        insert (Proxy :: _ "passwordHash") passwordHash user
                result <- lift $ createAccount accountsAVar account ③
                ???
```

① Add createAcccount to import list.

② Also ask for accountsAVar.

③ Create the account capturing the result.

Next, we need to handle the 2 cases from createAccount. Here’s the CreateAccountResults definition for reference:

```
data CreateAccountResult
    = CreateAccountSuccess
    | CreateAccountAlreadyExists
```

Now we’ll handle the error case first: