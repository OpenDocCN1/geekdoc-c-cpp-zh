Several noteworthy aspects of this program should be pointed out:

+   - Method submit, like execute, typically triggers an asynchronous execution of its argument and returns immediately.
+   - The method returns a future, parameterized by the type of the value produced by a task—here, a list of strings. You can think of a future as a handle on a task, or even as the task itself (which it sometimes is, as the later discussion of FutureTask describes).
+   - Futures define mechanisms that you can use to retrieve the value produced by a task. On a Java future, this is method get.
+   - If a task is not finished—it is still running or not yet started—its return value is not available, and method get is blocking: f1.get blocks until the first task completes, and so does f2.get with the second task. This feature is used here by the main thread to wait for both tasks to finish, without the code shutting down the pool or using a latch as before.
+   - The mutable variables strings1 and strings2 of the previous program, which were assignable and arbitrarily initialized, have been replaced with functional, non-reassignable variables—the two futures.³

You can see from this example that futures are synchronizers: They can block a thread—using method get—based on the finished/unfinished state of a task. Like blocking queues, futures are both synchronizers and data structures. After a task terminates, a future contains the value produced by that task. Method get stops being blocking and can be used to simply access this value. In the previous example, if the main thread invokes f1.get or f2.get a second time, it will not block.

Futures are extremely powerful, and much concurrent programming can be simplified by leveraging them. Consider, for instance, a simple server similar to Listing 21.4:

```
Scala
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
```

³This transformation is similar to the transition from imperative to functional programming discussed in Part I—for instance, between Listing 3.2 and Listing 3.3.