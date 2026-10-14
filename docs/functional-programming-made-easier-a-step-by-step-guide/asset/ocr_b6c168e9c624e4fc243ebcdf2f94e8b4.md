```
import Data.Maybe (Maybe(..), maybe) ①

staticFiles :: Request -> ResponseM
staticFiles { path } =
    let fileName =
        if null path then "index.html"
        else intercalate "/" path in
mimeType fileName # maybe HTTPure.forbidden \mime -> do
    ???
```

① Added maybe to the import list.

② Use our mimeType Function to look up the MIME Type for the fileName. We’ll respond with forbidden or 403 if not found. Otherwise the Lambda is called with the MIME Type, mime.

And now, we’re ready to read the whole file:

```
import Control.Monad.Error.Class (try) ①
import Node.Encoding (Encoding(..))
import Node.FS.Aff (readTextFile)

staticFiles :: Request -> ResponseM
staticFiles { path } =
    let fileName =
        if null path then "index.html"
        else intercalate "/" path in
mimeType fileName # maybe HTTPure.forbidden \mime -> do
    fileData' <- try $ readTextFile ASCII $ staticRoot <> "/" <> fileName ②
    ???
```

① Added these imports.

② Reading file with prepended staticRoot on the front of the fileName. Use try so we can properly handle exceptions. Same caveat with Windows as with any File Path.

And now we handle the error case: