System.Threading.Thread object.

The following code demonstrates how to have a thread pool thread call a method asynchronously:

```
```csharp
using System;
using System.Threading;

public static class Program {
    public static void Main() {
        Console.WriteLine("Main thread: queuing an asynchronous operation");
        ThreadPool.QueueUserWorkItem(ComputeBoundOp, 5);
        Console.WriteLine("Main thread: Doing other work here...");
        Thread.Sleep(10000);   // Simulating other work (10 seconds)
        Console.WriteLine("Hit <Enter> to end this program...");
        Console.ReadLine();
    }

    // This method's signature must match the WaitCallback delegate
    private static void ComputeBoundOp(object state) {
        // This method is executed by a thread pool thread

        Console.WriteLine("In ComputeBoundOp: state={0}", state);
        Thread.Sleep(1000);   // Simulates other work (1 second)

        // When this method returns, the thread goes back
        // to the pool and waits for another task
    }
}
```
```

When I compile and run this code, I get the following output:

```
```
Main thread: queuing an asynchronous operation
Main thread: Doing other work here...
In ComputeBoundOp: state=5
```
```

And, sometimes when I run this code, I get this output:

```
```
Main thread: queuing an asynchronous operation
In ComputeBoundOp: state=5
Main thread: Doing other work here...
```
```

The difference in the order of the lines in the output is attributed to the fact that the two methods are running asynchronously with respect to one another. The Windows scheduler determines which thread to schedule first, or it may schedule them both simultaneously if the application is running on a multi-CPU machine.

**Note** If the callback method throws an exception that is unhandled, the CLR terminates the process (unless the host sets its own policy). Unhandled exceptions are discussed in Chapter 20, “Exceptions and State Management.”

**Note** For Windows Store apps, System.Threading.ThreadPool class is not publicly exposed.