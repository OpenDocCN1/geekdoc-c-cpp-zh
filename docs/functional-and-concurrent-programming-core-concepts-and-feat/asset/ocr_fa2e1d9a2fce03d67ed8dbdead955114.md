```
def compute(input: A, timeout: Double): scala.concurrent.Future[Option[B]] = ...
```

A call to compute returns immediately. Later, the future is completed when a strategy succeeds, all the strategies have failed, or the specified timeout is reached, whichever comes first. An asynchronous runner is more flexible than the blocking variant: You can choose to use the returned future asynchronously, by means of higher-order functions, or to block until the future is complete, which brings you back to the behavior of the previous (blocking) compute methods.

The implementation of an asynchronous runner using Scala futures faces two difficulties. First, you need a mechanism to complete a future after a timeout. You can reuse the approach described in Section 26.5, based on a promise and a timer, to implement a generic completeOnTimeout extension to futures:

```
extension [A](future: Future[A])
  def completeOnTimeout(timeout: Long, unit: TimeUnit)(fallbackCode: => A)(
    using exec: ExecutionContext, timer: ScheduledExecutorService
  ): Future[A] =
    if future.isCompleted then future
    else
      val promise   = Promise[A]()
      val complete  = (() => promise.completeWith(Future(fallbackCode))): Runnable
      val completion = timer.schedule(complete, timeout, unit)

      future.onComplete { result =>
        completion.cancel(false)
        promise.tryComplete(result)
      }
      promise.future
```

Listing 28.4: Extending Scala futures with completeOnTimeout.

If the future is not already completed, a promise is created, and a task is scheduled on a timer to complete this promise with a default value after a timeout delay. Using onComplete, a callback action is registered with the original future, which also tries to complete the same promise, using the future's own result. If this action runs before the timeout, the timer task is not needed and is canceled—completion is a Java future with a cancel method. In all cases, the promise is eventually completed either by the timer task, after a timeout delay, or when the initial future terminates, if this happens before the timeout.

You may be wondering about the initial if-then-else because no locks are used, which results in a non-atomic check-then-act. Could this be a problem? The answer is that the test is not strictly necessary: The code still works even if all it does is follow the else branch. The early test is merely an optimization that avoids creating a new promise if completeOnTimeout happens to be called on a completed future. If a future