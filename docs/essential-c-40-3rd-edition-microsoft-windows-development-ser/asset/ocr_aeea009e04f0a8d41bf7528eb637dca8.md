```
ThreadPool.QueueUserWorkItem(
    state =>
    {
        throw new Exception(
            "Arbitrary Exception");
    });

// ...
// Wait for the unhandled exception to fire
// ADVANCED: Use ManualResetEvent to avoid
// timing dependent code.
Thread.Sleep(100000);

Console.WriteLine("Still running...");
}
finally
{
    Console.WriteLine("Exiting...");
}
}
```

```
static void OnUnhandledException(
    object sender,
    UnhandledExceptionEventArgs eventArgs)
{
    Exception exception =
        (Exception)eventArgs.ExceptionObject;
    Console.WriteLine("ERROR ({0}): ---> {1}",
        exception.GetType().Name,
        exception.Message,
        exception.InnerException.Message);
}
```

```
public static void ThrowException()
{
    throw new ApplicationException(
        "Arbitrary exception");
}
```

OUTPUT 18.10:

```
Still running...
Exiting...
ERROR (AggregateException):One or more errors occurred. ---> Arbitrary
Exception
```