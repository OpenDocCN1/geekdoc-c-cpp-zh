This example starts a 1-second task and a 2-second task and registers a simple callback on each. It produces an output of the following form:

```
main at XX:XX:33.413: START
main at XX:XX:33.465: END
pool-1-thread-3 at XX:XX:34.466: Success(42)
pool-1-thread-3 at XX:XX:35.465: Failure(java.lang.NullPointerException)
```

You can see that the main thread terminates immediately—callback registration takes almost no time. One second later, the first callback runs and prints a Success value. One second after that, the second callback runs and prints a Failure value. In this output, both callbacks ran on the same thread, but there is no guarantee that this will always be the case.

You can use a callback in the ad-fetching scenario. Instead of waiting for a customized ad to assemble a page, as in Listing 26.2, you specify as an action what is to be done with the ad once it becomes available:

```
val futureAd: Future[Ad] = Future(fetchAd(request))
val data: Data = dbLookup(request)
futureAd.onComplete { ad =>
  val page = makePage(data, ad.get)
  connection.write(page)
}
```

Listing 26.3: Ad-fetching example with a callback on a future.

After the connection-handling thread completes the database lookup, it registers a callback action on the ad-fetching task, instead of waiting for the task to finish. The callback action extracts a customized ad from the Try value (assuming no error), assembles the data and ad into a page, and sends the page back as a reply as before. The key difference from Listing 26.2 is that no blocking is involved.

# 26.3 Higher-Order Functions on Futures

By using a callback to assemble and send the page, you avoid blocking, and thus eliminate the risk of deadlock. However, because the function argument of onComplete is an action, which is executed for its side effects, some of the earlier functional flavor is lost. Recall that in the full version of the server in Listing 25.2, the assembled page is also used in a statistics-keeping function. If a value produced as a future is needed in multiple places, handling these uses with callbacks can get complicated. If the value