When executed on a pool with multiple threads, this program prints the two statements "future 1 starts" and "future 2 starts", and then hangs. To complete, future2 needs a number from future1, and future1 needs a string from future2. This is a deadlock of futures, not of threads. A thread dump would reveal that all the threads from the pool are idle, waiting for tasks to execute.

You might object that this example is artificial (it is), but complex applications, especially when you use promises explicitly, can face this type of situation. It is also easy to end up deadlocked in a message-oriented framework by having a set of entities wait for messages in a cycle. For instance, you can use Kotlin coroutines to wait for a message on a channel without blocking a thread:

```
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