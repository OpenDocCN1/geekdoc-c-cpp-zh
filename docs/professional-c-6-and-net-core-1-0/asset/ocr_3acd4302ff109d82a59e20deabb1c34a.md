```
}
catch (Exception ex)
{
    // just display the exception information of the first task
    // that is awaited within WhenAll
    WriteLine($"handled {ex.Message}");
}
}
```

One way to get the exception information from all tasks is to declare the task variables t1 and t2 outside of the try block, so they can be accessed from within the catch block. Here you can check the status of the task to determine whether they are in a faulted state with the IsFaulted property. In case of an exception, the IsFaulted property returns true. The exception information itself can be accessed by using Exception.InnerException of the Task class. Another, and usually better, way to retrieve exception information from all tasks is demonstrated next.

# Using AggregateException Information

To get the exception information from all failing tasks, you can write the result from Task.WhenAll to a Task variable. This task is then awaited until all tasks are completed. Otherwise the exception would still be missed. As described in the last section, with the catch statement only the exception of the first task can be retrieved. However, now you have access to the Exception property of the outer task. The Exception property is of type AggregateException. This exception type defines the property InnerExceptions (not only InnerException), which contains a list of all the exceptions that have been awaited for. Now you can easily iterate through all the exceptions:

```
private static async void ShowAggregatedException()
{
    Task taskResult = null;
    try
    {
        Task t1 = ThrowAfter(2000,"first");
        Task t2 = ThrowAfter(1000,"second");
        await (taskResult = Task.WhenAll(t1, t2));
    }
    catch (Exception ex)
    {
        WriteLine($"handled {ex.Message}");
        foreach (var ex1 in taskResult.Exception.InnerExceptions)
        {
            WriteLine($"inner exception {ex1.Message}");
        }
    }
}
```

# Cancellation

With background tasks that can run longer in some scenarios, it is useful to cancel the tasks. For cancellation, .NET offers a standard mechanism. This mechanism can be used with the task-based