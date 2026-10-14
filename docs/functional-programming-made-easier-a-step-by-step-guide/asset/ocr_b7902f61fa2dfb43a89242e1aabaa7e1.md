```
createAccount :: AVar Accounts -> Account -> Aff CreateAccountResult
createAccount accountsAVar account@(Account { userName }) = do
  withAVar accountsAVar ①
    \accounts -> pure $ ②
      if Map.member userName accounts then ③
        Tuple accounts CreateAccountAlreadyExists
      else
        Tuple (Map.insert userName account accounts) CreateAccountSuccess
```

① We call withAVar passing in the accountsAVar.

② The original logic was a Pure Computation so we wrap it in Aff using pure.

③ Our if logic doesn’t change.

It’s nice that we incubated withAVar in this module, but it really doesn’t belong here. Besides, it would be nice to use it in verifySession.

So, we’re going to move it to a File called Utils.purs. Create that File under the src Folder and move withAVar and the appropriate imports.

Then remove the following import from Manager.Account:

```
import Effect.Aff.Class (class MonadAff, liftAff)
```

And add:

```
import Utils (withAVar)
```

Return here when you’ve completed these tasks.

Here’s Utils.purs: