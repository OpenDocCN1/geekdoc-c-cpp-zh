A list of the exceptions contained within an AggregateException available from the InnerExceptions property. As a result, you can iterate over this property to examine each exception and determine the appropriate course of action. Alternatively, as shown in Listing 19.5, you can use the AggregateException.Handle() method, specifying an expression to execute against each exception contained within the AggregateException. One important characteristic of the Handle() method to consider, however, is that it is a predicate. As such, the predicate should return true for any exceptions that the Handle() delegate successfully addresses. If any exception handling invocation returns false for an exception, the Handle() method will throw a new AggregateException that contains the composite list of such exceptions.

You can also observe the state of a faulted task without causing the exception to be rethrown on the current thread by simply looking at the Exception property of the task. Listing 19.6 demonstrates this approach by waiting for the completion of a task¹¹³ that we know will throw an exception.

Listing 19.6: Observing Unhandled Exceptions on a Task Using ContinueWith()

```
using System;
using System.Threading.Tasks;

public class Program
{
    public static void Main()
    {
        bool parentTaskFaulted = false;
        Task task = new(() =>
        {
            throw new InvalidOperationException();
        });
        Task continuationTask = task.ContinueWith(
            (antecedentTask) =>
            {
                parentTaskFaulted = antecedentTask.IsFaulted;
            }, TaskContinuationOptions.OnlyOnFaulted);
```

+   13. As we discussed earlier, waiting for a fault continuation to complete is a strange thing to most of the time it will never be scheduled to run in the first place. This code is provided for illustrative purposes only.