```
// Entry point of thread.
void Run() {
    Console.WriteLine("Inside thread " + Thrd.Name);
    for(int i=0; i<5; i++) {
        Console.WriteLine(Thrd.Name);
        Thread.Sleep(500);
    }
    Console.WriteLine(Thrd.Name + " Done!");
    // Signal the event.
    mre.Set();
}
class ManualEventDemo {
    static void Main() {
        ManualResetEvent evtObj = new ManualResetEvent(false);
        MyThread mt1 = new MyThread("Event Thread 1", evtObj);
        Console.WriteLine("Main thread waiting for event.");
        // Wait for signaled event.
        evtObj.WaitOne();
        Console.WriteLine("Main thread received first event.");
        // Reset the event.
        evtObj.Reset();
        mt1 = new MyThread("Event Thread 2", evtObj);
        // Wait for signaled event.
        evtObj.WaitOne();
        Console.WriteLine("Main thread received second event.");
    }
}
```

The output is shown here. (The actual output you see may vary slightly.)

```
Inside thread Event Thread 1
Event Thread 1
Main thread waiting for event.
Event Thread 1
Event Thread 1
Event Thread 1
Event Thread 1
Event Thread 1 Done!
Main thread received first event.
Inside thread Event Thread 2
```