# # Priority Queues (Heaps)

Although jobs sent to a printer are generally placed on a queue, this might not always be the best thing to do. For instance, one job might be particularly important, so it might be desirable to allow that job to be run as soon as the printer is available. Conversely, if, when the printer becomes available, there are several 1-page jobs and one 100-page job, it might be reasonable to make the long job go last, even if it is not the last job submitted. (Unfortunately, most systems do not do this, which can be particularly annoying at times.)

Similarly, in a multiuser environment, the operating system scheduler must decide which of several processes to run. Generally, a process is allowed to run only for a fixed period of time. One algorithm uses a queue. Jobs are initially placed at the end of the queue. The scheduler will repeatedly take the first job on the queue, run it until either it finishes or its time limit is up, and place it at the end of the queue if it does not finish. This strategy is generally not appropriate, because very short jobs will seem to take a long time because of the wait involved to run. Generally, it is important that short jobs finish as fast as possible, so these jobs should have precedence over jobs that have already been running. Furthermore, some jobs that are not short are still very important and should also have precedence.

This particular application seems to require a special kind of queue, known as a priority queue. In this chapter, we will discuss ...

+   - Efficient implementation of the priority queue ADT.
+   - Uses of priority queues.
+   - Advanced implementations of priority queues.

The data structures we will see are among the most elegant in computer science.

# ## 6.1 Model

A priority queue is a data structure that allows at least the following two operations: insert, which does the obvious thing; and deleteMin, which finds, returns, and removes the minimum element in the priority queue.1 The insert operation is the equivalent of enqueue, and deleteMin is the priority queue equivalent of the queue's dequeue operation.

1 The C++ code provides two versions of deleteMin. One removes the minimum; the other removes the minimum and stores the removed value in an object passed by reference.