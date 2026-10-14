We want to process the Eithers, i.e. results of the Ajax calls, that’s stored in this Array. But one or both could have failed. And if they didn’t fail, we really only care about the body from the Response Record.

How do would you proceed?

Well, we want to convert the Array (Either Error (Response a)) to Either Error (Array (Response a)). This way we either have an Error or an Array of Responses.

Do you remember something that does this?

If not, how about something that takes a t (m a) and makes it a m (t a)?

If still not, then search Pursuit for t (m a) -> m (t a) and see what you get.

I found sequence. Add that to your test code and then extract the bodies from the resulting Either. Do this before reading on.

So, here’s sequence added:

```
import Data.Traversable (sequence) ①

test :: Effect Unit
test = launchAff_ do
  results <- parSequence $ (\json -> Ajax.post ResponseFormat.json
    "http://localhost:3000/"
    $ Just $ RequestBody.String json)
    <$> [
      encodeJSON testTeacher
    , encodeJSON testStudent
    ]
  bodies <- sequence results --- COMPILER ERROR!! ②
  pure unit
```

① Import sequence.

② Added sequence.

Here’s the compiler error: