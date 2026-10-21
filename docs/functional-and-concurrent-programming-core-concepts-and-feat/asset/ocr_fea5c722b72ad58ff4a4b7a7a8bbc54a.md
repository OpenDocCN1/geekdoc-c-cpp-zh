This variant uses the newer `CompletableFuture`. As before, a promise is created and a task is scheduled to fulfill it. One difference from Listing 25.4 is that `CompletableFuture` doesn’t use a `Try` type, so you need to treat the successful and error cases separately. Another difference is that the promise is itself the future being returned—type `CompletableFuture` plays both parts.

Alternatively, you could implement `apply` by using Java’s older futures:

```
```scala
import java.util.concurrent.{ Future, FutureTask }

def apply[A](code: => A)(using exec: ExecutionContext): Future[A] =
  val promise = FutureTask(() => code)
  exec.execute(promise)
  promise
```
```

Listing 25.6: Future creation from a `FutureTask` promise.

The type `FutureTask` is both a `Runnable` and a `Future`, so the promise itself is being executed in the thread pool and returned as a future. If its run method fails, the future is completed exceptionally.

# 25.6  Illustration: Thread-Safe Caching

In Listings 25.4 to 25.6, promises are used in conjunction with thread pools to provide a user with a future, but there are many other useful patterns that involve promises. This section uses promises to implement a thread-safe variant of our memoization example from Chapter 12. No thread pools are involved, and futures are only used internally and are not publicly visible.

Recall that the problem is to cache the values computed by a function. In Listing 12.2, function `memo` uses a closure to store a mapping of input-output pairs of known outputs for given inputs. Given a function `f`, function `g = memo(f)` computes the same values as `f`, but with additional caching. Function `g`, however, contains a mutable state—the mapping inside the closure—and is not thread-safe, even if function `f` is.

⁵ JavaScript also implements a promise and a future as a single object but calls it a *promise*, while Java refers to it as a *future*. As it happens, because of the way promises are currently implemented in Scala, `promise.future` is also the same object as `promise`—the future simply returns this—but is used through two distinct types, `Future` and `Promise`.