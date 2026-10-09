```
public static void DoWork()
{
    Console.WriteLine("DoWork() started....");
    DoWorkSignaledResetEvent.Set();
    MainSignaledResetEvent.Wait();
    Console.WriteLine("DoWork() ending....");
}
public static void Main()
{
    using(MainSignaledResetEvent =
    new ManualResetEventSlim())
    using (DoWorkSignaledResetEvent =
    new ManualResetEventSlim())
    {
        Console.WriteLine(
    "Application started....");
        Console.WriteLine("Starting task....");
        // Use Task.Factory.StartNew for .NET 4.0
        Task task = Task.Run( ()=>DoWork());
        // Block until DoWork() has started
        DoWorkSignaledResetEvent.Wait();
        Console.WriteLine(
    " Waiting while thread executes...");
        MainSignaledResetEvent.Set();
        task.Wait();
        Console.WriteLine("Thread completed");
        Console.WriteLine(
    "Application shutting down....");
    }
}
```

**OUTPUT 20.6**

```
Application started....
Starting thread....
DoWork() started....
Waiting while thread executes...
DoWork() ending....
Thread completed
Application shutting down....
```

Listing 20.10 begins by instantiating and starting a new Task. Table 20.3 shows the execution path in which each column represents a thread. In cases where code appears on the same row, it is indeterminate which side executes first.