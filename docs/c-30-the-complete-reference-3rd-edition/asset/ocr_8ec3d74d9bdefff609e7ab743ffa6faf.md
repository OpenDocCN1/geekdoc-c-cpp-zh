```
Thread.Sleep(100);
} while (mt.Count != 10);
}
Console.WriteLine("Main thread ending.");
}
```

Let’s look closely at this program. MyThread defines a class that will be used to create a second thread of execution. Inside its Run() method, a loop is established that counts from 0 to 9. Notice the call to Sleep(), which is a static method defined by Thread. The Sleep() method causes the thread from which it is called to suspend execution for the specified period of milliseconds. When a thread suspends, another thread can run. The form used by the program is shown here:

```
public static void Sleep(int milliseconds)
```

The number of milliseconds to suspend is specified in milliseconds. If milliseconds is zero, the calling thread is suspended only to allow a waiting thread to execute.

Inside Main(), a new Thread object is created by the following sequence of statements:

```
// First, construct a MyThread object.
MyThread mt = new MyThread("Child #1");

// Next, construct a thread from that object.
Thread newThrd = new Thread(mt.Run);

// Finally, start execution of the thread.
newThrd.Start();
```

As the comments suggest, first an object of MyThread is created. This object is then used to construct a Thread object by passing the mt.Run() method as the entry point. Finally, execution of the new thread is started by calling Start(). This causes mt.Run() to begin executing in its own thread. After calling Start(), execution of the main thread returns to Main(), and it enters Main()’s do loop. Both threads continue running, sharing the CPU, until their loops finish. The output produced by this program is as follows. (The precise output that you see may vary slightly because of differences in your execution environment, operating system, and task load.)

```
Main thread starting.
Child #1 starting.
.....In Child #1, Count is 0
.....In Child #1, Count is 1
.....In Child #1, Count is 2
.....In Child #1, Count is 3
.....In Child #1, Count is 4
.....In Child #1, Count is 5
.....In Child #1, Count is 6
.....In Child #1, Count is 7
.....In Child #1, Count is 8
.....In Child #1, Count is 9
Child #1 terminating.
Main thread ending.
```

Often in a multithreaded program, you will want the main thread to be the last thread to finish running. Technically, a program continues to run until all of its foreground threads