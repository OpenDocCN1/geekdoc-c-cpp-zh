
If the compute-bound task throws an unhandled exception, the exception will be swallowed, stored in a collection, and the thread pool thread is allowed to return to the thread pool. When the Wait method or the Result property is invoked, these members will throw a System.AggregateException object.

The AggregateException type is used to encapsulate a collection of exception objects (which can happen if a parent task spawns multiple child tasks that throw exceptions). It contains an InnerExceptions property that returns a ReadOnlyCollection<T> object. Do not confuse the InnerExceptions property with the InnerException property, which the AggregateException class inherits from the System.Exception base class. For the example above, element 0 of AggregateException's InnerExceptions property would refer to the actual System.OverflowException object thrown by the compute-bound method (Sum).

As a convenience, AggregateException overrides Exception's GetBaseException method. AggregateException's implementation returns the innermost AggregateException that is the root cause of the problem (assuming that there is just one innermost exception in the collection). AggregateException also offers a Flatten method that creates a new AggregateException, whose InnerExceptions property contains a list of exceptions produced by walking the original AggregateException's inner exception hierarchy. Finally, AggregateException also provides a Handle method that invokes a callback method for each exception contained in the AggregateException. The callback can then decide, for each exception, how to handle the exception; the callback returns true to consider the exception handled and false if not. If, after calling Handle, at least one exception is not handled, then a new AggregateException object is created containing just the unhandled exceptions and the new AggregateException object is thrown. Later in this chapter, I show examples using the Flatten and Handle methods.

**Important** If you never call Wait or Result or query a Task's Exception property, then your code never observes that this exception has occurred. This is not ideal, as your program has experienced an unexpected problem that you are not aware of. To help you detect unobserved exceptions, you can register a callback method with TaskScheduler's static UnobservedTaskException event. This event is raised by the CLR's finalizer thread whenever a Task with an unobserved exception is garbage collected. When raised, your event handler method will be passed an UnobservedTaskExceptionEventArgs object containing the unobserved AggregateException.

In addition to waiting for a single task, the Task class also offers two static methods that allow a thread to wait on an array of Task objects. Task's static WaitAny method blocks the calling thread until any of the Task objects in the array have completed. This method returns an Int32 index into the array indicating which Task object completed, causing the thread to wake and continue running. The method returns -1 if the timeout occurs and throws an OperationCanceledException if WaitAny is canceled via a CancellationToken.

Similarly, the Task class has a static WaitAll method that blocks the calling thread until all the Task objects in the array have completed. The WaitAll method returns true if all the Task objects complete and false if a timeout occurs; an OperationCanceledException is thrown if WaitAll is canceled via a `CancellationToken`.

## Cancelling a Task

Of course, you can use a `CancellationTokenSource` to cancel a Task. First, we must revise our Sum method so that it accepts a `CancellationToken`:

```csharp
private static Int32 Sum(CancellationToken ct, Int32 n) {
    Int32 sum = 0;
    for (; n > 0; n--) {

        // The following line throws OperationCanceledException when Cancel
        // is called on the CancellationTokenSource referred to by the token
        ct.ThrowIfCancellationRequested();

        checked { sum += n; }   // if n is large, this will throw System.OverflowException
    }
    return sum;
}
```

In this code, the compute-bound operation’s loop periodically checks to see if the operation has been canceled by calling `CancellationToken`’s `ThrowIfCancellationRequested` method. This method is similar to `CancellationToken`’s `IsCancellationRequested` property shown earlier in the “Cooperative Cancellation” section. However, `ThrowIfCancellationRequested` throws an `OperationCanceledException` if the `CancellationTokenSource` has been canceled. The reason for throwing an exception is because, unlike work items initiated with ThreadPool’s QueueUserWorkItem method, tasks have the notion of having completed and a task can even return a value. So, there needs to be a way to distinguish a completed task from a canceled task, and having the task throw an exception lets you know that the task did not run all the way to completion.

Now, we will create the `CancellationTokenSource` and Task objects as follows:

```csharp
CancellationTokenSource cts = new CancellationTokenSource();
Task<Int32> t = Task.Run(() => Sum(cts.Token, 100000000), cts.Token);

// Sometime later, cancel the CancellationTokenSource to cancel the Task
cts.Cancel(); // This is an asynchronous request, the Task may have completed already

try {
    // If the task got canceled, Result will throw an AggregateException
    Console.WriteLine("The sum is: " + t.Result);   // An Int32 value
}
catch (AggregateException x) {
    // Consider any OperationCanceledException objects as handled.
    // Any other exceptions cause a new AggregateException containing
    // only the unhandled exceptions to be thrown
    x.Handle(e => e is OperationCanceledException);

    // If all the exceptions were handled, the following executes
    Console.WriteLine("Sum was canceled");
}
```

When creating a Task, you can associate a CancellationToken with it by passing it to Task’s constructor (as shown above). If the CancellationToken gets canceled before the Task is scheduled, the Task gets canceled and never executes at all⁴⁸. But if the Task has already been scheduled (by calling the Start method), then the Task’s code must explicitly support cancellation if it allows its operation to be canceled while executing. Unfortunately, while a Task object has a CancellationToken associated with it, there is no way to access it, so you must somehow get the same CancellationToken that was used to create the Task object into the Task’s code itself. The easiest way to write this code is to use a lambda expression and “pass” the CancellationToken as a closure variable (as I’ve done in the previous code example).

## Starting a New Task Automatically When Another Task Completes

In order to write scalable software, you must not have your threads block. This means that calling Wait or querying a task’s Result property when the task has not yet finished running will most likely cause the thread pool to create a new thread, which increases resource usage and hurts performance. Fortunately, there is a better way to find out when a task has completed running. When a task completes, it can start another task. Here is a rewrite of the earlier code that doesn’t block any threads:

```csharp
// Create and start a Task, continue with another task
Task<Int32> t = Task.Run(() => Sum(CancellationToken.None, 10000));

// ContinueWith returns a Task but you usually don’t care
Task cwt = t.ContinueWith(task => Console.WriteLine("The sum is: " + task.Result));
```

Now, when the task executing Sum completes, this task will start another task (also on some thread pool thread) that displays the result. The thread that executes the code above does not block waiting for either of these two tasks to complete; the thread is allowed to execute other code or, if it is a thread pool thread itself, it can return to the pool to perform other operations. Note that the task executing Sum could complete before ContinueWith is called. This will not be a problem because the ContinueWith method will see that the Sum task is complete and it will immediately start the task that displays the result.

Also, note that ContinueWith returns a reference to a new Task object (which my code placed in the cwt variable). Of course, you can invoke various members (like Wait, Result, or even ContinueWith) using this Task object, but usually you will ignore this Task object and will not save a reference to it in a variable.

I should also mention that Task objects internally contain a collection of ContinueWith tasks. So you can actually call ContinueWith several times using a single Task object. When the task completes, all the ContinueWith tasks will be queued to the thread pool. In addition, when calling

⁴⁸ By the way, if you try to cancel a task before it is even started, an InvalidOperationException is thrown.
