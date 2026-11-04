# Part I: C# Fundamentals

The ThreadAbortException exception is fired on any thread that you kill. Ideally, you should clean up the resources in this exception handler (via the finally statement):

```
```csharp
static void DoSomething()
{
    try
    {
        while (true)
        {
            Console.WriteLine("Doing something...");
        }
    }
    catch (ThreadAbortException ex)
    {
        Console.WriteLine(ex.Message);
    }
    finally {
        //---clean up your resources here---
    }
}
```
```

The output of the preceding program may look like this:

```
```
Continuing with the execution...
Doing something...
Doing something...
Doing something...
Doing something...
Doing something...
Doing something...
Doing something...
Thread was being aborted.
```
```

Notice that I say the program may look like this. When you have multiple threads running in your application, you don't have control over which threads are executed first. The OS determines the actual execution sequence and that is dependent on several factors such as CPU utilization, memory usage, and so on. It is possible, then, that the output may look like this:

```
```
Doing something...
Continuing with the execution...
Doing something...
Doing something...
Doing something...
Doing something...
Doing something...
Doing something...
Thread was being aborted.
```
```

While you can use the Abort() method to kill a thread, it is always better to exit it gracefully whenever possible.