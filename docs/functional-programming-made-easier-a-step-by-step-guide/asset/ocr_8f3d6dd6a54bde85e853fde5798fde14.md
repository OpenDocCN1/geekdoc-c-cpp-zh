```
import Prelude ①

import Control.Monad.Error.Class (try)
import Node.FS.Aff (exists)

accountsFile :: String ②
accountsFile = "accounts.csv"

loadAccounts :: Aff (Array Account)
loadAccounts = do
  --- COMPILER WARNING!! ③
  exists <- try $ exists accountsFile ④
  pure [] ⑤
```

① Add these imports.

② Define the file name so we don’t have to keep typing the literal String, which are just more opportunities for us to mistype it.

③ We’ll ignore the compiler warning since we’re not using exists yet.

④ We try to check for existence. Note that Value exists is an Either.

⑤ This is here to make the compiler happy. We’re returning an empty Array for now.

We’ll need to add node-fs-aff to spago.dhall since we’re importing Node.FS.Aff: