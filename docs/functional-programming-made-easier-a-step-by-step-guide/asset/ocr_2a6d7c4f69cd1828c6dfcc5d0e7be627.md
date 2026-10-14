```
gauntlet :: Int -> Maybe Int
gauntlet x = do
  o <- oddTest x
  let y = o + 1
  if o .&. 1 == 0 then do ① ②
    z <- greaterThanTest 10 y
    lessThanTest 20 z
  else
    Nothing
```

① I realize that this test is redundant. It’s only here to demonstrate how if expressions work in a do block.

② Notice how we start a new do block under the then section. That’s because we have multiple steps to complete in the section. Not so under the else section where we handle the error case.

You may have noticed that I’ve been using different variables to hold the result of our tests. But if you remember our tests all return the original value in a Maybe UNCHANGED.

This means I can write the following code:

```
gauntlet :: Int -> Maybe Int
gauntlet x = do
  o <- oddTest x
  let y = o + 1
  greaterThanTest 10 y --- COMPILER ERROR!!
  lessThanTest 20 y
```

But we get a compiler error:

![](bbox=[0.23, 0.65, 0.77, 0.89])

This is because we are discarding the result of a computation in a do block. You might remember in early Chapters we added the Function discard to our Prelude imports. The discard Function is automatically