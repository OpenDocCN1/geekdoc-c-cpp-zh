
## Code Example: Busy Indicator

```csharp
foreach(
    char busySymbol in Utility.BusySymbols())
{
    if(task.IsCompleted)
    {
        Console.Write('\b');
        break;
    }
    Console.Write(busySymbol);
}
Console.WriteLine();
Console.WriteLine(task.Result);
System.Diagnostics.Trace.Assert(
    task.IsCompleted);
```

```csharp
public class PiCalculator
{
    public static string Calculate(int digits = 100)
    {
        // ...
    }
}
```

```csharp
public class Utility
{
    public static IEnumerable<char> BusySymbols()
    {
        string busySymbols = @"-~\/|";
        int next = 0;
        while(true)
        {
            yield return busySymbols[next];
            next = (next + 1) % busySymbols.Length;
            yield return '\b';
        }
    }
}
```

This listing shows that the data type of the task is `Task<string>`. The generic type includes a `Result` property from which to retrieve the value returned by the `Func<string>` that the `Task<string>` executes.

Note that Listing 19.4 does not make a call to `Wait()`. Instead, reading from the `Result` property automatically causes the current thread to block until the result is available, if it isn’t already; in this case we know that it will already be complete when the result is fetched.

In addition to the `IsCompleted` and `Result` properties on `Task<T>`, several others are worth noting:

- The `IsCompleted` property is set to `true` when a task completes, whether it completed normally or faulted (i.e., ended because it threw an exception). More detailed information on the status of a task can be obtained by reading the `Status` property, which returns a value of type `TaskStatus`. Possible values are `Created`, `WaitingForActivation`, `WaitingToRun`, `Running`, `WaitingForChildrenToComplete`, `RanToCompletion`, `Canceled`, and `Faulted`. `IsCompleted` is `true` whenever the `Status` is `RanToCompletion`, `Canceled`, or `Faulted`. Of course, if the task is running on another thread and you read the status as running, the status could change to completed at any time, including immediately after you read the value of the property. The same is true of many other states—even `Created` could potentially change if a different thread starts it. Only `RanToCompletion`, `Canceled`, and `Faulted` can be considered final states that no longer can be transitioned.

- A task can be uniquely identified by the value of the `Id` property. The static `Task.CurrentId` property provides the identifier for the currently executing `Task` (i.e., the task that is executing the `Task.CurrentId` call). These properties are especially useful when debugging.

- You can use the `AsyncState` to associate additional data with a task. For example, imagine a `List<T>` whose values will be computed by various tasks. Each task could contain the index of the value in the `AsyncState` property. This way, when the task completes, the code can index into the list using the `AsyncState` (first casting it to an `int`).¹

We discuss other useful properties later in this chapter under “Canceling a Task.”

> 5. Be careful when using tasks to asynchronously mutate collections. The tasks might be running on worker threads, and the collection might not be thread safe. It is safer to fill in the collection from the main thread after the tasks are completed.

## Task Continuation

We’ve talked several times about the control flow of a program without ever saying what the most fundamental nature of control flow is: Control flow determines what happens next. When you have a simple control flow like `Console.WriteLine(x.ToString());`, the control flow tells you that when `ToString` completes normally, the next thing that will happen is a call to `WriteLine` with the value returned as the argument. The concept of “what happens next” is called **continuation**; each point in a control flow has a continuation. In our example, the continuation of `ToString` is `WriteLine` (and the continuation of `WriteLine` is whatever code runs in the next statement). The idea of continuation is so elementary to C# programming that most programmers don’t even think about it; it’s part of the invisible air that they breathe. The act of C# programming is the act of constructing continuation upon continuation until the control flow of the entire program is complete.

Notice that the continuation of a given piece of code in a normal C# program will be executed *immediately* upon the completion of that code. When `ToString()` returns, the point of control on the current thread immediately does a synchronous call to `WriteLine`. Notice also that there are actually two possible continuations of a given piece of code: the *normal* continuation and the *exceptional* continuation that will be executed if the current piece of code throws an exception.

Asynchronous method calls, such as starting a `Task`, add an additional dimension to the control flow. With an asynchronous `Task` invocation, the control flow goes immediately only to the statement after the `Task.Start()`, while at the same time, it begins executing within the body of the `Task` delegate. In other words, what happens next when asynchrony is involved is multidimensional. Unlike with exceptions where the continuation is just a different path, with asynchrony continuation is an additional, parallel path.

Asynchronous tasks also allow composition of larger tasks out of smaller tasks by describing asynchronous continuations. Just as with regular control flow, a task can have different continuations to handle error situations, and tasks can be melded together by manipulating their continuations. There are several techniques for doing so, the most explicit of which is the `ContinueWith()` method (see Listing 19.5 and its corresponding output, Output 19.2).

### LISTING 19.5: Calling Task.ContinueWith()

```csharp
using System;
using System.Threading.Tasks;

public class Program
{
    public static void Main()
    {
        Console.WriteLine("Before");
        // Use Task.Factory.StartNew<string>() for
        // TPL prior to .NET 4.5
        Task taskA =
            Task.Run(() =>
                Console.WriteLine("Starting..."))
                .ContinueWith(antecedent =>
                    Console.WriteLine("Continuing A..."));
        Task taskB = taskA.ContinueWith(antecedent =>
            Console.WriteLine("Continuing B..."));
        Task taskC = taskA.ContinueWith(antecedent =>
            Console.WriteLine("Continuing C..."));
        Task.WaitAll(taskB, taskC);
        Console.WriteLine("Finished!");
    }
}
```

### OUTPUT 19.2

![](img/ef6a8a417630b222bfb3f3b949facff0_833_0.png)

The `ContinueWith()` method enables "chaining" two tasks together, such that when the predecessor task—the **antecedent task**—completes, the second task—the **continuation task**—is automatically started asynchronously. In Listing 19.5, for example, `Console.WriteLine("Starting...")` is the antecedent task body and `Console.WriteLine("Continuing A...")` is its continuation task body. The continuation task takes a `Task` as its argument (antecedent), thereby allowing the continuation task's code to access the antecedent task's completion state. When the antecedent task is completed, the continuation task starts automatically, asynchronously executing the second delegate and passing the just-completed antecedent task as an argument to that delegate. Furthermore, since the `ContinueWith()` method returns a Task as well, that Task can be used as the antecedent of yet another Task, and so on, forming a continuation chain of Tasks that can be arbitrarily long.

If you call `ContinueWith()` twice on the same antecedent task (as Listing 19.5 shows with `taskB` and `taskC` representing continuation tasks for `taskA`), the antecedent task (`taskA`) has two continuation tasks, and when the antecedent task completes, both continuation tasks will be executed asynchronously. Notice that the order of execution of the continuation tasks from a single antecedent is indeterminate at compile time. Output 19.2 happens to show `taskC` executing before `taskB`, but in a second execution of the program, the order might be reversed. However, `taskA` will always execute before `taskB` and `taskC` because the latter are continuation tasks of `taskA` and therefore can’t start before `taskA` completes. Similarly, the `Console.WriteLine("Starting...")` delegate will always execute to completion before `taskA` (`Console.WriteLine("Continuing A...")`) because the latter is a continuation task of the former. Furthermore, `Finished!` will always appear last because of the call to `Task.WaitAll(taskB, taskC)` that blocks the control flow from continuing until both `taskB` and `taskC` complete.

Many different overloads of `ContinueWith()` are possible, and some of them take a `TaskContinuationOptions` value to tweak the behavior of the continuation chain. These values are flags, so they can be combined using the logical OR operator (`|`). A brief description of some of the possible flag values appears in Table 19.1; see the online MSDN documentation² for more details.

**TABLE 19.1: List of Available TaskContinuationOptions Enums**

| Enum | Description |
| :--- | :--- |
| None | This is the default behavior. The continuation task will be executed when the antecedent task completes, regardless of its task status. |

> ² MSDN .NET Framework Developer Center, http://msdn.microsoft.com/en-us/library/system.threading.tasks.taskcontinuationoptions(v=vs.110).aspx
