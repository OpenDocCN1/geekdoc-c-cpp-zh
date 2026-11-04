# Summary

Taking advantage of multicore machines is becoming increasingly important. From a programmer’s point of view, the new features in .NET 4’s System.Threading libraries make it easier to do so.

In this chapter, we explored the notion of task parallelism centered around the Task and Task<TResult> types. We discussed how to create tasks, await their results, work with continuations, and deal with various aspects such as errors and cancellation. In summary, tasks are the new means to perform work asynchronously, whether it’s long running (where you’d have used threads before) or more ad hoc short-lived computations (using thread pools before). We also discussed how the task scheduler works, layered atop of the improved thread pool, employing techniques such as work stealing.

We finished our discussion of modern .NET 4 approaches to parallelism with a tour through data parallelism, exposed through the Parallel class’s loop methods. During our discussion, you learned about loop state, parallelization options, partitioning schemes, and more.