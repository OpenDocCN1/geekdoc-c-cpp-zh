```
Monitor.Pulse(this); // let Tick() run
Monitor.Wait(this); // wait for Tick() to complete
}

class MyThread {
  public Thread Thrd;
  TickTock ttOb;

  // Construct a new thread.
  public MyThread(string name, TickTock tt) {
    Thrd = new Thread(this.Run);
    ttOb = tt;
    Thrd.Name = name;
    Thrd.Start();
  }

  // Begin execution of new thread.
  void Run() {
    if (Thrd.Name == "Tick") {
      for (int i=0; i<5; i++) ttOb.Tick(true);
      ttOb.Tick(false);
    }
    else {
      for (int i=0; i<5; i++) ttOb.Tock(true);
      ttOb.Tock(false);
    }
  }
}

class TickingClock {
  static void Main() {
    TickTock tt = new TickTock();
    MyThread mt1 = new MyThread("Tick", tt);
    MyThread mt2 = new MyThread("Tock", tt);

    mt1.Thrd.Join();
    mt2.Thrd.Join();
    Console.WriteLine("Clock Stopped");
  }
}
```

The proper Tick Tock output is the same as before.

As long as the method being synchronized is not defined by a public class or called on a public object, then whether you use lock or MethodImplAttribute is your decision. Both produce the same results. Because lock is a keyword built into C#, that is the approach the examples in this book will use.

> **REMEMBER** Do not use MethodImplAttribute with public classes or with public instances. Instead, use lock, locking on a private object (as explained earlier).