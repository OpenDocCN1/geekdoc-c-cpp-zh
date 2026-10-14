```
```haskell
processAjaxResult
  :: V a
  . Show a
  => Decode a
  => Proxy a
  -> Either Ajax.Error (Ajax.Response String)
  -> String

processAjaxResult _ = case _ of
  Left err -> Ajax.printError err
  Right { body } -> case runExcept (decodeJSON body :: _ a) of
    Left err -> show err
    Right reversedRecord -> show reversedRecord
```
```

① Renamed `reverseTeacher` to `reversedRecord`.

At this point, stop to make sure your code matches this then continue.

Next, modify the test code to call `processAjaxResult` before reading any further.

Here’s the change to `test` that leverages `processAjaxResult`:

```
```purescript
import Type.Proxy (Proxy(..)) ①

test :: Effect Unit
test = launchAff_ do
  result <- Ajax.post ResponseFormat.string
    "http://localhost:3000/"
    $ Just $ RequestBody.String $ encodeJSON teacher
  log $ processAjaxResult (Proxy :: _ ReversedTeacher) result ②
```
```

① Added `(..)` to import the `Proxy` Data Constructor.

② Give it a `Proxy` with a Type of `Proxy ReversedTeacher`, but using `_` in place of `Proxy` since the compiler can figure that part out for itself and I want to keep this as readable as possible.

Just for grins, run the test and make sure you get:

```
```text
lanosrep: { ega: (Years 31), thgieh: (Centimeters 162.56), thgieh: (Kilograms 63.5) }, sedarg: [Preschool,Kindergarten,(Grade 1)], stnedutsForebmun: 23, sutats: NonTenured }
```
```