
import Foreign.JSON (parseJSON) ①

test :: Effect Unit
test = launchAff_ do
  results <- parSequence $ (\json -> Ajax.post ResponseFormat.string "http://localhost:3000/" $ Just $ RequestBody.String json)
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
    o <- parseJSON json ② ③
    ???

① Add this import.

② o represents the JSON Object that we’re going to give to _reverseKeys.

③ If this step fails because we give it a bogus JSON String, we won’t crash, but instead it’ll be handled thanks to the underlying ExceptT. Contrast that to our earlier discussion about using JSON.parse in the Javascript code.

If you got stuck, stop reading and see if you can finish this now.

Next, I want to reverse the keys and give those results to decodeJson:

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

① decodeJSON returns an F a so there’s no need for pure here.

And now, we can use processJSON:

```haskell
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
      show (processJSON teacherJson :: _ Teacher) <> "\n\n"
    _ -> show (processJSON studentJson :: _ Student)
    Right _ ->
      "The number of Ajax calls is different than what's being processed."
  where
    processJSON json = runExcept do
      o <- parseJSON json
      decodeJSON $ _reverseKeys o
```

① Use `processJSON` in these 2 places.

Let’s look at that pesky compiler error:

![](img/8c0e9b687c62642e828ccb5481e11313_1266_0.png)

We’ve seen this error before. The compiler is overspecializing again.

Make sure your test code matches the above code.

Then comment out the offending line of code.

And finally, add a Type Signature to `processJSON` with a Type Hole like we did last time to see what Type the compiler infers.

Then take that Type and generalize it. Once that compiles, then you can uncomment out the offending line of code and, hopefully, everything will compile.

Give that a shot and return here when you’re either done or stumped.

Okay, so here’s all of those changes right up to the Type Hole:

```
test :: Effect Unit
test = launchAff_ do
  results <- parSequence $ (\json -> Ajax.post ResponseFormat.string "http://localhost:3000/" $ Just $ RequestBody.String json)
    <$> [
      encodeJSON testTeacher
    , encodeJSON testStudent
    ]
  log $ case map (_ . body) <$> sequence results of
    Left err -> Ajax.printError err
    Right [teacherJson, studentJson] ->
      show (processJSON teacherJson :: _ Teacher) <> "\n\n"
      -- <>  show (processJSON studentJson :: _ Student) ①
    Right _ ->
      "The number of Ajax calls is different than what's being processed."
where
  processJSON :: ?x ②
  processJSON json = runExcept do
    o <- parseJSON json
    decodeJSON $ _reverseKeys o
```

① Commented out the offending line.

② Added Type Signature with a Type Hole.

And here’s the Type it inferred:

```
String -> Either (NonEmptyList ForeignError) Teacher
```

But since:

```
type MultipleErrors = NonEmptyList ForeignError
```

we can reduce it to:

```
String -> Either MultipleErrors Teacher
```

And now, we can generalize this as:

```
∀ a. String -> Either MultipleErrors a
```

Adding that yields:

```
import Foreign (Foreign, MultipleErrors) ①

test :: Effect Unit
test = launchAff_ do
  results <- parSequence $ (\json -> Ajax.post ResponseFormat.string "http://localhost:3000/" $ Just $ RequestBody.String json)
    <$> [
      encodeJSON testTeacher
    , encodeJSON testStudent
    ]
  log $ case map (_.body) <$> sequence results of
    Left err -> Ajax.printError err
    Right [teacherJson, studentJson] ->
      show (processJSON teacherJson :: _ Teacher) <> "\n\n"
      -- <>  show (processJSON studentJson :: _ Student)
    Right _ ->
      "The number of Ajax calls is different than what's being processed."
  where
    processJSON :: ∀ a. String -> Either MultipleErrors a ②
    processJSON json = runExcept do
      o <- parseJSON json
      decodeJSON $ _reverseKeys o -- COMPILER ERROR!!
```

① Added MultipleErrors to import list.

② Added our generalized Type Signature.

And now, another compiler error:

![](img/8c0e9b687c62642e828ccb5481e11313_1269_0.png)

Okay, so unlike our last processJSON, we're calling decodeJSON here, so we'll need to constrain a accordingly:

```
test :: Effect Unit
test = launchAff_ do
  results <- parSequence $ (\json -> Ajax.post ResponseFormat.string "http://localhost:3000/" $ Just $ RequestBody.String json)
    <$> [
      encodeJSON testTeacher
    , encodeJSON testStudent
    ]
  log $ case map (_.body) <$> sequence results of
    Left err -> Ajax.printError err
    Right [teacherJson, studentJson] ->
      show (processJSON teacherJson :: _ Teacher) <> "\n\n"
      <> show (processJSON studentJson :: _ Student) ①
    Right _ ->
      "The number of Ajax calls is different than what's being processed."
  where
    processJSON :: ∀ a. Decode a => String -> Either MultipleErrors a ②
    processJSON json = runExcept do
      o <- parseJSON json
      decodeJSON $ _reverseKeys o
```

① Uncommented.

② Constrain a to have a Decode Instance.

Make these changes to your code (don't forget to uncomment) and run it to see if it works.

And now we have to re-add foreign back to our spago.dhall file:

```
[error] Some of your project files import modules from packages that are not in the direct dependencies of your project.
To fix this error add the following packages to the list of dependencies in your config:
- foreign
```

Once this is fixed, we run it to see if it works. And it does NOT:

```
(Left (NonEmptyList (NonEmpty (ForeignError "Unexpected token o in JSON at position 1") Nil)))

(Left (NonEmptyList (NonEmpty (ForeignError "Unexpected token o in JSON at position 1") Nil)))
```

But why not? Where do we even begin to look?

Well, we can see that the decoding is failing. So, let’s see what we’re giving decodeJSON using spy:

```
import Debug (spy)

-- REDACTED test code above the where section
where
processJSON :: ∀ a. Decode a => String -> Either MultipleErrors a
processJSON json = runExcept do
  o <- parseJSON json
  decodeJSON $ spy "json" $ _reverseKeys o ①
```

① Added spy between decodeJSON and _reverseKeys. Talk about a man-in-the-middle attack.

Make this change and add debug` to your `spago.dhall (if it’s not there).

Now run it and see what prints out in the console. From that, you have enough information to figure this problem out.

It may not be obvious at first. It took me a few minutes, but when it hit me, I felt pretty stupid that I coded this even though it’s an easy mistake to make.

Give it try and see if you can see my mistake.

Here’s a partial listing of the output:
