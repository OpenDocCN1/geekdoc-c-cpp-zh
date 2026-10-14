
accountsParser is a parser that returns an Array of Accounts.

And now write the rest of the parser until you get stuck or finish. Then keep reading.

The next part is to use sepBy:

```
import Text.Parsing.Parser.Combinators (sepBy) ①

accountsParser :: AccountParserT (Array Account)
-- COMPILER ERROR!!
accountsParser = accountParser `sepBy` char '\n' ②
```

① Added this import.

② We're using sepBy infix for readability.

The compiler error is because we haven't converted the List that sepBy gives us to an Array to match our Type Signature.

If you didn't finish stop now and make this final change before reading on.

```
import Data.Array (many, some, (:), fromFoldable) ①

accountsParser :: AccountParserT (Array Account)
accountsParser = accountParser `sepBy` char '\n' <#> fromFoldable ②
```

① Added fromFoldable to import list.

② Map fromFoldable over the parser. This takes the List that sepBy gives us and maps it to an Array.

Now, we need to find where accountParser is currently called and replace it with accountsParser.

Search your code for where it's called, then return here.

I found it here in Handler.Account:

```
loadAccounts :: Aff (Either ParseError (Array Account))
loadAccounts = do
  exists' <- try $ exists accountsFile
  let exists = case exists' of
    Left _ -> false
    Right b -> b
  unless exists do
    bsa <- bootstrapAccount
    writeTextFile ASCII accountsFile bsa
  accountLines <- lines <$> readTextFile ASCII accountsFile ①
  pure $ sequence
    $ unwrap <<< flip runParserT accountParser <$> accountLines ②
```

① This line needs to be rewritten since we don’t want to break the file up into lines anymore since we’re going to parse the whole thing.

② This line needs to be rewritten to use our new parser.

First step is to comment out the lines we’re going to rewrite and then add something to the end of this Function to keep the compiler happy.

Go ahead and do that before returning here.

Here’s those changes:

```
loadAccounts :: Aff (Either ParseError (Array Account))
loadAccounts = do
  exists' <- try $ exists accountsFile
  let exists = case exists' of
    Left _ -> false
    Right b -> b
  unless exists do
    bsa <- bootstrapAccount
    writeTextFile ASCII accountsFile bsa
  -- accountLines <- lines <$> readTextFile ASCII accountsFile ①
  -- pure $ sequence
  -- $ unwrap <<< flip runParserT accountParser <$> accountLines ①
  pure $ Right [] ②
```

① Commented this out since we’re going to rewrite them.

② Added an empty Array wrapped in an Either using Right and then wrapped in Aff with pure.

Now, read the file data but this time don’t break them up into lines using lines. Put it into a Variable called fileData. Make this one change and then return here.

Here’s that change:

```
loadAccounts :: Aff (Either ParseError (Array Account))
loadAccounts = do
  exists' <- try $ exists accountsFile
  let exists = case exists' of
    Left _ -> false
    Right b -> b
  unless exists do
    bsa <- bootstrapAccount
    writeTextFile ASCII accountsFile bsa
  fileData <- readTextFile ASCII accountsFile ①
  -- accountLines <- lines <$> readTextFile ASCII accountsFile
  -- pure $ sequence
  -- $ unwrap <<< flip runParserT accountParser <$> accountLines
  pure $ Right []
```

① Here we read the whole file into fileData with no post-processing.

Next, add the following to the code:

```
loadAccounts :: Aff (Either ParseError (Array Account))
loadAccounts = do
  exists' <- try $ exists accountsFile
  let exists = case exists' of
    Left _ -> false
    Right b -> b
  unless exists do
    bsa <- bootstrapAccount
    writeTextFile ASCII accountsFile bsa
  fileData <- readTextFile ASCII accountsFile
  let x = ??? :: ?x ①
  -- accountLines <- lines <$> readTextFile ASCII accountsFile
  -- pure $ sequence
  -- $ unwrap <<< flip runParserT accountParser <$> accountLines ②
  pure $ Right []
```

① Add this line minus the ???.

② Use this line for reference.

The ??? is where you’re going to incubate the parsing code we’re going to eventually replace the pure $ Right [] with.

The Type Hole will help us keep track of our Types.

Go ahead and add code where the ??? is to run accountsParser using runParserT before reading on.

Here’s just that:

```
import Parser.Account (accountsParser) ①

loadAccounts :: Aff (Either ParseError (Array Account))
loadAccounts = do
  exists' <- try $ exists accountsFile
  let exists = case exists' of
    Left _ -> false
    Right b -> b
  unless exists do
    bsa <- bootstrapAccount
    writeTextFile ASCII accountsFile bsa
  fileData <- readTextFile ASCII accountsFile
  let x = runParserT fileData accountsParser :: ?x ②
  -- accountLines <- lines <$> readTextFile ASCII accountsFile
  -- pure $ sequence
  -- $ unwrap <<< flip runParserT accountParser <$> accountLines
  pure $ Right []
```

① Added accountsParser to the import list. Also, removed accountParser.

② The Type Hole is Identity (Either ParseError (Array Account)).

Now, add code to our test line to eliminate the Identity. Then return to reading.

Here’s just that addition:

```
```haskell
loadAccounts :: Aff (Either ParseError (Array Account))
loadAccounts = do
  exists' <- try $ exists accountsFile
  let exists = case exists' of
        Left _ -> false
        Right b -> b
  unless exists do
    bsa <- bootstrapAccount
    writeTextFile ASCII accountsFile bsa
  fileData <- readTextFile ASCII accountsFile
  let x = unwrap $ runParserT fileData accountsParser :: ?x
  -- accountLines <- lines <$> readTextFile ASCII accountsFile
  -- pure $ sequence
  --   $ unwrap <<< flip runParserT accountParser <$> accountLines
  pure $ Right []
```
```

❶ The Type Hole is `Either ParseError (Array Account)`.

We almost have what we need. You can see this by looking at what `loadAccounts` is supposed to return.

Add the last bit of code to make that happen and then keep reading.

Here’s that change:

```
```haskell
loadAccounts :: Aff (Either ParseError (Array Account))
loadAccounts = do
  exists' <- try $ exists accountsFile
  let exists = case exists' of
        Left _ -> false
        Right b -> b
  unless exists do
    bsa <- bootstrapAccount
    writeTextFile ASCII accountsFile bsa
  fileData <- readTextFile ASCII accountsFile
  -- COMPILER ERROR:!
  let x = pure $ unwrap $ runParserT fileData accountsParser :: ?x
  -- accountLines <- lines <$> readTextFile ASCII accountsFile
  -- pure $ sequence
  --   $ unwrap <<< flip runParserT accountParser <$> accountLines
  pure $ Right []
```
```

❶ Added `pure`.

Here’s the compiler error:

It underlines the `pure` since it cannot determine the `Applicative`. That’s because we’ve put this in a `let` statement, so it could be any `Applicative`.

Let’s tell the compiler which `Applicative` by changing the Type hole from `?x` to `Aff ?x`. Do this and see what you get.

Here’s what I get for the Type Hole:

That means that our incubated line of code has Type: `Aff (Either ParseError (Array Account))`, which is exactly what we need.

Replace the final line with the incubated code and then remove the `let` line. Then return here and continue on.

Here’s that final change:

```
loadAccounts :: Aff (Either ParseError (Array Account))
loadAccounts = do
  exists <- try $ exists accountsFile
  let exists = case exists' of
        Left _ -> false
        Right b -> b
  unless exists do
    bsa <- bootstrapAccount
    writeTextFile ASCII accountsFile bsa
  fileData <- readTextFile ASCII accountsFile
  -- accountLines <- lines <$> readTextFile ASCII accountsFile
  -- pure $ sequence $ unwrap <<< flip runParserT accountParser <$> accountLines
  pure $ unwrap $ runParserT fileData accountsParser
```

> ① Here’s the line we incubated in a `let` definition with a Type Hole.

At this point, you’ll be able to remove the following imports:

```
import Data.String.Utils (lines)
import Data.Traversable (sequence)
```

Now run the server and see what the error message says now.

First I got:

```
[warn] None of your project files import modules from some projects that are
in the direct dependencies of your project.
These dependencies are unused. To fix this warning, remove the following
packages from the list of dependencies in your config:
- stringutils
```

Remove `stringutils` from `spago.dhall`.

After that I got:

```
Cannot load accounts: (ParseError "Unexpected EOF" (Position { line: 2,
column: 1 })) ❶
```

❶ Notice the line number is 2 now. That’s because we’re parsing all the lines not just one at a time. This is
far better since we know which line in the file is a problem.

It was just as I suspected. Empty lines are a problem.

So, let’s allow for an empty line in our parser.

Let’s look back at our parser:

```
accountsParser :: AccountParser (Array Account)
accountsParser = accountParser `sepBy` char '\n' <#> fromFoldable
```

We need to parse with accountParser OR a parser that parses nothing. Do you remember how to do an OR
with parsers?

How about how to select between 2 parsers?

To do this we use `alt` or more commonly we use it’s Binary Operator, <|>.

Now, we need a parser that doesn’t consume anything from the `String`. Can you remember what we wrote
like this when we wrote our `Parser`?
