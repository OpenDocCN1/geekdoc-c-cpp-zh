# Multithreading Basics 939

get replaced with the data from thread B (or vice versa). If there are too many threads, the switching overhead can begin to noticeably affect performance. Adding more threads will likely decrease performance, to the point where the processor spends more time switching from one thread to another than it does accomplishing the work of each thread.

Even if we ignore the cost of context switching, time slicing itself can have a huge impact on performance. Suppose, for example, that you have two processor-bound high-latency tasks, each working out the average of two lists of 1 billion numbers each second. Suppose the processor can perform 1 billion operations per second. If the two tasks are each associated with a thread, and the two threads each have their own core, obviously we can get results in 1 second.

If, however, the two threads share a single processor, time slicing performs a few thousand operations on one thread, then switches to the other thread, then switches back, and so on. Each task consumes a total of 1 second of processor time, and the results of both are available after 2 seconds, leading to an average completion time of 2 seconds. (Again, we are ignoring the cost of context switching.)

If we assigned those two tasks to a single thread that performed the first task and did not even start the second until the first was completed, the result of the first task would be obtained in 1 second after that, and the result of the subsequent task would be obtained 1 second after that, leading to an average time of 1.5 seconds (a task completes in either 1 or 2 seconds and therefore, on average, completes in 1.5 seconds).

# Guidelines

> DO NOT fall into the common error of believing that more threads always make code faster.

DO carefully measure performance when attempting to speed up processor-bound problems through multithreading.