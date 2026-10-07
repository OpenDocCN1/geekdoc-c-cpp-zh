```
}
}
public class Utility
{
    public static IEnumerable<char> BusySymbols()
    {
        string busySymbols = "@\-/\\|/\";
        int next = 0;
        while(true)
        {
            yield return busySymbols[next];
            next = next + 1 % busySymbols.Length;
            yield return '\b';
        }
    }
}
// / ...
```

This listing shows that the data type of the task is Task<string>. The generic type includes a Result property from which to retrieve the value returned by the Func<string> that the Task<string> executes.

Note that 19.2 does not make a call to Wait(). Instead, reading from the Result property automatically causes the current thread to block until the result is available, if it isn't already; in this case, we know that it will already be complete when the result is fetched.

In addition to the IsCompleted and Result properties on Task<T>, several others are worth noting:

+   - The IsCompleted property is set to true when a task completes, whether it completed normally or faulted (i.e., ended because it threw an exception). More detailed information on the status of a task can be obtained by reading the Status property, which returns a value of type TaskStatus. Possible values are Created, WaitingForActivation, WaitingToRun, Running, WaitingForChildrenToComplete, RanToCompletion, Canceled, Faulted. IsCompleted is true whenever the Status is RanToCompletion, Canceled, or Faulted. Of course, if the task is running on another thread and you read the status as running, the status could change to completed at any time, including immediately after you read the value of the property. The same is true of many other states—even Created could potentially change if a different thread starts it. Only