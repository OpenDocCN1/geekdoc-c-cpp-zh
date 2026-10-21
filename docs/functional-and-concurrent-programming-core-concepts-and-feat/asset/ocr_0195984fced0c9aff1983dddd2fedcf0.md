The calls futureData.join() and futureAd.join() do not block the thread, even if the ad or the data is not yet available. Contrast this implementation with Listing 25.2, in which method get of a regular future is used to retrieve the ad, possibly causing a worker thread to block if the ad-fetching task is still running.

For all practical purposes, the implementation in Listing 27.4 is equivalent to Listing 26.7, which uses flatMap and map to combine the ad with database data in a non-blocking way. Its main benefit is that it is closer in style to familiar (but blocking) variants like that seen in Listing 25.2.

With fork and join, you have a mechanism for a task to wait for another task without blocking a thread. However, if you use a lock, or a semaphore, or a blocking queue, you can still block a thread. To truly leverage the advantages of ForkJoinPool, you need to refrain from using synchronizers. If you absolutely need to block a thread, the framework defines a ManagedBlocker interface, which you can use to indicate that a thread is about to block. This makes it possible for the pool to create additional threads appropriately to maintain a desired level of parallelism.

# 27.4 Asynchronous Programming

The idea of waiting without blocking, as in Listing 27.4, is also found in other programming models. These tend to focus on making code asynchronous—as opposed to concurrent—but can also typically be configured to support concurrency. In Scala, for instance, you can use an experimental asynchronous framework to implement the parallel ad-fetching and database lookup example in a standard-looking style:

```
import cps.compat.sip22.{ async, await }

async {
  val futureAd: Future[Ad]      = Future(fetchAd(request))
  val futureData: Future[Data] = Future(dbLookup(request))
  val ad: Ad                    = await(futureAd)
  val data: Data                = await(futureData)
  val page: Page                = makePage(data, ad)
}
```

Listing 27.5: Example of non-blocking concurrency with an async/await construct.

Method await suspends the execution of the async block until its target future is completed, but it does not block the thread, which continues to run code elsewhere. The implementation again follows a conventional blocking style but is pretty much equivalent in behavior to Listing 26.7 (with flatMap/map) or Listing 27.4 (with ForkJoinPool).⁹

> ⁹This example uses a non-standard library by Ruslan Shevchenko, which actually transforms async/await code into corresponding calls to map/flatMap at compile time.