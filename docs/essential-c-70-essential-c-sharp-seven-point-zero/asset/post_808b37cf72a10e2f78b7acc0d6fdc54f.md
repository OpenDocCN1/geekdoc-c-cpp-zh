
# 20 Thread Synchronization

In Chapter 19, we discussed the details of multithreaded programming using the Task Parallel Library (TPL) and Parallel LINQ (PLINQ). One topic we specifically avoided, however, was thread synchronization, which prevents race conditions while avoiding deadlocks. Thread synchronization is the topic of this chapter.

![](img/ef6a8a417630b222bfb3f3b949facff0_899_0.png)

We begin with a multithreaded example with no thread synchronization around shared data—resulting in a race condition in which data integrity is lost. This discussion serves as the introduction for why we need thread synchronization. It is followed by coverage of myriad mechanisms and best practices for doing it.

Prior editions of this book included a significant section on additional multithreading patterns and another on various timer callback mechanisms. With the introduction of the async/await pattern, however, those approaches have essentially been replaced unless you are programming with frameworks prior to C# 5.0/.NET 4.5. However, pre-C# 5.0 material is still available from this book's website: https://IntelliTect.com/EssentialCSharp.

This entire chapter uses the TPL, so the samples cannot be compiled on frameworks prior to Microsoft .NET Framework 4. However, unless specifically identified as a Microsoft .NET Framework 4 API, the only reason for the Microsoft .NET Framework 4 restriction is the use of the System.Threading.Tasks.Task class to execute the asynchronous operation. Modifying the code to instantiate a System.Threading.Thread and use a Thread.Join() to wait for the thread to execute will allow the vast majority of samples to compile on earlier frameworks.

That being said, the specific API for starting tasks throughout this chapter is the .NET 4.5 (or later) System.Threading.Tasks.Task.Run(). As we discussed in Chapter 19, this method is preferred over System.Threading.Tasks.Task.Factory.StartNew() because it is simpler and sufficient for the majority of scenarios. If you are limited to .NET 4, you can replace Task.Run() with Task.Factory.StartNew() without any additional modifications. (For this reason, the chapter does not explicitly highlight such code as .NET 4.5-specific code when only this method is used.)

## Why Synchronization?

Running a new thread is a relatively simple programming task. What makes multithreaded programming difficult, however, is identifying which data multiple threads can safely access simultaneously. The program must synchronize such data to prevent simultaneous access, thereby creating the “safety.” Consider Listing 20.1.

### LISTING 20.1: Unsynchronized State

```csharp
using System;
using System.Threading.Tasks;

public class Program
{
    const int _Total = int.MaxValue;
    static long _Count = 0;

    public static void Main()
    {
        // Use Task.Factory.StartNew for .NET 4.0
        Task task = Task.Run(() => Decrement());

        // Increment
        for (int i = 0; i < _Total; i++)
        {
            _Count++;
        }

        task.Wait();
        Console.WriteLine("Count = {0}", _Count);
    }

    static void Decrement()
    {
        // Decrement
        for (int i = 0; i < _Total; i++)
        {
            _Count--;
        }
    }
}
```

One possible result of Listing 20.1 appears in Output 20.1.

### **Output 20.1**

![](img/ef6a8a417630b222bfb3f3b949facff0_901_0.png)

The important thing to note about Listing 20.1 is that the output is not 0. It would have been if Decrement() was called directly (sequentially). However, when calling Decrement() asynchronously, a race condition occurs because the individual steps within `_Count++` and `_Count--` statements intermingle. (As discussed in the Beginner Topic titled “Multithreading Jargon” in Chapter 19, a single statement in C# will likely involve multiple steps.) Consider the sample execution in Table 20.1.

### **TABLE 20.1: Sample Pseudocode Execution**

| Main Thread | Decrement Thread | Count |
| :--- | :--- | :---: |
| ... | ... | ... |
| Copy the value 0 out of `_Count`. | | 0 |
| Increment the copied value (0), resulting in 1. | | 0 |
| Copy the resultant value (1) into `_Count`. | | 1 |
| Copy the value 1 out of `_Count`. | | 1 |
| | Copy the value 1 out of `_Count`. | 1 |
| Increment the copied value (1), resulting in 2. | | 1 |
| Copy the resultant value (2) into `_Count`. | | 2 |
| | Decrement the copied value (1), resulting in 0. | 2 |
| | Copy the resultant value (0) into `_Count`. | 0 |
| ... | ... | ... |

Table 20.1 shows a parallel execution (or a thread context switch) by the transition of instructions appearing from one column to the other. The value of `_Count` after a particular line has completed appears in the last column. In this sample execution, `_Count++` executes twice and `_Count--` occurs once. However, the resultant `_Count` value is 0, not 1. Copying a result back to `_Count` essentially wipes out any `_Count` value changes that have occurred since the read of `_Count` on the same thread.

The problem in Listing 20.1 is a race condition, where multiple threads have simultaneous access to the same data elements. As this sample execution demonstrates, allowing multiple threads to access the same data elements is likely to undermine data integrity, even on a single-processor computer. To remedy this potential problem, the code needs synchronization around the data. Code or data synchronized for simultaneous access by multiple threads is thread-safe.

There is one important point to note about atomicity of reading and writing to variables. The runtime guarantees that a type whose size is no bigger than a native (pointer-size) integer will not be read or written partially. With a 64-bit operating system, therefore, reads and writes to a `long` (64 bits) will be atomic. However, reads and writes to a 128-bit variable such as `decimal` may not be atomic. Therefore, write operations to change a `decimal` variable may be interrupted after copying only 32 bits, resulting in the reading of an incorrect value, known as a torn read.

### BEGINNER TOPIC

### Multiple Threads and Local Variables

Note that it is not necessary to synchronize local variables. Local variables are loaded onto the stack, and each thread has its own logical stack. Therefore, each local variable has its own instance for each method call. By default, local variables are not shared across method calls; likewise, they are not shared among multiple threads.

However, this does not mean local variables are entirely without concurrency issues—after all, code could easily expose the local variable to multiple threads.¹ A parallel for loop that shares a local variable between iterations, for example, will expose the variable to concurrent access and a race condition (see Listing 20.2).

### LISTING 20.2: Unsynchronized Local Variables

```csharp
using System;
using System.Threading.Tasks;

public class Program
{
    public static void Main()
    {
        int x = 0;
        Parallel.For(0, int.MaxValue, i =>
        {
            x++;
            x--;
        });
        Console.WriteLine("Count = {0}", x);
    }
}
```

¹ While at the C# level it’s a local, at the Common Intermediate Language level it’s a field—and fields can be accessed from multiple threads.

In this example, `x` (a local variable) is accessed within a parallel for loop, so multiple threads will modify it simultaneously, creating a race condition very similar to that in Listing 20.1. The output is unlikely to yield the value 0 even though `x` is incremented and decremented the same number of times.

## Synchronization Using Monitor

To synchronize multiple threads so that they cannot execute particular sections of code simultaneously, you can use a **monitor** to block the second thread from entering a protected code section before the first thread has exited that section. The monitor functionality is part of a class called `System.Threading.Monitor`, and the beginning and end of protected code sections are marked with calls to the static methods `Monitor.Enter()` and `Monitor.Exit()`, respectively.

Listing 20.3 demonstrates synchronization using the `Monitor` class explicitly. As this listing shows, it is important that all code between calls to `Monitor.Enter()` and `Monitor.Exit()` be surrounded with a try/finally block. Without this block, an exception could occur within the protected section and `Monitor.Exit()` may never be called, thereby blocking other threads indefinitely.

### LISTING 20.3: Synchronizing with a Monitor Explicitly

```csharp
using System;
using System.Threading;
using System.Threading.Tasks;

public class Program
{
    readonly static object _Sync = new object();
    const int _Total = int.MaxValue;
    static long _Count = 0;

Begin 4.0
```
