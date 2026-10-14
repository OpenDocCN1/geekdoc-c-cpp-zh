Now, we should review our `CreateUserRequest`:

```
newtype CreateUserRequest = CreateUserRequest
  { authToken :: UUID
  , user :: Record (UserRow ( password :: String ))
  }
```

Here `user` is everything a `User` is plus a `password`.

This means that we can take the `User` fields from the `CreateUserRequest` and compute the `passwordHash` from the `password` to create an `Account` that we can send to `createAccount` for both the Account Manager and Account Handler.

Now that we have a plan, let’s start by writing `createAccount` for the Account Manager, i.e. in the `Manager.Account` module.

Just write the Type Signature and then continue reading.

We’re going to put this in `Manager.Account`:

```
createAccount :: AVar Accounts -> Account -> Aff Unit ❶
```

> ❶ We pass in the `accountsAVar` and an `account`.

Now, just write the left-hand side of the implementation, then read on.

Here’s that addition:

```
createAccount :: AVar Accounts -> Account -> Aff Unit
createAccount accountsAVar account = do
  ???
  pure unit ❶
```

> ❶ Since we’re coding this one line at a time, it can be helpful to keep the compiler happy. That’s why we’ve added this here. Now, we’ll get compiler errors as we code instead of getting them all at the very end. Do NOT forget to delete it.

One thing to note here is that we could’ve chosen to simply pass `CreateUserRequest` instead of `Account`.

Why do you think what we’ve done is better than doing that? Or do you think passing `CreateUserRequest` is better?

If we were to pass `CreateUserRequest` then API changes COULD also break our Account Manager. We want the knowledge of the API to be limited to the API Handler. This is what is meant by Separation of