```
accountToCSV :: Account -> String
accountToCSV (Account
    { userName
    , passwordHash
    , temporaryPassword
    , admin
    , firstName
    , lastName }) =
intercalate ","
    [ userName
    , passwordHash
    , show temporaryPassword
    , show admin
    , firstName
    , lastName
    ] <> "\n" ①
```

① Appended \n to the CSV line.

Now, we’ve got a bad accounts.csv. So delete it. Don’t worry our server will recreate it if it’s missing.

Now, kill your server and rerun it with:

```
npx spago run
```

Now, rerun the test then go check the file to see how it looks. Then return here.

Okay, that didn’t work for me. It put a newline on the end of the CreateUser account, but it’s missing from the first line, i.e. our bootstrapAccount.

Let’s look at how the bootstrapAccount is created:

```
bootstrapAccount :: Aff String
bootstrapAccount = do
  let userName = "admin"
      password = "admin"
  passwordHash <- passwordHashHex userName password
  let true' = show true
  pure $ intercalate ","
    [ userName , passwordHash , true' , true' , "Joe", "Admin" ]
```

And now it’s clear that this is NOT using the accountToCSV Function. It should be. Change