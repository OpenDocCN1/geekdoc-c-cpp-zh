```
import Effect.Aff (Aff, launchAff_) ①

test :: Effect Unit
test = launchAff_ do ②
  bus <- Bus.make ③
  ???
```

① Added launchAff_ to import list.

② The body of do now runs in Aff.

③ Luckily, make runs in both Effect and Aff.

At this point, we’re ready to run the Publishers and Subscribers. It’s always best to have the Subscribers run before the Publishers:

```
import Effect.Aff (Aff, launchAff_, forkAff) ①

test :: Effect Unit
test = launchAff_ do
  bus <- Bus.make
  void $ forkAff $ runFiberM bus logger ② ③ ④
  ???
```

① Added forkAff to the import list.

② We’re going to have to add a do-nothing version of logger later.

③ Our Stack has Aff at the bottom, which is what runFiberM returns. That process is forked as a separate process by forkAff.

④ We throw away the Fiber that forkAff returns using void.

Now, we’ll run the Publishers, which will be randomGenerator with a different Predicate for each. In our case, the Predicate is a Function that takes a Number and returns a Boolean:

```
test :: Effect Unit
test = launchAff_ do
  bus <- Bus.make
  void $ forkAff $ runFiberM bus logger -- COMPILER ERROR!
  void $ forkAff $ runFiberM bus $ randomGenerator (_ > 0.5) ① ②
  void $ forkAff $ runFiberM bus $ randomGenerator (_ < 0.5) ① ②
  void $ forkAff $ runFiberM bus $ randomGenerator (_ > 0.1) ① ②
```

① We’re going to have to add a do-nothing version of randomGenerator later.