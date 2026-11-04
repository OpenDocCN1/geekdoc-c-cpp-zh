```
Console.WriteLine("Main thread starting.");
// First, construct a MyThread object.
MyThread mt = new MyThread("Child #1");
do {
    Console.Write(".");
    Thread.Sleep(100);
} while (mt.Count != 10);
Console.WriteLine("Main thread ending.");
}
```

This version produces the same output as before. Notice that the thread object is stored in Thrd inside MyThread.

# Creating Multiple Threads

The preceding examples have created only one child thread. However, your program can spawn as many threads as it needs. For example, the following program creates three child threads:

```
// Create multiple threads of execution.
using System;
using System.Threading;

class MyThread {
    public int Count;
    public Thread Thrd;

    public MyThread(string name) {
        Count = 0;
        Thrd = new Thread(this.Run);
        Thrd.Name = name;
        Thrd.Start();
    }

    // Entry point of thread.
    void Run() {
        Console.WriteLine(Thrd.Name + " starting.");
        do {
            Thread.Sleep(500);
            Console.WriteLine("In " + Thrd.Name + ", Count is " + Count);
            Count++;
        } while (Count < 10);
        Console.WriteLine(Thrd.Name + " terminating.");
    }
}
```