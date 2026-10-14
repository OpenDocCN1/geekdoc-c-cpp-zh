```
```haskell
test :: Effect Unit
test = launchAff_ do
  results <- parSequence $ (\\json -> Ajax.post ResponseFormat.string
      "http://localhost:3000/"
      $ Just $ RequestBody.String json)
    <$> [
      encodeJSON testTeacher
    , encodeJSON testStudent
    ]
  log $ case map (\_.body) <$> sequence results of
    Left err -> Ajax.printError err
    Right [teacherJson, studentJson] ->
      show (processJSON teacherJson :: _ Teacher) <> "\n\n"
    _ -> show (processJSON studentJson :: _ Student)
    Right _ ->
      "The number of Ajax calls is different than what's being processed."
  where
    processJSON json = runExcept do
      o <- parseJSON json
      decodeJSON $ _reverseKeys o
```
```

① Use `processJSON` in these 2 places.

Let’s look at that pesky compiler error:

![](bbox=[0.279, 0.592, 0.721, 0.784])

We’ve seen this error before. The compiler is overspecializing again.

Make sure your test code matches the above code.

Then comment out the offending line of code.

And finally, add a Type Signature to `processJSON` with a Type Hole like we did last time to see what Type the compiler infers.