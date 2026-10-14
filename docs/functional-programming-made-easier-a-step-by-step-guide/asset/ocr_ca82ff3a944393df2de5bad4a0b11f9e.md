```
npx spago build
```

Now, write the code to read the file and break it up into lines then return here.

We read the file then map lines over it:

```
import Data.String.Utils (lines) ①
import Node.FS.Aff (exists, writeTextFile, readTextFile) ②

loadAccounts :: Aff (Array Account)
loadAccounts = do
  exists <- try $ exists accountsFile
  when (isLeft exists)
    $ writeTextFile ASCII accountsFile bootstrapAccount
  -- COMPILER WARNING!! ③
  accountLines <- lines <$> readTextFile ASCII accountsFile ④
  pure []
```

① Import lines.

② Added readTextFile to the import list.

③ We're not using accountLinst yet.

④ Map lines over the Aff String we get back from readTextFile.

At this point, we should review our initial plan:

+   - Create initial Accounts File with a Bootstrap Account with a temporary password
+   - Load all Accounts from the File
+   - Append a new Account to the Accounts File

Looks like we're done with the first one and partially on the second.

Next, we'll need to parse each line into an Account. We're going to use a parser library found in the purescript-parsing package.

Add the parsing dependency to your spago.dhall. Then run:

```
npx spago build
```

You're going to get the following warning: