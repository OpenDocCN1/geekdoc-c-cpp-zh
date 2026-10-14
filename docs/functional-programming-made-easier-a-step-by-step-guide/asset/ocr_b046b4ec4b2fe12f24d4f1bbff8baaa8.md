It appears to me that `const QueryUsersResultsSuccess` is expecting `{ users :: Array User } -> QueryUsersResults` but got `QueryUsersResults` instead.

Can you see why that is?

It’s because of this line:

```
pure $ QueryUsersResultsSuccess { users }
```

> In the success case, we return `QueryUsersResults` unlike what we did in `CreateUsers` where we’ve been stealing code from. In `CreateUsers`, we simply returned `unit` via the `AH.createAccount` call.

Because we’re returning something different than we did in `CreateUsers`, this line will need to change:

```
(ok <<< const QueryUsersResultsSuccess)
```

We can simply respond using `ok` since we already have a `QueryUsersResultsSuccess`:

```
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
      let users = accounts <#> \(Account r) =>
            User $ delete (Proxy :: _ "passwordHash") r
      pure $ QueryUsersResultsSuccess { users }
  let ok = HTTPure.ok <<< encodeJSON <<< QueryUsersResponse
  result # either
    (ok <<< \reason -> QueryUsersResultsFailure { reason })
    ok
```

> Removed `const` Function.

Now, that compiles.

That’s the danger of copying code. It turns out that we used `const` in `CreateUser` since `CreateUserResultsSuccess` doesn’t take any Parameters, hence the use of `const` to throw away