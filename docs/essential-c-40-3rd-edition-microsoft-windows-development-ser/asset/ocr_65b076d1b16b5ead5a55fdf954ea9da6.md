```
TaskContinuationOptions.OnlyOnCanceled);
Task completedTask = task.ContinueWith(
    (antecedentTask) =>
    {
        Trace.Assert(task.IsCompleted);
        Console.WriteLine("Task State: Completed");
    },
    TaskContinuationOptions.OnlyOnRanToCompletion);
completedTask.Wait();
}
```

In this listing, we effectively register for “events” on the antecedent’s task so that if the event occurs, the particular “listening” task will begin executing. This is a powerful capability, especially when using a fire-and-forget behavior on the task—no Wait()-type behavior is invoked on the task. Instead, we can just call Start() or Factory.StartNew(), register for the “notifications,” and then discard the reference to the task. The task will begin executing asynchronously without any need for follow-up code that “checks” the status. In this case, we leave the completedTask.Wait() call so that the program does not exit before the completed output appears (see Output 18.2).

# OUTPUT 18.2:

```
Task State: Completed.
```

Even if the task hasn’t finished executing, the program will still exit if no explicit wait is specified.

The Wait() method is a means of joining tasks back to the calling thread so that the thread calling Wait() will continue only when the other task (the instance on which Wait() is called) has completed. Typically, this is necessary because one task is relying on the effects or results of the other task.

Note that we can successfully call Wait() on canceledTask or faultedTask; since the task didn’t and won’t complete the work there is nothing to wait for. The continuation options in Listing 18.3 happen to be mutually exclusive, so when the antecedent task runs to completion and