```
{
    Parallel.ForEach(files, (fileName) =>
    {
        Encrypt(fileName);
    });
}
catch (AggregateException exception)
{
    Console.WriteLine(
        "ERROR: {0} :",
        exception.GetType().Name);
    foreach (Exception item in
        exception.InnerExceptions)
    {
        Console.WriteLine(" {0} - {1}",
            item.GetType().Name, item.Message);
    }
}
// ...
}
```

# Output 18.7:

> ERROR: AggregateException:
> UnauthorizedAccessException - Attempted to perform an unauthorized
> operation.
> UnauthorizedAccessException - Attempted to perform an unauthorized
> operation.
> UnauthorizedAccessException - Attempted to perform an unauthorized
> operation.

Output 18.7 shows that three exceptions occurred while executing the Parallel.ForEach<T>(...) loop. However, in the code, there is only one catch of type System.AggregationException. The UnauthorizedAccessExceptions were retrieved from the InnerExceptions property on the AggregationException. With a Parallel.ForEach<T>() loop, each iteration could potentially throw an exception and so the System.AggregationException thrown by the method call will contain each of those exceptions within its InnerExceptions property.

# Canceling a Parallel Loop

Unlike a task which requires an explicit call in order to block until it completes, a parallel loop executes iterations in parallel but still blocks until