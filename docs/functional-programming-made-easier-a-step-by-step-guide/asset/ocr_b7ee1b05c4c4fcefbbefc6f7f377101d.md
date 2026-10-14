```
data CreateAccountError = CreateAccountAlreadyExists
```

Go to Manager.Account and replace the CreateAccountResult with CreateAccountError.

And now, we’ll make createAccount in the same module return Aff (Either CreateAccountError Unit):

```
import Data.Either (Either(..)) ①

createAccount
  :: AVar Accounts
  -> Account
  -> Aff (Either CreateAccountError Unit) ②
createAccount accountsAvar account@(Account { userName }) = do
  withAvar accountsAvar
    \accounts -> pure $
      if Map.member userName accounts then
        Tuple accounts (Left CreateAccountAlreadyExists) ③
      else
        Tuple (Map.insert userName account accounts) (Right unit) ④
```

① Added this import.

② Changed the return Type.

③ Wrap in a Left.

④ Wrap unit in a Right. Deleted the CreateAccountSuccess.

Make these changes to Manager.Account.

And now, while we’re at it, let’s do the same for the Account Handler’s createHandler in Handler.Account:

```
data CreateAccountError = CreateAccountFileError String ① ②

createAccount :: Account -> Aff (Either CreateAccountError Unit) ③
createAccount account = lmap show
  <$> (try $ appendTextFile ASCII accountsFile $ accountToCSV account)
  <#> lmap CreateAccountFileError ④ ⑤
```

① New Type for errors.

② Don’t forget to delete CreateAccountResult.

③ Changed return Type.