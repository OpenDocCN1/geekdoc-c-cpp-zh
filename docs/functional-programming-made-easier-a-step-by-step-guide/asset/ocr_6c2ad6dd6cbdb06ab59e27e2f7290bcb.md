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