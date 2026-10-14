```
import Data.Either (Either(..)) ①

test :: Effect Unit
test = launchAff_ do
  result <- Ajax.post ResponseFormat.string
    "http://localhost:3000/"
    $ Just $ RequestBody.String $ encodeJSON teacher
  case result of
    Left err -> Ajax.printError err ②
    Right { body } -> ??? ③ ④
```

① Import Either’s Data Constructors.

② Again, we’re using Ajax.printError to convert Error to a String.

③ We get the Ajax Response in the Right case and destructure the Record to gain access to body.

④ Removed pure unit since we don’t need it anymore.

Next, we call decodeJSON:

```
import Foreign.Generic (encodeJSON, genericEncode, genericDecode
  , defaultOptions, decodeJSON) ①

test :: Effect Unit
test = launchAff_ do
  result <- Ajax.post ResponseFormat.string
    "http://localhost:3000/"
    $ Just $ RequestBody.String $ encodeJSON teacher
  case result of
    Left err -> Ajax.printError err
    Right { body } -> decodeJSON body :: ??? ②
```

① Added decodeJSON to import list.

② We know from last Chapter that we have to explicitly tell the compiler what Type it’s decoding, unless we’re going to use the results of the decode such that the compiler can infer it. In our case, we’re just going to log it, which means the compiler won’t be able to infer its Type.

So, the big question here is what Type is decodeJSON body. Use Pursuit to figure that out. Keep in mind that we’re passing decodeJSON a String. Then return here.

Here’s what I found:

```
decodeJSON :: ∀ a. Decode a => String -> F a
```