Worse, `Thread.Sleep()` is often used as a "poor man's synchronization system." That is, if you have some unit of asynchronous work, and the current thread cannot proceed until that work is done, you might be tempted to put the thread to sleep for much longer than you think the asynchronous work will take, in the hopes that it will be finished when the current thread wakes up. This is a bad idea: Asynchronous work, by its very nature, can take longer than you think. Use proper thread synchronization mechanisms, described in the next chapter, to synchronize threads. (We'll give an example of this sort of abuse in Listing 19.2.)

Putting a thread to sleep is also a bad programming practice because it means that the sleeping thread is, obviously, unresponsive to attempts to run code on it. If you put the main thread of a Windows application to sleep, that thread will no longer be processing messages from the user interface and will therefore appear to be hung.

More generally, putting a thread to sleep is a bad programming practice because the whole point of allocating an expensive resource like a thread is to get work out of that resource. You wouldn't pay an employee to sleep, so do not pay the price of allocating an expensive thread only to put it to sleep for millions or billions of processor cycles.

That said, there are some valid uses of `Thread.Sleep()`. First, putting a thread to sleep with a time delay of zero tells the operating system "the current thread is politely giving up the rest of its quantum to another thread if there is one that can use it." The polite thread will then be scheduled normally, without any further delay. Second, `Thread.Sleep()` is commonly used in test code to simulate a thread that is working on some high-latency operation without actually having to burn a processor doing some pointless arithmetic. Other uses in production code should be reviewed carefully to ensure that there is not a better way to obtain the desired effect.

In task-based asynchronous programming in C# 5, you can use the `await` operator on the result of the `Task.Delay()` method to introduce an asynchronous delay without blocking the current thread. See the "Timers" section in Chapter 20 for further detail.

**Guidelines**

AVOID calling `Thread.Sleep()` in production code.