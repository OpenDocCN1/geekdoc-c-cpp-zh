provide information about whether it is currently locked: IsHeld and IsHeldByCurrentThread.

> NOTE Be careful when passing SpinLock instances around. Because SpinLock is defined as a struct, assigning one variable to another creates a copy. Always pass SpinLock instances by reference.

# WaitHandle

WaitHandle is an abstract base class that you can use to wait for a signal to be set. You can wait for different things, because WaitHandle is a base class and some classes are derived from it.

Wait handles are also used by simple asynchronous delegates. The TakesAWhileDelegate is defined as follows (code file AsyncDelegate/Program.cs):

```
public delegate int TakesAWhileDelegate(int x, int ms);
```

The method BeginInvoke of the asynchronous delegate returns an object that implements the interface IAsyncResult. Using IAsyncResult, you can access a WaitHandle with the property AsyncWaitHandle. When you invoke the method WaitOne, the thread waits until a signal is received that is associated with the wait handle, or when the timeout occurs. Invoking the EndInvoke method, the thread finally blocks until the result is here:

```
static void Main()
{
    TakesAWhileDelegate d1 = TakesAWhile;

    IAsyncResult ar = d1.BeginInvoke(1, 3000, null, null);
    while (true)
    {
        Write(".");
        if (ar.AsyncWaitHandle.WaitOne(50))
        {
            WriteLine("Can get the result now");
            break;
        }
    }
    int result = d1.EndInvoke(ar);
    WriteLine($"result: {result}");
}

public static int TakesAWhile(int x, int ms)
{
    Task.Delay(ms).Wait();
    return 42;
}
```