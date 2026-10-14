
❷ The Predicates come straight from the specifications.

Let’s comment out all the lines with `logger` and `randomGenerator` for now since we haven’t written them yet. This way other compiler errors will show as we code until we are ready to write them:

```
```haskell
test :: Effect Unit
test = launchAff_ do
  bus <- Bus.make
  -- void $ forkAff $ runFiberM bus logger
  -- void $ forkAff $ runFiberM bus $ randomGenerator (_ > 0.5)
  -- void $ forkAff $ runFiberM bus $ randomGenerator (_ < 0.5)
  -- void $ forkAff $ runFiberM bus $ randomGenerator (_ > 0.1)
  pure unit
```
```

❶ Had to add this since a `do` block must end with an Expression.

Now, it’s clear that we’re always doing `void $ forkAff $` for each `Fiber`. We can factor that out into `runFiberM`.

Go ahead and move that code to `runFiberM` before moving forward.

Here is the change:

```
```haskell
-- COMPILER ERROR!
runFiberM :: BusRW String -> FiberM Unit -> Aff (Tuple Unit State)
runFiberM bus = void <<< forkAff
  <<< flip runStateT { count: 10 }
  <<< flip runReaderT { bus }
```
```

❶ Notice how we’ve changed `void $ forkAff` to `void <<< forkAff` to keep `runFiberM` Point-free.

We’ll return to this compiler error in a moment.

For now, though, we’ll remove the duplicate code from `test` since it’s been factored out into `runFiberM`:

```
```haskell
test :: Effect Unit
test = launchAff_ do
  bus <- Bus.make
  -- runFiberM bus $ logger
  -- runFiberM bus $ randomGenerator (_ > 0.5)
  -- runFiberM bus $ randomGenerator (_ < 0.5)
  -- runFiberM bus $ randomGenerator (_ > 0.1)
  pure unit
```
```

We're keeping these lines commented out for now.

Notice that we had to pass bus to runFiberM. We could factor that out too:

```
test :: Effect Unit
test = launchAff_ do
  bus <- Bus.make
  let forkFiberM = runFiberM bus ①
  -- forkFiberM logger
  -- forkFiberM $ randomGenerator (_ > 0.5)
  -- forkFiberM $ randomGenerator (_ < 0.5)
  -- forkFiberM $ randomGenerator (_ > 0.1)
  pure unit
```

① This somewhat reduces the noise.

And now we're ready to deal with the compiler error on runFiberM, which shouldn't be too surprising since we've changed the output:

![](img/8c0e9b687c62642e828ccb5481e11313_1058_0.png)

The compiler is expecting a Unit but got a Tuple Unit State. This is because we called void which voids the Tuple. Let's fix that:

```
runFiberM :: BusRW String -> FiberM Unit -> Aff Unit ①
runFiberM bus = void <<< forkAff
  <<< flip runStateT { count: 10 }
  <<< flip runReaderT { bus }
```

① We don't need the Tuple import any more since we replaced Tuple Unit State with Unit.

Don't forget to remove the Data.Tuple import.

Let' uncomment out the code in test:

```
```text
test :: Effect Unit
test = launchAff_ do
  bus <- Bus.make
  let forkFiberM = runFiberM bus
  forkFiberM logger
  forkFiberM $ randomGenerator (_ -> 0.5)
  forkFiberM $ randomGenerator (_ < 0.5)
  forkFiberM $ randomGenerator (_ > 0.1)
```
```

❶ Deleted the `pure unit` since the final call to `forkFiberM` is a valid Expression to terminate our `do`.

Now we have a compiler error in our test code since we’ve not written `logger` yet. So, go ahead and create a do-nothing version of `logger` remembering to use `pure unit`.

Once you’ve done that, continue reading.

First, we write the Type Signature for `logger`:

```
```text
logger :: Aff Unit
```
```

And finally, the do-nothing implementation:

```
```text
logger :: Aff Unit
logger = pure unit
```
```

Now, the compiler should be pointing to the fact that `randomGenerator` is missing. Write that as a do-nothing Function as well. Don’t forget that it takes a Parameter. Then continue on.

Here’s its Type Signature:

```
```text
randomGenerator :: (Number -> Boolean) -> Aff Unit ❶
```
```

❶ First Parameter is a Predicate.

Now, we’ll add the same do-nothing code:

```
```text
randomGenerator :: (Number -> Boolean) -> Aff Unit
randomGenerator pred = pure unit ❶
```
```

❶ We’ve put in the Parameter `pred` even though it’s not used yet.

But now we have an unexpected compiler error on `logger` in our test code:

![](img/8c0e9b687c62642e828ccb5481e11313_1060_0.png)

Can you see where I went wrong?

I forgot that we’re not running in Aff. We are running in our Stack, i.e. what we called FiberM. So, I’ve used the wrong Monad on logger. Now that I think about it, randomGenerator is wrong too.

Let’s fix my mistakes:

```
logger :: FiberM Unit ①
logger = pure unit

randomGenerator :: (Number -> Boolean) -> FiberM Unit ①
randomGenerator pred = pure unit
```

① Changed Aff to FiberM since our Fibers run in the FiberM Monad, i.e they run in the Monad Stack defined by FiberM.

And now this compiles clean sans the warning that we aren’t using pred. We will soon enough.

Now, what should we write?

Well, we have to write logger and randomGenerator and once we do that we’re done. So, I’m going to suggest you start with logger since it’s simpler.

Here’s the logger specification for reference:

```
Subscribers will listen to the `Bus` and log the data they get from the `Bus` to the console. There will be 1 Subscriber.
```

So, code logger before you continue reading on.

We currently have the following:

```
logger :: FiberM Unit
logger = pure unit
```

We need to replace the pure unit with real code. We’re going to start with a do block:

```
logger :: FiberM Unit
logger = do
  ???
```

The next thing we want to do is read from the Bus. But how do we get the Bus? Remember that it’s not passed to us.

We could pass it to this Function, but we’re running in a Stack with ReaderT and our Config has a Bus in it:

```
type Config = { bus :: BusRW String }
```

This means we can read it from ReaderT. Do you remember how to do this?

To do this, we do the following:

```
import Control.Monad.Reader.Trans (ReaderT, runReaderT, ask) ①

logger :: FiberM Unit
logger = do
  { bus } <- ask ②
  ???
```

① Added ask to the import list.

② Read Config from ReaderT. Since it’s a Record, we destructure it into a Variable called bus.

Next, we need to read from the Bus:

```
logger :: FiberM Unit
logger = do
  { bus } <- ask
  s <- Bus.read bus ①
  ???
```

① This runs in Aff!!

But wait. Bus.read runs in Aff, but we’re coding in FiberM. That means we need to lift this Function from

MonadEffect. Then return here.

It turns out that ReaderT has a MonadEffect Instance. In fact, all the Monad Transformers do. And because of this, log will run in ReaderT meaning that it does NOT require any lifting.

Next, we need to loop forever:

```
logger :: FiberM Unit
logger = do
  { bus } <- ask
  s <- lift $ lift $ Bus.read bus
  log $ "Logger: " <> s
  logger
```

And while this will work, the infinite recursion can get lost if our Function is large. Not ideal. But there is a better solution:

```
import Control.Monad.Rec.Class (forever) ①

logger :: FiberM Unit
logger = forever do ②
  { bus } <- ask
  s <- lift $ lift $ Bus.read bus
  log $ "Logger: " <> s
```

① Need to import forever.

② Using forever at the top of the do block makes it immediately clear that we have an infinite recursion.

Now, let’s fix the ugly lift $ lift $ part.

Write a function called liftAffToFiberM to lift an Aff to FiberM. Use the Natural Transformation syntax in the Type Signature, i.e. ~>, since both are Monads and all Monads are Functors.

Code this and then continue on.

The code for this is very simple but will factor out the ugliness in our code:

```
liftAffToFiberM :: Aff ~> FiberM ①
liftAffToFiberM = lift <<< lift ②
```

① Use Natural Transformation syntax, which is equivalent to ∀ a. Aff a -> FiberM a.

② Lift twice. With our Stack, we’re first lifting the base Monad, Aff, to StateT and then ReaderT.

probably won’t need it since we only have to do 2 things, which almost always looks better using a bind.

I could be wrong, so we’ll write it with do to start and improve it afterwards if need be:

```
delayRandom :: Aff Number
delayRandom = do
  ???
```

Next, we delay 1000 milliseconds:

```
import Data.Time.Duration (Milliseconds(..)) ①
import Effect.Aff (Aff, launchAff_, forkAff, delay) ②

delayRandom :: Aff Number
delayRandom = do
  delay $ Milliseconds 1000.0 ③
  ???
```

① Import Milliseconds Type with its Data Constructors.

② Added delay to the import list.

③ The Data Constructor, Milliseconds, wants a Number, i.e. 1000.0 NOT an Int, which would be 1000 without a decimal point.

And now, we can generate our Random Number:

```
delayRandom :: Aff Number
delayRandom = do
  delay $ Milliseconds 1000.0
  randomAff ①
```

① randomAff returns Aff Number so there’s no need for pure here.

Just as I suspected, the do block can be reduced to a single line of code. Rewrite delayRandom by using >>= and then we’ll see how to remove the Lambda. Try it first, then read on.

Here’s delayRandom using bind:

```
delayRandom :: Aff Number
delayRandom = delay (Milliseconds 1000.0) >>= \_ -> randomAff ①
```

① We’ve dropped the $ since we only want the Milliseconds to be Parenthesized, not the whole right side of the line.
