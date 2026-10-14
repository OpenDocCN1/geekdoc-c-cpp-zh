![](bbox=[0.23, 0.06, 0.77, 0.28])

Now, restart your server. Now, re-logon to the Application and navigate to the Users Page.

Notice how your unique user is MISSING?

This is because of a problem in our parser. To understand why, let’s revisit our parser.

First, there an important thing to notice about accountParser:

```
accountParser :: AccountParserT Account
accountParser = do
  userName' <- userName # comma
  passwordHash' <- passwordHash # comma
  temporaryPassword' <- temporaryPassword # comma
  admin' <- admin # comma
  firstName' <- firstName # comma
  lastName' <- lastName
  pure $ Account
    { userName: userName'
    , passwordHash: passwordHash'
    , temporaryPassword: temporaryPassword'
    , admin: admin'
    , firstName: firstName'
    , lastName: lastName' ①
    }
where
  comma :: ∀ a. AccountParserT a -> AccountParserT a
  comma p = p <* char ','
```

① Notice here that lastName has nothing following it.

Since, nothing follows the lastName, the account line parsers just fine. Had we put McCloud for the firstName, we would’ve gotten a parser error since a name of McCloud is invalid and a comma and lastname follows.