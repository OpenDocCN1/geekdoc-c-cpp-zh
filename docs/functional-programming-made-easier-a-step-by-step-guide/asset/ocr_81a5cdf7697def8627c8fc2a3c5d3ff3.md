```
test :: Effect Unit
test = launchAff_ do
    results <- parSequence $ (\json -> Ajax.post ResponseFormat.string
        "http://localhost:3000/"
        $ Just $ RequestBody.String json)
        <$> [
            encodeJSON testTeacher
        , encodeJSON testStudent
        ]
    log $ case map (_.body) <$> sequence results of
        Left err -> Ajax.printError err
        Right [teacherJson, studentJson] ->
            show (runExcept $ decodeJSON teacherJson :: _ Teacher) <> "\n\n"
            <> show (runExcept $ decodeJSON studentJson :: _ Student)
        Right _ ->
            "The number of Ajax calls is different than what's being processed."
    where
        processJSON json = runExcept do
            o <- parseJSON json
            decodeJSON $ _reverseKeys o ①
```

① decodeJSON returns an F a so there’s no need for pure here.

And now, we can use processJSON: