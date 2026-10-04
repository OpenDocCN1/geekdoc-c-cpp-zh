+   * OrderedTaskScheduler This scheduler allows only one task to execute at a time. This class is derived from LimitedConcurrencyLevelTaskScheduler and just passes 1 for n.

+   * PrioritizingTaskScheduler This scheduler queues tasks for the CLR's thread pool. After this has occurred, you can call Prioritize to indicate that a Task should be processed after all normal tasks (if it hasn't been processed already). You can call Deprioritize to make a Task be processed after all normal tasks.

+   * ThreadPerTaskScheduler This scheduler creates and starts a separate thread for each task; it does not use the thread pool at all.

# Parallel's Static For, ForEach, and Invoke

There are some common programming scenarios that can potentially benefit from the improved performance with tasks. To simplify programming, the System Threading.Parallel class encapsulates these scenarios while using Task objects internally. For example, instead of processing all items in a collection you like

```
// One thread performs all work sequentially
for (Int32 i = 0; i < 1000; i++) DoWork(i);
```

you can get inside multiple thread pools to assist in performing this work by using the Parallel class's For method.

```
// The thread pool's threads processes the work in parallel
Parallel.ForEach(0, 1000, i => DoWork(i));
```

And if you have a collection, instead of doing this:

+   * One thread performs all work sequentially
foreach (var item in collection) DoWork(item);

you can do this.

```
// The thread pool's threads processes the work in parallel
Parallel.ForEach(collection, item => DoWork(item));
```

And you can use either For or ForEach in your code, then it is recommended that you use For because it executes faster.

And finally, if you have several methods that you need to execute, you could execute them sequentially, like this:

```
// One thread executes all the methods sequentially
Method1();
Method2();
Method3();
```