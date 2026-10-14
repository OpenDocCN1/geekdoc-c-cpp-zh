We can see that runParserT takes a String to parse and a ParserT. We have both of those things. We have lines from our Accounts File and we have accountParser.

Go ahead and add to our incubation line the code to run accountParser over each line in the Array, i.e. accountLines. Then continue reading.

We're going to map runParserT over accountLines to accomplish this:

```
import Parser.Account (accountParser) ①
import Text.Parsing.Parser (runParserT)

loadAccounts :: Aff (Array Account)
loadAccounts = do
  exists <- try $ exists accountsFile
  when (isLeft exists)
    $ writeTextFile ASCII accountsFile bootstrapAccount
  accountLines <- lines <$> readTextFile ASCII accountsFile
  let x = flip runParserT accountParser <$> accountLines :: ?x ② ③ ④
  pure []
```

① Add these imports.

② We flipped runParserT to give it the parser Parameter before the String to parse.

③ We map over each line in the Array.

④ The Type Hole is Array (Identity (Either ParseError Account)).

We now have an Array of Identity, so go ahead and add code to unwrap the elements before reading on.

We're going to simply compose unwrap with runParserT. We can do this instead of calling map again thanks to the Functor Laws:

```
import Data.Newtype (unwrap) ①

loadAccounts :: Aff (Array Account)
loadAccounts = do
  exists <- try $ exists accountsFile
  when (isLeft exists)
    $ writeTextFile ASCII accountsFile bootstrapAccount
  accountLines <- lines <$> readTextFile ASCII accountsFile
  let x = unwrap
        <<< flip runParserT accountParser <$> accountLines :: ?x ② ③
  pure []
```

① Import unwrap.