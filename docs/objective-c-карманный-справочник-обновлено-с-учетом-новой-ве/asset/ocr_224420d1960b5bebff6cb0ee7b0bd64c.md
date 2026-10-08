# Waiting for a Condition 285

**NSCondition**, the condition object will be locked. You must test your condition and then either unlock the condition object or go back to sleep.

You use the same pattern with condition variables in almost every case you will use them. Generally, they let you establish a producer-consumer relationship between threads. The consumer thread needs to sleep until there is some data waiting for it. The producer threads need to wake up the consumer thread when there is some data for it.

The example at the start of this section showed two methods on a class. The `-addToQueue` method is expected to be called from a producer thread, whereas the `-main` method implements the consumer thread.

The consumer thread code shows several important features of a threaded object. Rather than using an `NSRunLoop`, this implements its own run loop, an infinite loop, and creates and destroys an autorelease pool at every iteration explicitly. In each iteration, if there is no data waiting, it first locks the condition and releases the lock and sleeps.

A producer thread can then acquire the lock and signal the condition. When this happens, the consumer thread will be poised to wake up as soon as the lock becomes available. The producer permits this by releasing the lock.

The consumer thread then gets the next bit of