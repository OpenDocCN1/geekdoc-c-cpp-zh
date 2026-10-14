```
import Record (delete) ①
import Type.Proxy (Proxy(..))

handler :: CreateUserRequest -> Handler
handler (CreateUserRequest { authToken, user: user' }) = do ②
    { sessionsAVar } <- ask
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
                    $ passwordHashHex user'.userName user'.password ③
                let user = delete (Proxy :: _ "password") user' ④
                ???
```

① Add these imports.

② Renamed user to user' since it's not REALLY a User.

③ Use user' instead of user.

④ Delete the password field from user' to produce a real User called user.

Next, build an Account Value from the user and the passwordHash using insert from the purescript-record package. Then return here continue on.

Here is the code for creating an Account from user and passwordHash: