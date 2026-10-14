```
pure $ fromCharArray (first : rest)

firstName :: AccountParserT String
firstName = properName

lastName :: AccountParserT String
lastName = properName
```

① Make sure the module name is correct.

Now, we can write a Function called accountParser, which will parse each element followed by a comma. Give it a try and see how far you get before reading on.

Here’s our bootstrapAccount as reference:

```
-- userName,passwordHash,temporaryPassword,admin,firstName,lastName
bootstrapAccount :: String
bootstrapAccount = "admin,placeholder,true,true,Joe,Admin"
```

If you got stuck, here’s the first part:

```
accountParser :: AccountParserT Account
accountParser = do
  userName' <- userName # comma ① ② ③
  ???
```

① Here comma is going to be a parser, which we have yet to write, that will take a AccountParserT and combine it with a parser that parses a single comma. The comma, however, will NOT be returned from comma. Instead, it will return whatever the parser it was passed parses.

② Naming the result of the parse with a prime, i.e. userName' since the parser has the same name and we don’t want to shadow it.

③ Call comma at the end using # because the code will read in the same order as we parse, i.e. parse userName and then parse the comma.

Stop reading at this point and see how far you code before returning here.

Here’s the rest of the individual columns: