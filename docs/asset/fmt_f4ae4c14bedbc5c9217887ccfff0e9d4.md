
Callbacks can only do Side-effects since it returns `Effect Unit`.

This is the limitation of running in Node or more specifically in Javascript. It only has a single thread of execution at a time, which is why we cannot afford to block the current thread. If we do, then nothing else can run.

If we're reading a File when we start a program, then we can certainly read it synchronously since we don't mind waiting for the File I/O to complete. But if we're reading a File in a running server under Node, then we don't want to halt the whole server just to read that File.

If you're writing a non-browser program in Haskell, you won't have to worry about these issues since it has proper threading, i.e. multiple concurrent threads.

What we need in PureScript is a non-blocking way to do operations that allow us to write as if our thread has been blocked like we can in Haskell.

## 22.2. Working with the `Aff` `Monad`

While `Effect` is the `Monad` that our program ultimately runs in, there’s another more powerful effects `Monad` called `Aff`, which is a `Monad` for Asynchronous Effects.

To get any real work done, we’re going to rely heavily on `Aff`. If we want to run HTTP requests while handling user input from the Browser, we’re going to use `Aff`.

On the backend, if we’re running in Node, we’re going to want to handle multiple requests at a time, which means we’re going to run our request handlers in `Aff`.

Learning how to work within `Aff` and its ancillary services is imperative to building an application of any level of complexity.

So let’s start that process by looking at how we can read a File in an Asynchronous way:

```
import Prelude

import Effect (Effect)

import Effect.Aff (Aff, launchAff_)

import Effect.Class.Console (log) ①

import Node.Encoding (Encoding(..))

import Node.FS.Aff (readTextFile) ②

readAFile :: Aff Unit ③

readAFile = do

  text <- readTextFile ASCII "test.txt"

  log text

test :: Effect Unit

test = launchAff_ readAFile ④
```

① We’re importing a different version of `log` here. This version will work in `Effect` and any `Monad` that has a `MonadEffect` Instance. It turns out that `Aff` has such an instance meaning we can also call `log` in `Aff`.

② We need to add `node-fs-aff` to our `spago.dhall` file to import this module.

③ We are running in the `Aff` `Monad`.

④ `launchAff_` is one of many ways of running Asynchronous processes, in this case, `readAFile`.

This code uses a different Node library that allows us to easily work with files in the `Aff` `Monad` without having to deal with Callback, which makes our coding much easier.

But, this particular library will throw exceptions and crash your program if it receives an error. In the above code, if `test.txt` doesn’t exist, this will crash.

But this is easy to fix:

```
import Prelude

import Control.Monad.Error.Class (try) ①

import Data.Either (Either(..)) ②

import Effect (Effect)

import Effect.Aff (Aff, launchAff)

import Effect.Class.Console (log)

import Node.Encoding (Encoding(..))

import Node.FS.Aff (readTextFile)

readAFile :: Aff Unit

readAFile = do

  result <- try $ readTextFile ASCII "test.txt" ③

  case result of ④

    Right fileData -> log fileData

    Left err -> log $ show err

test :: Effect Unit

test = launchAff_ readAFile
```

① Import `try` from `MonadError`.

② We import `Either` along with it Data Constructors.

③ Now we try to read the File returning an `Either` `Error` `String`.

④ We now check the results of the File read.

The magic elixir here is `try`:

```
try :: ∀ e m a. MonadError e m => m a -> m (Either e a) ①
```

① This takes a Monadic Computation and if it throws an exception, it will catch that exception and return it instead as an `Either` within that same Monadic Context.

As it turns out both `Effect` and `Aff` have `MonadError` Instances, which is why we can use it here.

While the previous approach was simpler, it didn’t handle errors and would crash our app.

With this approach, our program is more robust but we have to check for errors explicitly using a `case` expression.

If we were running in a `Monad` Stack that contained `ExceptT`, then we could convert the `Either` to `ExceptT` using `except`:

```
except :: ∀ e m a. Applicative m => Either e a -> ExceptT e m a
```

This approach would allow us to code the Happy Path since `ExceptT` will short-circuit for us.

### 22.2.1. `Fibers`

Let’s imagine now that we want to read a file in one Asynchronous Process while another does something else, e.g. logs to the console every second.

We can run these 2 processes in what PureScript calls `Fibers`. These aren’t Threads as we might have in Haskell or in other multi-threaded languages. We’re running in Javascript, so we’re limited to a single thread of execution.

Javascript has Cooperative Multitasking, i.e. the current running thread MUST relinquish control to allow other parts of the program to run. That’s why you see callbacks in Node and Browser APIs.

The PureScript libraries do a good job of abstracting this away for us as we’ve seen with reading a File. Although our first example had an explicit callback, we eventually found a library that reduced that cognitive overhead. And if we don’t find one, we could probably write one.

So, how do we create a `Fiber` and run code in it?

One way is to use `forkAff`:

```
forkAff :: ∀ a. Aff a -> Aff (Fiber a)
```

`forkAff` takes something that runs in `Aff` and forks a separate process, i.e. a `Fiber`, where it will run.

Let’s start by writing a Function that runs in `Aff` that will write to the console every second:

```
import Prelude

import Data.Time.Duration (Milliseconds(..)) ①

import Effect.Aff (Aff, delay) ②

import Effect.Class.Console (log) ③

logEverySecond :: Aff Unit

logEverySecond = go 0 where ④

  go x = do ⑤

    log $ show x ⑥

    delay (Milliseconds 1000.0) ⑦

    go $ x + 1 ⑧
```

- 1 Import `Milliseconds` from `Data.Time.Duration`.
- 2 Import `delay`, which will block our `Fiber` for the specified number of milliseconds.
- 3 Notice that we’re importing the version of `log` that works in `MonadEffect`.
- 4 Call `go` with the initial value to log as 0.
- 5 Notice the `do` block starts here, which is running in the `Aff` `Monad`.
- 6 Log `x` to the console.
- 7 Sleep for 1 second.
- 8 Recurse with an incremented Value for `x`.

Next, let’s write another Function that’ll wait for 2 seconds and then read from a file. We’ll call it `readAFileAfterTwoSeconds`:

```
readAFileAfterTwoSeconds :: Aff Unit

readAFileAfterTwoSeconds = do

  delay (Milliseconds 2000.0) ①

  result <- try $ readTextFile ASCII "test.txt"

  case result of

    Right text -> log text

    Left err -> log $ show err
```

① We’ve added a `delay` for 2 seconds to our most recent version of `readAFile`.

Here’s the contents of `test.txt`:

```
This is a test. ①
```

① The file has a newline at the end of the file.

Now, we’d like to have both of these Functions running simultaneously. We’ll let them run for 5 seconds and then terminate them.

First, we’ll write a Function to terminate them called `kill`:

```
import Effect.Aff (Aff, Fiber, delay, killFiber) ①

import Effect.Exception (error) ②

kill :: ∀ a. Fiber a -> Aff Unit

kill = killFiber (error "Killing you softly...") ③ ④
```

① Added `Fiber` and `killFiber` to import list.

② 添加了 `错误 :: String -> Error`。取消时它会传递给 `Fiber`。我们稍后会处理 `Canceler`。

③ 这是 Point-free 形式，其中 `Fiber` 是未命名的参数。

④ 错误是使用 `error` 构造的。该错误将传递给 `Canceler`，即 `Fiber` 的中止处理程序。稍后会详细介绍。

其次，我们将编写一些测试代码来运行所有内容：

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
