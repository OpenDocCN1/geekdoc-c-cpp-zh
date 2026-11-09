Constructing a **Thread** object is a relatively lightweight operation because it does not actually create a physical operating system thread. To actually create the operating system thread and have it start executing the callback method, you must call **Thread's Start** method, passing into it the object (state) that you want passed as the callback method's argument. The following code demonstrates how to create a dedicated thread and have it call a method asynchronously:

```
~~~csharp
using System;
using System.Threading;

public static class Program {
    public static void Main() {
        Console.WriteLine("Main thread: starting a dedicated thread " +
            "to do an asynchronous operation");
        Thread dedicatedThread = new Thread(ComputeBoundOp);
        dedicatedThread.Start();

        Console.WriteLine("Main thread: Doing other work here...");
        Thread.Sleep(10000);      // Simulating other work (10 seconds)

        dedicatedThread.Join();   // Wait for thread to terminate
        Console.WriteLine("Hit <Enter> to end this program...");
        Console.ReadLine();
    }

    // This method's signature must match the ParameterizedThreadStart delegate
    private static void ComputeBoundOp(Object state) {
        // This method is executed by a dedicated thread

        Console.WriteLine("In ComputeBoundOp: state={0}", state);
        Thread.Sleep(1000); // Simulates other work (1 second)

        // When this method returns, the dedicated thread dies
    }
}
~~~
```

When I compile and run this code, I get the following output:

```
~~~text
Main thread: starting a dedicated thread to do an asynchronous operation
Main thread: Doing other work here...
In ComputeBoundOp: state=5
~~~
```

Sometimes when I run this code, I get the following output since I can't control how Windows schedules the two threads:

```
~~~text
Main thread: starting a dedicated thread to do an asynchronous operation
In ComputeBoundOp: state=5
Main thread: Doing other work here...
~~~
```

Notice that the **Main** method calls **Join**. The **Join** method causes the calling thread to stop executing any code until the thread identified by **dedicatedThread** has destroyed itself or been terminated.