# Using Blocks with Threads

I’m sure that you can think of many different uses for blocks in your code. I’m going to touch on a couple of them in the next few sections.

If you think about the way that blocks enable you to encapsulate functionality in your application in a nice neat package, functionality that can be easily reused, then it makes sense that one of the most commonly used design patterns for blocks in Objective-C is to provide code that can be run in parallel. In other words, threads.

Indeed, one of the first use cases that Apple demonstrated when it introduced blocks in Objective-C was the ability to use them in its (at the time) brand-new parallelization framework, Grand Central Dispatch.

# Working with Grand Central Dispatch

Grand Central Dispatch is a framework that ships with Mac OS X version 10.6. It provides an easy-to-use abstraction layer that enables developers to take advantage of multiprocessor and multicore architectures without having to deal with lower-level thread management.

Using GCD, developers need only provide blocks of code, which encapsulate functionality that can safely run in parallel. They hand these blocks off to GCD queues, which then handle all of the low-level details surrounding things such as the creation of threads, the management of those threads, even how many threads should be created to run the tasks provided on a given system. GCD knows how many cores a machine has and will only allocate enough threads to maximize performance over those cores. It completely handles queuing up the tasks provided to it and distributing those tasks to the threads that it creates.

Tasks can be provided to Grand Central Dispatch as either functions or blocks. Obviously, given the topic of this chapter, we are going to focus on using blocks with Grand Central Dispatch.

# Using GCD functions to dispatch code blocks in threads

The core of the GCD API centers around the concept of queues. By using GCD, you can either select one of the pre-existing system queues, such as the global queue. You access it by using the method `dispatch_get_global_queue()`, which returns the global concurrent queue associated with your application, or you can create your own private serial queue by using the function `dispatch_queue_create`.

Queues themselves can be either concurrent or serial, indicating that the objects placed within them can be run in parallel, relative to each other, in the case of a concurrent queue or sequentially, relative to each other in the case of a serial queue.