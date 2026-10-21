
As a side note, actors have the interesting property that they can switch behaviors, and thus process subsequent incoming messages differently. This can be leveraged to implement state machines in terms of actors:

```scala
trait Command
case class Start(replyTo: ActorRef[Number]) extends Command
case class Number(value: Int) extends Command
case object Stop extends Command

def reset(): Behavior[Command] =
  Behaviors.receiveMessagePartial {
    case Start(replyTo) => add(replyTo, reset())
  }

def add(replyTo: ActorRef[Number], reset: Behavior[Command]): Behavior[Command] =
  var sum = 0
  Behaviors.receiveMessagePartial {
    case Number(value) =>
      sum += value
      Behaviors.same
    case Stop =>
      replyTo ! Number(sum)
      reset
  }
```

Listing 27.8: Example of a state machine as an actor that switches behavior.

This example implements a counter by starting an actor with a reset behavior. This actor waits for the Start command. When Start is received, the actor changes its behavior to add, passing its current behavior as an argument so it can be used later to switch back. Messages are then processed according to the new behavior. When a message of type Number is received, its value is added into an accumulator sum, and the behavior of the actor remains the same. When the Stop message is received, the actor replies with the accumulated sum and reverts to its initial behavior, waiting for another Start message. As a state machine, the actor transitions between states as follows:

![](img/74309e2bdd93f68d2e94338a3d73517f_448_0.png)

Method add is implemented in an imperative style, with a mutable variable sum. This is done on purpose, to emphasize the fact that, within an actor, messages are processed sequentially. The actor may receive numbers concurrently and still add them correctly, even though no lock is used and the assignment sum += value is not thread-safe.

## 27.6 Reactive Streams

Listings 27.4 to 27.7 all end with a single page having been constructed. In an actual application, you would then need to operate on the page in some fashion. This pattern works well if all the pages are used independently from each other, as in the server example: Each page is sent back to a client via a socket. But if you need to handle all the pages, as a whole, within a larger component, a scattering of asynchronously created pages—a collection of Future[Page] values, for instance—becomes inadequate. As an alternative, you can use a stream of asynchronous pages.

Reactive streams are an abstraction that combines the asynchronous characteristics of futures with the manifold nature of iterators. Several implementations exist, in a variety of languages—for example, RxJava, RxSwift, RxAndroid, Akka Streams, and Vert.x—including a bare-bones variant as java.util.concurrent.Flow. The next example uses Reactor, a popular Java implementation:

```scala
import reactor.core.publisher.{ Flux, Mono }

def makePages(requests: Flux[Request]): Flux[Page] =
  requests.flatMap { request =>
    val adF = CompletableFuture.supplyAsync(() => fetchAd(request), exec)
    val dataF = CompletableFuture.supplyAsync(() => dbLookup(request), exec)
    val pageF = dataF.thenCombine(adF, makePage)
    Mono.fromFuture(pageF)
  }
```

Listing 27.9: Example of non-blocking transformation using reactive streams.

Instead of creating a single page from a single request, this variant transforms a stream (called Flux in Reactor) of requests into a stream of pages. The code is asynchronous: A call to method makePages on a stream of requests completes immediately and returns a stream of pages. Later, as requests are added to the input stream, corresponding pages appear in the output stream. As before, ad fetching and database lookup are executed in parallel on a thread pool.[10] The two futures are combined into a future page asynchronously (thenCombine is CompletableFuture’s version of zipWith, which was used in Section 26.4). The future page is transformed into a short stream of one value, called Mono in Reactor.

The power of reactive streams lies in their mechanisms for managing back pressure (slowing upstream computations until downstream can catch up), error handling, and time-based processing. These mechanisms are beyond the scope of this book, but as a brief illustration of time-based processing, consider this example:

```scala
val pages: Flux[Page] = ...

val largestPastHour: Flux[Int] =
  pages
    .map(_.length)
    .window(Duration.ofHours(1), Duration.ofMinutes(5))
    .flatMap(lengths => lengths.reduce(0, Integer.max))
```

The expression uses overlapping windows to report every 5 minutes the length of the longest page created in the previous hour, as a stream of numbers. Think of how you would implement this directly in terms of individual futures of pages, without ever blocking a thread. This is a nontrivial problem.

## 27.7 Non-blocking Synchronization

This chapter and Chapter 26 present several techniques that avoid blocking threads. In this last section, I want to clear up a misconception I have encountered several times. It is the idea that because threads are never blocked when using these approaches, synchronization mistakes such as deadlocks are impossible. This is not the case. Yes, some common deadlock-prone situations can be avoided by not blocking threads—see, for instance, the discussion of recursive tasks in Section 26.1. But it does not follow that synchronization mistakes—including deadlocks—cannot happen.

You need to distinguish between a future, task, coroutine, or actor “waiting” for some event—which does not involve blocking a thread—and a thread being parked. In particular, you can still end up with a deadlock by having futures, tasks, coroutines, or actors wait for each other in a cycle, independently from the status of the threads that run them. As an illustration, this (contrived) example has two futures waiting for each other:

```scala
lazy val future1: Future[Int] = Future.delegate {
  println("future 1 starts")
  val future2: Future[String] = Future.delegate {
    println("future 2 starts")
    future1.map(n => n.toString)
  }
  future2.map(str => str.length)
}
```

When executed on a pool with multiple threads, this program prints the two statements "future 1 starts" and "future 2 starts", and then hangs. To complete, future2 needs a number from future1, and future1 needs a string from future2. This is a deadlock of futures, not of threads. A thread dump would reveal that all the threads from the pool are idle, waiting for tasks to execute.

You might object that this example is artificial (it is), but complex applications, especially when you use promises explicitly, can face this type of situation. It is also easy to end up deadlocked in a message-oriented framework by having a set of entities wait for messages in a cycle. For instance, you can use Kotlin coroutines to wait for a message on a channel without blocking a thread:

```kotlin
val strings = Channel<String>()
val ints = Channel<Int>()

suspend fun task1() = coroutineScope {
    launch { task2() }
    println("waiting for a string")
    val str = strings.receive()
    ints.send(str.length)
}

suspend fun task2() = coroutineScope {
    println("waiting for an int")
    val n = ints.receive()
    strings.send(n.toString())
}
```

This program also prints two messages and then stops, even though method receive is not blocking threads and all threads are idle. You face the same difficulty with actors. It is a common pattern for an actor to need N messages before it can issue a response—similar to using a countdown latch in a blocking variant. If you wait for N − 1 messages instead, you may produce an incomplete response; if you wait for N + 1 messages, you may end up in a deadlock, with no response being sent at all.

Besides performance considerations, which are important, a major benefit of non-blocking strategies is that they help programmers shift their attention from non-interference to cooperation. Non-interference synchronization—typically using locks—is not needed, but the patterns that would require a cooperating synchronizer—such as a blocking queue or a countdown latch—are still there. You just implement them differently—for instance, as an actor or a coroutine waiting for messages, or by combining several futures through zip or flatMap. The fact that threads are not blocked,
