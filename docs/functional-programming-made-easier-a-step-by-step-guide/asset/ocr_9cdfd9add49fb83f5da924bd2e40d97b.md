Now, rerun the test, i.e. send LogonRequest first. Then take the authToken and copy and paste it into the CreateUserRequest. Then send that.

After that, check accounts.csv. It should have our new account on it’s own line.

Now, before we shutdown the server, try to send the CreateUserRequest one more time and see what you get.

Here’s what I got:

```
{"contents":{"contents":{"reason":{"tag":"AlreadyExists"},"tag":"CreateUserResultsFailure"},"tag":"CreateUserResponse"}
```

Now, shutdown the server and restart it to make sure that it reads accounts.csv correctly.

And it does!

# 28.10.4. Coding QueryUsers API Handler

Querying the users should be pretty easy since we have everything in place for what we’ll need. Our basic plan will be to get the Accounts from the Account Manager and convert them from Accounts to Users and then return that to the client.

To prepare to write the API handler, we’ll first write a Function called getAccounts in Manager.Account.

Write only the Type Signature and then continue reading.

Here’s the Type Signature:

```
getAccounts :: AVar Accounts -> Aff (Array Account)
```

That Type Signature says it all. We give the Function an AVar of Accounts, which, don’t forget, is a Map, and it’ll give us back just an Array of the Accounts.

Take the time to write this now. Then return here if you get stuck or when you’re finished.

We’ll write the left-hand side of the equal sign next:

```
getAccounts :: AVar Accounts -> Aff (Array Account)
getAccounts accountsAVar = ???
```

And now we can just use AVar.read to get the Array of Accounts: