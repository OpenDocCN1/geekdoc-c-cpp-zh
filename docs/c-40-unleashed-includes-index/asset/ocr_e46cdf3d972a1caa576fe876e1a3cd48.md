```
static void Main()
{
    var t1 = new Thread(() =>
    {
        for (int i = 0; i < 10; i++)
        {
            Console.WriteLine("Background says {0}", i);
            Thread.Sleep(500);
        }
    }) { IsBackground = true };

    var t2 = new Thread(() =>
    {
        for (int i = 0; i < 10; i++)
        {
            Console.WriteLine("Foreground says {0}", i);
            Thread.Sleep(100);
        }
    });

    t1.Start();
    t2.Start();
}
```

This code prints all the messages from the foreground thread, which is keeping the process alive. However, when the foreground thread completes in about 1 second, the background thread won’t have a chance to execute further because the sole thread that kept the process alive has exited.

Notice there are three threads in this example: the two that have been created using our code, and one for the main thread. Can you infer whether the main thread is foreground or background? Observe how the Main method can finish without taking down the process. Why is that? Because some foreground thread keeps the process alive.

What happens if the main thread is still going but all other threads in the program have finished? Clearly, you don’t want your program’s main thread to be terminated abruptly because some of your other threads have finished their duties. In other words, the main thread needs to keep the process alive as well, having a chance to reach its end. That’s exactly what it means to be a foreground thread:

```
static void Main(string[] args)
{
    // Prints false
    Console.WriteLine(Thread.CurrentThread.IsBackground);
}
```