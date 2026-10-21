
Several noteworthy aspects of this program should be pointed out:

- Method `submit`, like `execute`, typically triggers an asynchronous execution of its argument and returns immediately.
- The method returns a future, parameterized by the type of the value produced by a task—here, a list of strings. You can think of a future as a handle on a task, or even as the task itself (which it sometimes is, as the later discussion of `FutureTask` describes).
- Futures define mechanisms that you can use to retrieve the value produced by a task. On a Java future, this is method `get`.
- If a task is not finished—it is still running or not yet started—its return value is not available, and method `get` is blocking: `f1.get` blocks until the first task completes, and so does `f2.get` with the second task. This feature is used here by the main thread to wait for both tasks to finish, without the code shutting down the pool or using a latch as before.
- The mutable variables `strings1` and `strings2` of the previous program, which were assignable and arbitrarily initialized, have been replaced with functional, non-reassignable variables—the two futures.[^3]

You can see from this example that futures are synchronizers: They can block a thread—using method `get`—based on the finished/unfinished state of a task. Like blocking queues, futures are both synchronizers and data structures. After a task terminates, a future contains the value produced by that task. Method `get` stops being blocking and can be used to simply access this value. In the previous example, if the main thread invokes `f1.get` or `f2.get` a second time, it will not block.

Futures are extremely powerful, and much concurrent programming can be simplified by leveraging them. Consider, for instance, a simple server similar to Listing 21.4:

```scala
val exec = Executors.newFixedThreadPool(16)
val server = ServerSocket(port)

def handleConnection(connection: Connection): Unit =
  val request = connection.read() // get request from client
  val data = dbLookup(request) // search the database
  addToLog(data) // log the results of the search
  val ad = fetchAd(request) // fetch a customized ad
  val page = makePage(data, ad) // create a page
  connection.write(page) // reply to the client
  connection.close() // close the socket
  updateStats(page) // record some statistics

while true do
  val socket = server.accept()
  exec.execute(() => handleConnection(Connection(socket)))
```

This server uses a thread pool to handle incoming connections in parallel, up to 16 requests concurrently. Each connection, however, is processed sequentially through a series of operations: First read the request, then retrieve data from a database, then fetch a customized ad, and so on.

Instead of happening in sequence, some of these steps could be executed concurrently. For instance, the server could be made faster and more responsive by fetching the ad in parallel with the other operations:

```scala
val exec1 = Executors.newFixedThreadPool(12)
val exec2 = Executors.newFixedThreadPool(8)
val server = ServerSocket(port)

def handleConnection(connection: Connection, exec: ExecutorService): Unit =
  val request = connection.read()
  val futureAd = exec.submit(() => fetchAd(request))
  val data = dbLookup(request)
  addToLog(data)
  val page = makePage(data, futureAd.get())
  connection.write(page)
  connection.close()
  updateStats(page)

while true do
  val socket = server.accept()
  exec1.execute(() => handleConnection(Connection(socket), exec2))
```

Listing 25.2: A parallel server with parallelism within responses; see also Lis. 26.8.

After a request has been read from a socket, a task is created to fetch a customized ad. The call to method `submit` returns immediately with a future, and the thread handling the request continues with the database lookup. After the data has been retrieved and logged, the ad is needed to assemble the page. You obtain it by calling `get` on the future. There are two possibilities at this point. If the ad-fetching task is still running, method `get` blocks. Once the ad becomes available, `get` unblocks, and the page is assembled. If, however, the ad-fetching task is already finished by the time you reach `makePage`, method `get` does not block and simply returns the ad, which you use to assemble the page. In other words, fetching the ad and querying the database now happen in parallel, and the same code handles all cases, whether ad fetching is faster or slower than database querying.

In addition to the no-argument method `get`, futures in Java define a method `isDone` to query the status of a task without blocking. It can be used to implement more complex strategies that involve combinations of polling and blocking. Note that the server in Listing 25.2 uses two thread pools. Using the same executor to run `handleConnection` and `fetchAd` would run a risk of deadlock. This topic is discussed in detail in Section 26.1.

## 25.3 Timeouts, Failures, and Cancellation

A future carries the result of a functional task after the task has completed. But what happens if the task fails? In this case, the future must still be completed—there is no point in waiting on `get` for a result that will never come. Instead of the task’s result, the future then contains the cause of the failure. In Java, method `get` rethrows the exception that caused a task to fail but wraps it first inside an `ExecutionException`.

As with almost all synchronizers, you can set an upper limit on the amount of time a thread might be blocked. Java’s method `get` accepts an optional timeout argument. If the timeout is reached before a task produces a value, this variant of `get` throws a `TimeoutException`.

As an illustration, you can modify the server from Listing 25.2 to use a fallback ad if loading a customized ad fails and to replace a customized ad with a default ad if loading takes more than 0.5 second after database lookup and logging have been completed:

```scala
val futureAd = exec.submit(() => fetchAd(request))
... // DB lookup and logging
val ad =
  try futureAd.get(500, MILLISECONDS)
  catch
    case _: ExecutionException => failedAd
    case _: TimeoutException => futureAd.cancel(true); timeoutAd
val page = makePage(data, ad)
...
```

Listing 25.3: Dealing with a future’s timeout and failure.

Variable `ad` is set with one of three values: (1) a customized ad, if loading finishes within the 0.5-second timeout; (2) a failed ad if loading fails within 0.5 second; or (3) a default ad if loading is still running after 0.5 second. In this last case, the ad that is still being loaded will never be used, and loading can be interrupted. This is the purpose of the call `cancel(true)`.[^4]

## 25.4 Future Variants

The code examples in Sections 25.2 and 25.3 rely on `java.util.concurrent.Future`, the oldest of Java’s two Future types. Java 8 introduced `java.util.concurrent.CompletableFuture`, which is created slightly differently. For instance, the future `f1` in Listing 25.1 could be created as a `CompletableFuture` as

```scala
val f1 = CompletableFuture.supplyAsync(() => makeStrings(5, "T1"), exec)
```

or

```scala
val f1 = CompletableFuture.supplyAsync(() => makeStrings(5, "T1"))
```

The second form uses a common thread pool instead of a user-specified thread pool. Scala uses its own futures and specifies the thread pool to use as an implicit argument. This allows you to write

```scala
given ExecutionContext = exec

val f1 = Future(makeStrings(5, "T1")) // uses exec
```

or

```scala
val f1 = Future(makeStrings(5, "T1")) // uses the default thread pool in scope
```

Note that Scala relies on an unevaluated, by-name argument, thereby avoiding the use of a lambda expression as an explicit thunk (see the discussion in Section 12.2). With both Scala’s `Future` and Java’s `CompletableFuture`, the future that is returned implements a richer interface that supports a form of functional-concurrent programming, as discussed in Chapter 26.

## 25.5 Promises

Promises are the internal mechanism by which futures are created. A promise represents the (yet-to-come) value of a future. In some sense, it is the data part of the data/synchronizer combination that constitutes a future.

A promise can be fulfilled with either a value or an error, at which point the future is complete. Promises are often—but not always—created by one thread and completed

[^3]: This transformation is similar to the transition from imperative to functional programming discussed in Part I—for instance, between Listing 3.2 and Listing 3.3.

[^4]: The Boolean argument in `cancel` affects tasks that have already started to run. If it is `true`, there is an attempt to terminate the execution. This is often implemented by interrupting the running thread, which may or may not stop the task. If the Boolean is `false`, no attempt is made to stop a running task, but the future is still marked as canceled. Java’s newer futures implement only `cancel(false)` semantics, and Scala’s futures have no cancellation mechanism. (The rationale is that, as a cancellation mechanism, interruption works adequately only with tasks designed to respond to it. Tasks that perform non-interruptible I/O, for instance, will not react to `cancel(true)`.) Canceling running tasks is difficult in general. The case study in Chapter 28 requires the need to cancel tasks after they have begun to run and implements an ad hoc cancellation strategy independent of futures.
