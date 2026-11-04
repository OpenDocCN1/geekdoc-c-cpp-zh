![](bbox=[0.02, 0.05, 0.98, 0.78])

# FIGURE 29.19 Different relative execution orders yield different results.

No matter how many times you run this code, the outcome should always be zero (as we expected in the first place). The way this works is by the monitor's guarantee that no two threads can be operating under the lock at the same time.

Monitors use an object as the “cookie” to perform the synchronization with, which relates to the way the common language runtime provides this service. (Objects have a SyncBlock associated with them.) It's typical to simply allocate a dummy object and use it around the code blocks that shouldn't run at the same time from different threads.

Use of the lock keyword turns into a try-finally statement, where the try block contains the code to enter the monitor and the finally block takes care of exiting the monitor. For example, consider the following piece of code: