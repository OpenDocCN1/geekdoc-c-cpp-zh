```
import Effect.Aff (Aff, delay, launchAff_)

test :: Effect Unit
test = launchAff_ do
  ???
```

① Added launchAff_ to the import list.

② Using launchAff_ to run in Aff. This will make working with Fibers and Affs much easier than working in Effect.

Next, we’ll create the AVar:

```
test :: Effect Unit
test = launchAff_ do
  ttAVar <- AVar.empty ①
  ???
```

① Create this empty. This gives us time to start the Fibers before the clock starts to run.

Next, we’ll start the Clock Fiber and the Bomb Fiber:

```
import Effect.Aff (Aff, delay, launchAff_, forkAff) ①

test :: Effect Unit
test = launchAff_ do
  ttAVar <- AVar.empty ①
  clockFiber <- forkAff $ clock ttAVar
  bombFiber <- forkAff $ bomb ttAVar 3 ②
  ???
```

① Added 'forkAff' to the import list.

② The detinationCount is 3 seconds.

Now that the Fibers are running, we can start the clock. Realize that the Clock Fiber will block when it tries to take the AVar before this step. The same is true for the Bomb Fiber when it tries to read the AVar: