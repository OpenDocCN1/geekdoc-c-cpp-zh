```
apiCall :: V request response m
  . MonadAff m
  => Encode request
  => Decode response
  => request ① ②
  -> m (Either String response)
apiCall request = do ③
  ajaxResult <- H.liftAff $ Ajax.post ResponseFormat.string
    "http://localhost:3000/"
    $ Just $ RequestBody.String
    $ encodeJSON request
  pure do
    { body } <- lmap Ajax.printError ajaxResult
    lmap show $ runExcept $ decodeJSON body :: _ response
```

+   ① Removed the UUID Type Parameter.
+   ② Changed -> to =>.
+   ③ Removed authToken Parameter.

We also can delete the import:

```
import Data.UUID (UUID)
```

Looking at apiCall, I’m wondering if the explicit Type Signature on the following line is really necessary anymore:

```
lmap show $ runExcept $ decodeJSON body :: _ response
```

Let’s take it out and see if the compiler can figure it out without our help.

Turns out that it can: