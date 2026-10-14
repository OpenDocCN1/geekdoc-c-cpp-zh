② Added error :: String -> Error. This is passed to the Fiber upon canceling. We’ll do Canceler handling later.

③ This is Point-free where the Fiber is the unnamed Parameter.

④ The Error is constructed using error. This error will be passed to the Canceler, i.e. the Fiber’s abortion handler. More on this later.

Second, we’ll write some test code to run everything:

```
import Effect (Effect) ①
import Effect.Aff (Aff, Fiber, delay, killFiber, launchAff_, forkAff) ②

test :: Effect Unit
test = launchAff_ do ③
  logger <- forkAff logEverySecond ④
  fileReader <- forkAff readAFileAfterTwoSeconds ④
  delay (Milliseconds 5000.0) ⑤
  kill logger ⑥
  kill fileReader ⑥
```

① Import Effect for test.

② Added launchAff_ and forkAff.

③ Ultimately our program runs in Effect, which is why test runs in Effect. But, we want to run our Fibers in Aff, so we launch an Asynchronous Process using launchAff_. We’re using launchAff_ :: Effect Unit instead of launchAff :: Effect (Fiber a) since we don’t care about the Fiber that this process runs in.

④ We fork these 2 processes capturing their Fibers so we can kill them later.

⑤ Sleep for 5 seconds.

⑥ Kill our 2 processes. Chances are that the fileReader has already exited, but it doesn’t hurt to do this just in case.

The above code uses 2 different ways to start an Asynchronous Process, launchAff_ and forkAff. Their differences can be seen from their Type Signatures:

```
launchAff_ :: ∀ a. Aff a -> Effect Unit
forkAff :: ∀ a. Aff a -> Aff (Fiber a)
```

Since test is running in the Effect Monad, we have to use launchAff_. Once we’re in the Aff Monad, we can use forkAff.

When this code is run, we get the following output: