
## Part I: C# Fundamentals

![](img/a977a875c7c627b45d939729705a252e_319_0.png)

Figure 10-2

Figure 10-3 shows graphically the two different threads of execution.

![](img/a977a875c7c627b45d939729705a252e_319_1.png)

Figure 10-3

As shown in Figure 10-2, it just so happens that before the DoSomething() method gets the chance to execute, the main thread has proceeded to execute its next statements. Hence, the output shows the main thread executing before the DoSomething() method. In reality, both threads have an equal chance of executing, and one of the many possible outputs could be:

```
Doing something...
Doing something...
Continuing with the execution...
Doing something...
Doing something...
...
```

A thread executes until:

- [ ] It reaches the end of its life (method exits), or
- [ ] You prematurely kill (abort) it.

### Aborting a Thread

You can use the Abort() method of the Thread class to abort a thread after it has started executing.
Here's an example:

```
class Program
{
    static void Main(string[] args)
    {
        Thread t = new Thread(new ThreadStart(DoSomething));
        t.Start();
        Console.WriteLine("Continuing with the execution...");

        while (!t.IsAlive) ;

        Thread.Sleep(1);
        t.Abort();

        Console.ReadLine();
    }

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
    }
}
```

When the thread is started, you continue with the next statement and print out the message "Continuing with the execution..." . You then use the IsAlive property of the Thread class to find out the execution status of the thread and block the execution of the Main() function (with the while statement) until the thread has a chance to start. The Sleep() method of the Thread class blocks the current thread (Main()) for a specified number of milliseconds. Using this statement, you are essentially giving the DoSomething() function a chance to execute. Finally, you kill the thread by using the Abort() method of the Thread class.

## Part I: C# Fundamentals

The ThreadAbortException exception is fired on any thread that you kill. Ideally, you should clean up the resources in this exception handler (via the finally statement):

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

The output of the preceding program may look like this:

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

Notice that I say the program may look like this. When you have multiple threads running in your application, you don't have control over which threads are executed first. The OS determines the actual execution sequence and that is dependent on several factors such as CPU utilization, memory usage, and so on. It is possible, then, that the output may look like this:

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

While you can use the Abort() method to kill a thread, it is always better to exit it gracefully whenever possible.

Here's a rewrite of the previous program:

```
class Program
{
    private static volatile bool _stopThread = false;

    static void Main(string[] args)
    {
        Thread t = new Thread(new ThreadStart(DoSomething));
        t.Start();

        Console.WriteLine("Continuing with the execution...");

        while (!t.IsAlive) ;
        Thread.Sleep(1);
        _stopThread = true;
        Console.WriteLine("Thread ended.");
        Console.ReadLine();
    }

    static void DoSomething()
    {
        try
        {
            while (! _stopThread)
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
}
```

First, you declare a static Boolean variable called _stopThread:

```
private static volatile bool _stopThread = false;
```

Notice that you prefix the declaration with the volatile keyword, which is used as a hint to the compiler that this variable will be accessed by multiple threads. The variable will then not be subjected to compiler optimization and will always have the most up-to-date value.

To use the _stopThread variable to stop the thread, you modify the DoSomething() function, like this:

```
while (! _stopThread)
{
    Console.WriteLine("Doing something...");
}
```

## Part I: C# Fundamentals

Finally, to stop the thread in the `Main()` function, you just need to set the `_stopThread` variable to `true`:

```
_stopThread = true;
Console.WriteLine("Thread ended.");
```

The output of this program *may* look like this:

```
Continuing with the execution.
Doing something...
Doing something...
Doing something...
Doing something...
Doing something...
Doing something...
Thread ended.
Doing something...
```

The `DoSomething()` function may print another message after the `"Thread ended."` message. That's because the thread might not end immediately. To ensure that the `"Thread ended."` message is printed only after the `DoSomething()` function ends, you can use the `Join()` method of the `Thread` class to join the two threads:

```
static void Main(string[] args)
{
    Thread t = new Thread(new ThreadStart(DoSomething));
    t.Start();

    Console.WriteLine("Continuing with the execution...");

    while (!t.IsAlive) ;

    Thread.Sleep(1);
    _stopThread = true;

    //---joins the current thread (Main()) to t---
    t.Join();
    Console.WriteLine("Thread ended.");
    Console.ReadLine();
}
```

The `Join()` method essentially blocks the calling thread until the thread terminates. In this case, the Thread ended message will be blocked until the thread (`t`) terminates.

The output of the program now looks like this:

```
Continuing with the execution.
Doing something...
Doing something...
Doing something...
Doing something...
Doing something...
Doing something...
Thread ended.
```

Figure 10-4 shows graphically the two different threads of execution.

![](img/a977a875c7c627b45d939729705a252e_324_0.png)

Figure 10-4

### Passing Parameters to Threads

In the past few examples, you've seen how to create a thread using the ThreadStart delegate to point to a method. So far, though, the method that you have been pointing to does not have any parameters:

```csharp
static void DoSomething()
{
    ...
    ...
}
```

What if the function you want to invoke as a thread has a parameter? In that case, you have two choices:

- Wrap the function inside a class, and pass in the parameter via a property.
- Use the ParameterizedThreadStart delegate instead of the ThreadStart delegate.

Using the same example, the first choice is to wrap the DoSomething() method as a class and then expose a property to take in the parameter value:

```csharp
class Program
{
    static void Main(string[] args)
    {
        SomeClass sc = new SomeClass();
        sc.msg = "useful";
        Thread t = new Thread(new ThreadStart(sc.DoSomething));
        t.Start();
    }
}

class SomeClass
```

(continued)

```
{
    public string msg { get; set; }
    public void DoSomething()
    {
        try
        {
            while (true)
            {
                Console.WriteLine("Doing something... {0}", msg);
            }
        }
        catch (ThreadAbortException ex)
        {
            Console.WriteLine(ex.Message);
        }
        finally
        {
            //---clean up your resources here---
        }
    }
}
```

In this example, you create a thread for the DoSomething() method by creating a new instance of the SomeClass class and then passing in the value through the msg property.

For the second choice, you use the ParameterizedThreadStart delegate instead of the ThreadStart delegate. The ParameterizedThreadStart delegate takes a parameter of type object, so if the function that you want to invoke as a thread has a parameter, that parameter must be of type object.

To see how to use the ParameterizedThreadStart delegate, modify the DoSomething() function by adding a parameter:

```csharp
static void DoSomething(object msg)
{
    try
    {
        while (true)
        {
            Console.WriteLine("Doing something... {0}", msg);
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
