```
test :: Effect Unit
test = launchAff_ do
  parSequence $ (\json -> Ajax.post ResponseFormat.json ①
    "http://localhost:3000/"
    $ Just $ RequestBody.String json) ②
  <$> [
    encodeJSON testTeacher ③
  , encodeJSON testStudent ③
  ]
```

① Renamed Lambda Parameter to json.

② We can pass the json directly as the body of the POST.

③ We encode each different element of the Array to homogenize them, i.e. make them the same Type.

The next step is to retrieve the results from the resulting Array. First, extract the results of the parSequence call and then add a pure unit at the end of the do block to keep the compiler happy for the moment.

Then read on.

Here's those changes:

```
test :: Effect Unit
test = launchAff_ do
  results <- parSequence $ (\json -> Ajax.post ResponseFormat.json ①
    "http://localhost:3000/"
    $ Just $ RequestBody.String json)
  <$> [
    encodeJSON testTeacher
  , encodeJSON testStudent
  ]
  pure unit ②
```

① Extract the results from the Aff (Array a).

② This is here for now to keep the compiler happy. We'll probably delete this later.

Next, ignoring the compiler warning, we need to process results, but before we can do that we need to know results's Type.

How can we figure that out?

If we look up parSequence in Pursuit we see it returns an m (t a) where m is the Monad or in our case Aff and t is the Traversable which is an Array and a is something. That means it returns an Aff (Array