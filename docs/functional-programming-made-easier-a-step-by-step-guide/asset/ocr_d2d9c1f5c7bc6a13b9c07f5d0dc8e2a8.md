+   ① Added this import.
+   ② Added Encode Constraint on request.

And now we need to constrain response for Decode:

```
import Foreign.Generic.Class (class Encode, class Decode) ①

apiCall :: ∀ request response m
  . MonadAff m
  => Encode request
  => Decode response ②
  => UUID
  -> request
  -> m (Either String response)
-- COMPILER WARNING!!
apiCall authToken request = do
  ajaxResult <- H.liftAff $ Ajax.post ResponseFormat.string
    "http://localhost:3000/"
    $ Just $ RequestBody.String
    $ encodeJSON request
  pure do
    { body } <- lmap Ajax.printError ajaxResult
    lmap show $ runExcept $ decodeJSON body :: _ response
```

+   ① Added class Decode to import list.
+   ② Added Decode Constraint on response.

The compiler is telling us that authToken isn’t used. We needed it to construct QueryResultRequest, but now we’re just passing in the full request, so we can remove this Parameter: