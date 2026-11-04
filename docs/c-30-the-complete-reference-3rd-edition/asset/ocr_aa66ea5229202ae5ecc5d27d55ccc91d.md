```
Thread.Sleep(1000); // let child execute a bit longer
Console.WriteLine("Stopping thread.");
mt1.Thrd.Abort(100); // this will stop the thread
mt1.Thrd.Join(); // wait for thread to terminate
Console.WriteLine("Main thread terminating.");
}
```

The output is shown here:

```
My Thread starting.
1 2 3 4 5 6 7 8 9 10
11 12 13 14 15 16 17 18 19 20
21 22 23 24 25 26 27 28 29 30
31 32 33 34 35 36 37 38 39 40
Stopping thread.
Abort Cancelled! Code is 0
41 42 43 44 45 46 47 48 49 50
51 52 53 54 55 56 57 58 59 60
61 62 63 64 65 66 67 68 69 70
71 72 73 74 75 76 77 78 79 80
Stopping thread.
Thread aborting, code is 100
Main thread terminating.
```

In this example, if Abort() is called with an argument that equals zero, then the abort request is cancelled by the thread by calling ResetAbort(), and the thread's execution continues. Any other value causes the thread to stop.

# Suspending and Resuming a Thread

In early versions of the .NET Framework, a thread could be suspended by calling Thread.Suspend() and resumed by calling Thread.Resume(). Today, however, both of these methods are marked as obsolete and should not be used for new code. One reason is that Suspend() is inherently dangerous because it can be used to suspend a thread that is currently holding a lock, thus preventing the lock from being released, resulting in deadlock. This can cause a systemwide problem. You must use C#'s other synchronization features, such as a mutex, to suspend and resume a thread.

# Determining a Thread's State

The state of a thread can be obtained from the ThreadState property provided by Thread. It is shown here:

```
public ThreadState ThreadState{ get; }
```