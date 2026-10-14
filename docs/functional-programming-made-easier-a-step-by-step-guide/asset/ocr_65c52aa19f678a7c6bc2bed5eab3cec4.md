And, of course, a compiler error:

![](bbox=[0.28, 0.095, 0.72, 0.324])

This tells us that the compiler encountered a Tuple but expected a Function. The first thing I ask myself when this happens is what’s different between State and Writer since I copy-pasta’d that code.

And that difference is that Writer contains a Tuple, whereas State contains a Function that returns a Tuple. Let’s fix that:

```
runWriter :: ∀ a w. Writer w a -> Tuple a w ①
runWriter (Writer x) = x ②
```

① Changed (w -> Tuple a w) to Tuple a w.

② Renamed f to x to reflect the fact that Writer contains a Value NOT a Function like State does.

Now we get a compiler error on this line of our test code:

```
test :: Effect Unit
test = do
  log $ show $ runWriter
    (fullNameValid Nothing (Just "") Nothing) [] -- COMPILER ERROR!!
```

Here’s the compiler error: