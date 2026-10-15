
}
else
{
    // ...
}
}
else
{
    task.Wait();
    Console.ForegroundColor = ConsoleColor.Green;
    Console.Write("Completed successfully");
}
Console.ForegroundColor = originalColor;
}

## OUTPUT 18.10

```
Cancelled: A task was canceled.
```

As with a parallel loop or task, canceling a PLINQ query requires a CancellationToken, which is available from a CancellationTokenSource. However, rather than overloading every PLINQ query to support the cancellation token, the ParallelQuery<T> object returned by IEnumerable’s AsParallel() method includes a WithCancellation() extension method that simply takes a CancellationToken. As a result, calling Cancel() on the CancellationTokenSource object will request the parallel query to cancel—because it checks the IsCancellationRequested property on the CancellationToken.

As mentioned, canceling a PLINQ query will throw an exception in place of returning the complete result. One common technique for dealing with a possibly canceled PLINQ query is to wrap the query in a try block and catch the OperationCanceledException. A second common technique, used in Listing 18.33, is to pass the CancellationToken both to ParallelEncrypt() and as a second parameter on Run(). This will cause task.Wait() to throw an AggregateException whose InnerException property will be set to a TaskCanceledException. The aggregating exception can then be caught, just as you would catch any other exception from a parallel operation.

## SUMMARY

In this chapter, we started by examining the basic parts of multithreaded programs: the Thread class, which represents an independent “point of control” in a program, and the ThreadPool, which encourages efficient allocation and scheduling of threads to multiple CPUs. However, these APIs are low-level entities that are difficult to work with directly. Starting with Version 4.0, the .NET Framework provides the Parallel Extensions library, which includes the Task Parallel Library (TPL) and Parallel LINQ (PLINQ). Both provide new APIs for creating and scheduling units of work represented by Task objects, executing loops in parallel using Parallel.For() and Parallel.ForEach(), and automatically parallelizing LINQ queries with AsParallel().

We also discussed how C# 5.0 makes programming complex workflows with Task objects much easier by automatically rewriting your programs to manage the continuation “wiring” that composes larger tasks out of smaller tasks.

At the beginning of this chapter, we briefly glossed over some of the difficult problems that developers often face when writing multithreaded programs: atomicity problems, deadlocks, and other “race conditions” that introduce uncertainty and bad behavior into multithreaded programs. The standard way to avoid these problems is to carefully write code that uses “locks” to synchronize access to shared resources; this is the topic of the next chapter.

## 19.
Thread Synchronization

IN CHAPTER 18, WE DISCUSSED the details of multithreaded programming using the Task Parallel Library (TPL) and Parallel LINQ (PLINQ). One topic we specifically avoided, however, was thread synchronization, which prevents race conditions while avoiding deadlocks. Thread synchronization is the topic of this chapter.

![](img/25683ccec0773ba5b8794b11f2b12877_853_0.png)

We begin with a multithreaded example with no thread synchronization around shared data—resulting in a race condition in which data integrity is lost. This discussion serves as the introduction for why we need thread synchronization. It is followed by coverage of a myriad of mechanisms and best practices for doing it.

Prior editions of this book included a significant section on additional multithreading patterns and another on various timer callback mechanisms. With the introduction of the async/await pattern, however, those approaches have essentially been replaced unless you are programming with frameworks prior to C# 5.0/.NET 4.5. However, pre-C# 5.0 material still available from this book’s website—http://www.IntelliTect.com/EssentialCSharp.

This entire chapter uses the TPL, so the samples cannot be compiled on frameworks prior to .NET Framework 4. However, unless specifically identified as a .NET Framework 4 API, the only reason for the .NET Framework 4 restriction is the use of the System.Threading.Tasks.Task class to execute the asynchronous operation. Modifying the code to instantiate a System.Threading.Thread and use a Thread.Join() to wait for the thread to execute will allow the vast majority of samples to compile on earlier frameworks.

That being said, the specific API for starting tasks throughout this chapter is the .NET 4.5–specific System.Threading.Tasks.Task.Run(). As we discussed in Chapter 18, this method is preferred over System.Threading.Tasks.Task.Factory.StartNew() because it is simpler and sufficient for the majority of scenarios. Those readers limited to .NET 4 can replace Task.Run() with Task.Factory.StartNew() without any additional modifications. (For this reason the chapter does not explicitly highlight such code as .NET 4.5–specific code when only this method is used.)

Furthermore, Microsoft has released the Reactive Extensions to .NET (Rx), a separate download that adds support for the TPL and PLINQ within the .NET 3.5 Framework.¹ This framework also includes the concurrent and synchronization types introduced in this chapter. For this reason, code listings that depend on Task or that introduce C# 4.0 synchronization classes are, in fact, available from .NET 3.5 using the functionality backported to the .NET 3.5 Framework via Rx and a reference to the System.Threading.dll assembly. Reactive Extensions also includes functionality for leveraging LINQ with delegates. The full library is now available via open source at https://github.com/Reactive-Extensions/Rx.NET.

In summary, most of the samples in the chapter will require only minor modification to work with .NET prior to .NET 4.5, either by using

1. See http://bit.ly/Rx3point5

## OUTPUT 19.1

```
Count = 113449949
```

The important thing to note about Listing 19.1 is that the output is not 0. It would have been if Decrement() was called directly (sequentially). However, when calling Decrement() asynchronously, a race condition occurs because the individual steps within _Count++ and _Count-- statements inter mingle. (As discussed in the Beginner Topic titled “Multithreading Jargon” in Chapter 18, a single statement in C# will likely involve multiple steps.) Consider the sample execution in Table 19.1.

## TABLE 19.1: Sample Pseudocode Execution

| Main Thread | Decrement Thread | Count |
| ... | ... | ... |
| Copy the value 0 out of _Count. |  | 0 |
| Increment the copied value (0), resulting in 1. |  | 0 |
| Copy the resultant value (1) into _Count. |  | 1 |
| Copy the value 1 out of _Count. |  | 1 |
|  | Copy the value 1 out of _Count. | 1 |
| Increment the copied value (1), resulting in 2. |  | 1 |
| Copy the resultant value (2) into _Count. |  | 2 |
|  | Decrement the copied value (1), resulting in 0. | 2 |
|  | Copy the resultant value (0) into _Count. | 0 |
| ... | ... | ... |

Table 19.1 shows a parallel execution (or a thread context switch) by the transition of instructions appearing from one column to the other. The value

of _Count after a particular line has completed appears in the last column. In this sample execution, _Count++ executes twice and _Count-- occurs once. However, the resultant _Count value is 0, not 1. Copying a result back to _Count essentially wipes out any _Count value changes that have occurred since the read of _Count on the same thread.

The problem in Listing 19.1 is a race condition, where multiple threads have simultaneous access to the same data elements. As this sample execution demonstrates, allowing multiple threads to access the same data elements is likely to undermine data integrity, even on a single-processor computer. To remedy this potential problem, the code needs synchronization around the data. Code or data synchronized for simultaneous access by multiple threads is **thread-safe.**

There is one important point to note about atomicity of reading and writing to variables. The runtime guarantees that a type whose size is no bigger than a native (pointer-size) integer will not be read or written partially. With a 64-bit operating system, therefore, reads and writes to a long (64 bits) will be atomic. However, reads and writes to a 128-bit variable such as decimal may not be atomic. Therefore, write operations to change a decimal variable may be interrupted after copying only 32 bits, resulting in the reading of an incorrect value, known as a **torn read.**

## BEGINNER TOPIC

## Multiple Threads and Local Variables

Note that it is not necessary to synchronize local variables. Local variables are loaded onto the stack and each thread has its own logical stack. Therefore, each local variable has its own instance for each method call. By default, local variables are not shared across method calls; likewise, they are not shared among multiple threads.

However, this does not mean local variables are entirely without concurrency issues—after all, code could easily expose the local variable to multiple threads.² A parallel for loop that shares a local variable between iterations, for example, will expose the variable to concurrent access and a race condition (see Listing 19.2).

2. While at the C# level it’s a local, at the IL level it’s a field—and fields can be accessed from multiple threads.
