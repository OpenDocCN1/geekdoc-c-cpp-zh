creating continuations that act like event handlers for the antecedent task’s behavior. Listing 18.6 demonstrates how an antecedent task can be given multiple continuations that execute conditionally, depending on how the antecedent task completed.

# LISTING 18.6: Registering for Notifications of Task Behavior with ContinueWith()

```
using System;
using System.Threading.Tasks;
using System.Diagnostics;
using AddisonWesley.Michaelis.EssentialCSharp.Shared;

public class Program
{
    public static void Main()
    {
        // Use Task.Factory.StartNew<string>() for
        // TPL prior to .NET 4.5
        Task<string> task =
            Task.Run<string>(
                () => PiCalculator.Calculate(10));

        Task faultedTask = task.ContinueWith(
            (antecedentTask) =>
            {
                Trace.Assert(antecedentTask.IsFaulted);
                Console.WriteLine(
                    "Task State: Faulted");
            },
            TaskContinuationOptions.OnlyOnFaulted);

        Task canceledTask = task.ContinueWith(
            (antecedentTask) =>
            {
                Trace.Assert(antecedentTask.IsCanceled);
                Console.WriteLine(
                    "Task State: Canceled");
            },
            TaskContinuationOptions.OnlyOnCanceled);

        Task completedTask = task.ContinueWith(
            (antecedentTask) =>
            {
                Trace.Assert(antecedentTask.IsCompleted);
                Console.WriteLine(
                    "Task State: Completed");
            }, TaskContinuationOptions.
                OnlyOnRanToCompletion);
```