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