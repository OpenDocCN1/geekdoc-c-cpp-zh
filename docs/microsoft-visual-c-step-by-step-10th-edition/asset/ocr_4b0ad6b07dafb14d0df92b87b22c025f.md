```
// Perform loop processing
}
```

Using the overloads of the Parallel.For method, you can provide local data that's private to each thread, specify various options for creating the tasks run by the For method, and create a ParallelLoopState object that can be used to pass state information to other concurrent iterations of the loop. (Using a ParallelLoopState object is described later in this, in the section "Canceling tasks and handling exceptions")

+   * **Parallel.ForEach<T>** You can use this method in place of a C# foreach statement. By the For method, ForEach defines a loop in which iterations run in parallel. You specify a collection that implements IEnumerable<T> generic interface and a reference to a method that takes a single parameter of type T. The method is executed for each item in the collection, and the item is passed as the parameter to the method. Overloads are available with which you can provide local thread data and specify options for creating the tasks by the ForEach method.

+   * **Parallel.Invoke** You can use this method to execute a set of parameter-less method calls as parallel tasks. You specify a list of delegated method calls (or lambda expressions) that take no parameters and dont return values. Each method can run on a separate thread, in any order. For example, the following code makes a series of method calls:

```
doWork();
doMoreWork();
doYetMoreWork();
```

You can replace these statements with the following code, which invokes these methods by a series of tasks:

```
Parallel.Invoke(
  doWork,
doMoreWork,
  doYetMoreWork
);
```

The Parallel class determines the degree of parallelism appropriate for the environment and workload of the computer. For example, if you use Parallel.For to implement a loop that performs 1,000 iterations, the Parallel class doesn't necessarily create 1,000 concurrent tasks (unless you have an exceptionally powerful processor with 1,000 cores). Instead, the Parallel class creates what it