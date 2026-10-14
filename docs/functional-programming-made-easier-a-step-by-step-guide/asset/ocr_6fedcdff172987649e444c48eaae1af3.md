```
accountParser :: AccountParserT Account
accountParser = do
    userName' <- userName # comma
    passwordHash' <- passwordHash # comma
    temporaryPassword' <- temporaryPassword # comma
    admin' <- admin # comma
    firstName' <- firstName # comma
    lastName' <- lastName ①
    ???
```

① Notice there is NO comma call here. That because this is at the end of the line.

Now, add the code to return an Account. Consult the Account Data Constructor to see how to do this before reading any more.

Here’s the construction of an Account:

```
import Entity.Account (Account(..)) ①

accountParser :: AccountParserT Account
accountParser = do
    userName' <- userName # comma
    passwordHash' <- passwordHash # comma
    temporaryPassword' <- temporaryPassword # comma
    admin' <- admin # comma
    firstName' <- firstName # comma
    lastName' <- lastName
    pure $ Account ②
        { userName: userName'
        , passwordHash: passwordHash'
        , temporaryPassword: temporaryPassword'
        , admin: admin'
        , firstName: firstName'
        , lastName: lastName'
        }
where
    comma p = ???
```

① Include Account Data Constructor.

② Had to use the verbose syntax here since local names and field names collide with the parser names. We could rename the parser functions to shrink this, but probably six to one half dozen of the other.

Now, write the comma Parser Combinator, i.e. a Function that takes a parser and returns another parser.