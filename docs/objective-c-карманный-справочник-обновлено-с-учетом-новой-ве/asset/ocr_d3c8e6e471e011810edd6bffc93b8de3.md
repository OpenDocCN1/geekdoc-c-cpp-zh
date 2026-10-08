# Creating Custom Work Queues 299

pushed, but they may complete in an arbitrary order, and any number of them might be running at once.

There is also one special queue, which is intended to run on the main thread. You can get a reference to this with dispatch_get_main_queue(). This queue is used on OS X 10.6 to implement the run loop. This queue is a FIFO queue, and you may wish to create similar queues. A FIFO queue is similar to a lightweight thread. It executes sequentially, one block at a time. The relationship between threads and queues is variable. All of your queues may end up running concurrently on separate threads, or all may be executed on a single OS thread, depending on various factors.

You create a new FIFO queue by calling dispatch_queue_create(). This is useful when you have a number of things that need to execute in a defined order, but are largely independent of the rest of the program. This helps reduce the need for explicit synchronization.

The example at the start of this chapter pushed three blocks that incremented a counter and one that printed its final value into a new queue. These blocks are all related; executing them in the wrong order is a very bad idea. With this approach, they all execute in a guaranteed order with respect to each other, but not with regard