
responsive application and the remaining core can help you run another part of code in parallel. In these cases, you want to specify the maximum degree of parallelism for a parallel loop.

## ParallelOptions

TPL enables you to specify a different maximum desired degree of parallelism by creating an instance of the new ParallelOptions class and changing the value of its MaxDegreeOfParallelism property. Listing 33-12 shows a new version of the two well-known subroutines that use Parallel.For, ParallelGenerateAESKeysMaxDegree and ParallelGenerateMD5HashesMaxDegree.

Now, they receive an Integer with the maximum desired degree of parallelism, maxDegree. Each subroutine creates a local instance of ParallelOptions and assigns the value received as a parameter to its MaxDegreeOfParallelism property, which is a new parameter for each parallel loop before the body. This way, the loop won't be optimized to take advantage of all the available cores (MaxDegreeOfParallelism = -1). Instead, it will be optimized as if the total number of available cores were equal to the maximum degree of parallelism specified in the property:

```
Dim parallelOptions As New ParallelOptions()
parallelOptions.MaxDegreeOfParallelism = maxDegree
```

### LISTING 33-12: Specifying maximum desired degree of parallelism for Parallel.For loops

```
Sub ParallelGenerateAESKeysMaxDegree(ByVal maxDegree As Integer)
    Dim parallelOptions As New ParallelOptions()
    parallelOptions.MaxDegreeOfParallelism = maxDegree
    Dim sw = Stopwatch.StartNew()
    Parallel.For(1, NUM_AES_KEYS + 1, parallelOptions,
        Sub(i As Integer)
            Dim result() As Byte
            Dim hexString As String
            Dim aesM As New AesManaged()
            aesM.GenerateKey()
            result = aesM.Key
            hexString = ConvertToHexString(result)
            ' Console.WriteLine("AES:" + hexString)
        End Sub)
    Debug.WriteLine("AES: " + sw.Elapsed.ToString())
End Sub

Sub ParallelGenerateMD5HashesMaxDegree(ByVal maxDegree As Integer)
    Dim parallelOptions As New ParallelOptions
    parallelOptions.MaxDegreeOfParallelism = maxDegree
    Dim sw = Stopwatch.StartNew()
    Parallel.For(1, NUM_MD5_HASHES + 1, parallelOptions,
        Sub(i As Integer)
            Dim md5M As MD5 = MD5.Create()
            Dim result() As Byte
            Dim data() As Byte
            Dim hexString As String
            data = Encoding.Unicode.GetBytes(Environment.UserName + i.ToString())
            result = md5M.ComputeHash(data)
            hexString = ConvertToHexString(result)
            ' Console.WriteLine("MD5:" + hexString)
        End Sub)
    Debug.WriteLine("MD5: " + sw.Elapsed.ToString())
End Sub
```

> It is not convenient to work with static values for the desired degree of parallelism, because it can limit scalability when more cores are available. These options should be used carefully; it is best to work with relative values according to the number of available logical cores, or consider this number in order to prepare the code for further scalability.

This way, it is possible to call both subroutines with a dynamic value, considering the number of logical cores at runtime:

```
ParallelGenerateAESKeysMaxDegree(Environment.ProcessorCount - 1)
ParallelGenerateMD5HashesMaxDegree(Environment.ProcessorCount - 1)
```

Both Parallel.For loops are going to try to work with the number of logical cores minus 1. If the code runs with a quad-core microprocessor, then it will use just three cores.

The following is not a best practice for final code. However, sometimes you want to know whether two parallelized subroutines offer better performance if they are executed at the same time, limiting the number of cores for each one. You can test this situation using the following line:

```
Parallel.Invoke(Sub() ParallelGenerateAESKeysMaxDegree(2), Sub() ParallelGenerateAESKeysMaxDegree(2))
```

Code snippet from Listing12

The two subroutines will be launched in parallel and each will try to optimize its execution to use two of the four cores of a quad-core microprocessor. The obvious drawback of the previous line is that it uses a static number of cores. Nonetheless, this is just for performance testing purposes.

ParallelOptions also offers two additional properties to control more advanced options:

- CancellationToken — Allows assigning a new System.Threading.CancellationToken instance in order to propagate notification that parallel operations should be cancelled. The usage of this property is covered in detail later in this chapter.
- TaskScheduler — Allows assigning a customized System.Threading.Tasks.TaskScheduler instance. It is usually not necessary to define a customized task scheduler to schedule parallel tasks unless you are working with very specific algorithms.

## Understanding Hardware Threads and Logical Cores

The Environment.ProcessorCount property provides the number of logical cores. However, sometimes the number of logical cores, also known as hardware threads, is different from the number of physical cores.

For example, an Intel Core i7 microprocessor with four physical cores offering hyperthreading technology doubles the number to eight logical cores. Therefore, in this case, Environment.ProcessorCount is eight, not four. The operating system also works with eight logical processors.

All the code created using TPL runs using multiple software threads. Threads are the low-level lanes to run many parts of code in parallel, taking advantage of the presence of multiple cores in the underlying hardware. However, most of the time, the code running in these lanes has some imperfections. It waits for I/O data or other threads to finish, or it causes latency as it waits for data to be fetched from the different caches available in the microprocessor or the system memory. This means that there are idle execution units.

HyperThreading technology offers an increased degree of instruction-level parallelism, by duplicating the architectural states for each physical core in order to mitigate the imperfections of the parallel code running code from a second thread when the first one is waiting. This way, it appears to be a microprocessor with two times the real number of physical cores.

> Logical cores are not the same as real physical cores. Although this technique sometimes improves performance through increased instruction-level parallelism when each physical core has two threads with independent instruction streams, if the software threads don’t have many data dependencies, the performance improvements could be less than expected. It depends on the application.

As TPL uses the number of hardware threads, or logical cores, to optimize its execution, sometimes certain algorithms won’t offer the expected scalability as more cores appear because they aren’t real physical cores.

For example, if an algorithm offered a 6.5x speedup when executed with eight physical cores, it would offer a more reticent 4.5x speedup with a microprocessor with four physical cores and eight logical cores with hyperthreading technology.

## CREATING AND MANAGING TASKS

TPL introduced the new task-based programming model to translate multicore power into application performance without having to work with low-level, more complex and heavyweight, threads. It is very important to understand that tasks aren’t threads. Tasks run using threads. However, it doesn’t mean they replace threads. In fact, all the parallel loops used in the previous examples run by creating tasks, and their parallel and concurrent execution is supported by underlying threads, as shown in Figure 33-8.

![](img/d99870e80390742f93963da7be0b2e61_1077_0.png)

FIGURE 33-8

When you work with tasks, they run their code using underlying threads (software threads, scheduled on certain hardware threads, or logical cores). However, there isn’t a one-to-one relationship between tasks and threads. This means you aren’t creating a new thread each time you create a new task. The CLR creates the necessary threads to support the tasks’ execution needs. Of course, this is a simplified view of what goes on when creating tasks.

Synchronizing code running in multiple threads is indeed complex. Thus, a task-based alternative offers an excellent opportunity to leave some synchronization problems behind, especially those regarding work scheduling mechanisms. The CLR uses work-stealing queues to reduce the locks and to schedule small work chunks without adding a significant overhead. Creating a new thread introduces a big overhead, but creating a new task “steals” work from an existing thread. Therefore, tasks offer a new lightweight mechanism for parts of code capable of taking advantage of multiple cores.

The default task scheduler relies on an underlying thread pool engine. Thus, when you create a new task, it will use the steal-working queues to find the most appropriate thread to enqueue it. It steals work from an existing thread or creates a new one when necessary. The code included in tasks will run in one thread, but this happens under the hood, and the overhead is smaller than manually creating a new thread.

## System.Threading.Tasks.Task

So far, TPL has been creating instances of System.Threading.Tasks.Task under the hood in order to support the parallel execution of the iterations. In addition, calling Parallel.Invoke also creates as many instances of Task as delegates are called.

A Task represents an asynchronous operation. It offers many methods and properties that enable you to control its execution and get information about its status. The creation of a Task is independent of its execution. This means that you have complete control over the execution of the associated operation. The Task class provides the following properties:

> When you launch many asynchronous operations as Task instances, the task scheduler will try to run them in parallel in order to load-balance all the available logical cores at runtime. However, it isn’t convenient to use tasks to run any existing piece of code because tasks add an overhead. Sometimes it doesn’t make sense to use tasks. Although this overhead is smaller than that added by a thread, it is still an overhead that has to be considered. For example, it doesn’t make sense to create tasks to run two lines of code as two independent asynchronous tasks that solve very simple calculations. Remember to measure the speedups achieved between the parallel execution and the sequential version to decide whether parallelism is appropriate or not.

Table 33-2 explains the three possible situations considered in this example.

## TABLE 33-2: Task Read-only Properties

| PROPERTY | DESCRIPTION |
|---|---|
| AsyncState | A state Object supplied when you created the Task instance |
| CreationOptions | The TaskCreationOptions enum value used to provide hints to the task scheduler in order to help it make the best scheduling decisions |
| CurrentId | The unique ID for the Task being executed. It is not equivalent to a thread ID in unmanaged code. |
| Exception | The AggregateException that caused the Task to end prematurely. It is a null value if the Task hasn’t thrown exceptions at all or finished without throwing exceptions. |
