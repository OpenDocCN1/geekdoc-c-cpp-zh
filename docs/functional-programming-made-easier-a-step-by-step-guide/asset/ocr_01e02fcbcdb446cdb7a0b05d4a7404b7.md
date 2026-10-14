```
delayRandom :: Aff Number
 delayRandom = delay (Milliseconds 1000.0) *> randomAff

randomGenerator :: String -> (Number -> Boolean) -> FiberM Unit
randomGenerator valueType pred = do
  { count } <- get
  unless (count <= 0) do
    { bus } <- ask
    liftAffToFiberM do
      n <- delayRandom ①
      when (pred n) $ flip Bus.write bus
      $ "Found a value that is "
        <> valueType <> " (" <> show n <> ")"
    modify_ _ { count = count - 1 }
    randomGenerator valueType pred
```

① This schedules a callback through Javascript, which means our code will not exit before this call returns.

Notice the call to delayRandom. In delayRandom, we call delay, which is ultimately calling Javascript’s setTimeout. This keeps our program alive since we have an outstanding callback that Javascript knows about.

Once we return from delayRandom, we recurse and either exit or call delayRandom again, which keeps our program alive.

In the case of logger, there was a pending callback that only the AVar library knows about. Javascript is none the wiser. So, when all of the Publishers exit, the Javascript Runtime sees that there are no outstanding requests and it promptly exits.

I’m not a huge fan of PureScript on the backend for these kinds of quirky issues. I’d almost always write my backend in Haskell given the chance. But if you’re going to write PureScript and run it under Node, you’ll need to keep these sort of issues in mind.