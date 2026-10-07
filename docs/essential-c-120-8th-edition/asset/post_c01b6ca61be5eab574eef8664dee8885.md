
delegate's antecedentTask is a reference to the antecedent task (task), from outside the delegate listeners we can effectively discard the reference to the original task. We can then rely solely on the continuation tasks that begin asynchronously without any need for follow-up code that checks the status of the original task.

In this case, we called completedTask.Wait() so that the main thread does not exit the program before the completed output appears (see Output 19.2).

## Output 19.2

Task State: Completed

In this case, invoking completedTask.Wait() is somewhat contrived because we know that the original task will complete successfully. However, invoking Wait() on canceledTask or faultedTask will result in an exception. Those continuation tasks run only if the antecedent task is canceled or throws an exception; given that will not happen in this program, tasks will never be scheduled to run, and waiting for them completion would throw an exception. The continuation options in Listing 19.1 happen to be mutually exclusive, so when the antecedent task runs to completion and the task associated with completedTask executes, the task scheduler automatically cancels the tasks associated with canceledTask and faultedTask. The canceled tasks have their state set to Canceled. Therefore, calling Wait() (or any other invocation that would cause the current thread to wait for a task completion) on either of these tasks will throw an exception indicating that they are canceled. A less contrived approach might to call Task.WaitAny(completedTask, canceledTask, faultedTask), which will throw an AggregateException that needs to be handled.

## Unhandled Exception Handling on Task with AggregateException

When calling a method synchronously, we can wrap it in a try block with a catch clause to identify to the compiler which code we want to execute when an exception occurs. This does not work with an asynchronous call, however. We cannot simply wrap a try block around a call to Start() to catch an exception, because control immediately returns from the call, and control will then leave the try block, possibly long before the exception occurs on the worker thread. One solution is to wrap body of the task delegate with a try/catch block. Exceptions thrown on and subsequently caught by the worker thread will consequently not present problems, as a try block will work normally on the worker thread. This is not the case, however, for unhandled exceptions—those that the worker thread does not catch.

Generally (starting with version 2.0¹ of the CLR), unhandled exceptions on any thread will be treated as fatal, triggering the system error reporting dialog, and cause the application to terminate abnormally. All exceptions on all threads must be caught; if they are not, the application is not allowed to continue to run. (For some advanced techniques for dealing with unhandled exceptions, see the upcoming “Advanced Topic: Dealing with Unhandled Exceptions on a Thread.”) Fortunately, this is not the case for unhandled exceptions in an asynchronously running task. In such a case, the task scheduler inserts a catchall handler around the delegate so that if the task throws an unhandled exception, the catchall handler will catch it and record the details of the exception in the task, avoiding any trigger of the CLR automatically terminating the process.

As we in Listing 19.4, one technique for dealing with a faulted task is to explicitly create a continuation task that is the fault handler for task; the task scheduler will automatically schedule the continuation when it detects that the antecedent task threw an unhandled exception. If no such handler is present, however, and Wait() (or an attempt to get the Result) executes on a faulted task, an AggregateException will be thrown (see Listing 19.5 and Output 19.3).

Listing 19.5: Handling a Task's Unhandled Exception

```c
using System;
using System.Threading.Tasks;

public static class Program
{
    public static void Main()
{
```

¹² In version 1.0 of the CLR, an unhandled exception on a worker thread terminated the thread but not the application. As a result, it was possible for a buggy program to have all its worker threads die, but the main thread would continue to run, even though the program was no longer doing any work. This is a confusing situation for users to be; it is better to signal to the user that the application is in a bad state and terminate it before it can do any more harm.

```c
// Use Task.Factory.StartNew<string>() for
// // TPL prior to .NET 4.5
Task task = Task.Run(() =>
{
    throw new InvalidOperationException();
});

try {
    task.Wait();
} catch (AggregateException exception) {
    exception.Handle(eachException =>
    {
        Console.WriteLine("ERROR: {eachException.Message}");
        return true;
    });
}
}
```

## OUTPUT 19.3

ERROR: Operation is not valid due to the current state of the object.

The aggregate exception is so called because it may contain many exceptions collected from one or more faulted tasks. Imagine, for example, asynchronously executing ten tasks in parallel and five of them throwing exceptions. To report all five exceptions and have them handled in a single catch block, the framework uses the AggregateException as a means of collecting the exceptions and reporting them as a single exception. Furthermore, since it is unknown at compile time a worker thread will throw one or more exceptions, an unhandled faulted task will always throw an AggregateException. Listing 19.5 and Output 19.3 demonstrate this behavior. Even though the unhandled exception thrown on the worker thread was of type InvalidOperationException, the type of the exception caught on the main thread is AggregateException. Also, as expected, to catch the exception requires an AggregateException catch block.

The aggregate exception is so called because it may contain many exceptions collected from one or more faulted tasks. Imagine, for example, asynchronously executing ten tasks in parallel and five of them throwing exceptions. To report all five exceptions and have them handled in a single catch block, the framework uses the AggregateException as a means of collecting the exceptions and reporting them as a single exception. Furthermore, since it is unknown at compile time a worker thread will throw one or more exceptions, an unhandled faulted task will always throw an AggregateException. Listing 19.5 and Output 19.3 demonstrate this behavior. Even though the unhandled exception thrown on the worker thread was of type InvalidOperationException, the type of the exception caught on the main thread is AggregateException. Also, as expected, to catch the exception requires an AggregateException catch block.

The aggregate exception is so called because it may contain many exceptions collected from one or more faulted tasks. Imagine, for example, asynchronously executing ten tasks in parallel and five of them throwing exceptions. To report all five exceptions and have them handled in a single catch block, the framework uses the AggregateException as a means of collecting the exceptions and reporting them as a single exception. Furthermore, since it is unknown at compile time a worker thread will throw one or more exceptions, an unhandled faulted task will always throw an AggregateException. Listing 19.5 and Output 19.3 demonstrate this behavior. Even though the unhandled exception thrown on the worker thread was of type InvalidOperationException, the type of the exception caught on the main thread is AggregateException. Also, as expected, to catch the exception requires an AggregateException catch block.

The aggregate exception is so called because it may contain many exceptions collected from one or more faulted tasks. Imagine, for example, asynchronously executing ten tasks in parallel and five of them throwing exceptions. To report all five exceptions and have them handled in a single catch block, the framework uses the AggregateException as a means of collecting the exceptions and reporting them as a single exception. Furthermore, since it is unknown at compile time a worker thread will throw one or more exceptions, an unhandled faulted task will always throw an AggregateException. Listing 19.5 and Output 19.3 demonstrate this behavior. Even though the unhandled exception thrown on the worker thread was of type InvalidOperationException, the type of the exception caught on the main thread is AggregateException. Also, as expected, to catch the exception requires an AggregateException catch block.

The aggregate exception is so called because it may contain many exceptions collected from one or more faulted tasks. Imagine, for example, asynchronously executing ten tasks in parallel and five of them throwing exceptions. To report all five exceptions and have them handled in a single catch block, the framework uses the AggregateException as a means of collecting the exceptions and reporting them as a single exception. Furthermore, since it is unknown at compile time a worker thread will throw one or more exceptions, an unhandled faulted task will always throw an AggregateException. Listing 19.5 and Output 19.3 demonstrate this behavior. Even though the unhandled exception thrown on the worker thread was of type InvalidOperationException, the type of the exception caught on the main thread is AggregateException. Also, as expected, to catch the exception requires an AggregateException catch block.

The aggregate exception is so called because it may contain many exceptions collected from one or more faulted tasks. Imagine, for example, asynchronously executing ten tasks in parallel and five of them throwing exceptions. To report all five exceptions and have them handled in a single catch block, the framework uses the AggregateException as a means of collecting the exceptions and reporting them as a single exception. Furthermore, since it is unknown at compile time a worker thread will throw one or more exceptions, an unhandled faulted task will always throw an AggregateException. Listing 19.5 and Output 19.3 demonstrate this behavior. Even though the unhandled exception thrown on the worker thread was of type InvalidOperationException, the type of the exception caught on the main thread is AggregateException. Also, as expected, to catch the exception requires an AggregateException catch block.

The aggregate exception is so called because it may contain many exceptions collected from one or more faulted tasks. Imagine, for example, asynchronously executing ten tasks in parallel and five of them throwing exceptions. To report all five exceptions and have them handled in a single catch block, the framework uses the AggregateException as a means of collecting the exceptions and reporting them as a single exception. Furthermore, since it is unknown at compile time a worker thread will throw one or more exceptions, an unhandled faulted task will always throw an AggregateException. Listing 19.5 and Output 19.3 demonstrate this behavior. Even though the unhandled exception thrown on the worker thread was of type InvalidOperationException, the type of the exception caught on the main thread is AggregateException. Also, as expected, to catch the exception requires an AggregateException catch block.

The aggregate exception is so called because it may contain many exceptions collected from one or more faulted tasks. Imagine, for example, asynchronously executing ten tasks in parallel and five of them throwing exceptions. To report all five exceptions and have them handled in a single catch block, the framework uses the AggregateException as a means of collecting the exceptions and reporting them as a single exception. Furthermore, since it is unknown at compile time a worker thread will throw one or more exceptions, an unhandled faulted task will always throw an AggregateException. Listing 19.5 and Output 19.3 demonstrate this behavior. Even though the unhandled exception thrown on the worker thread was of type InvalidOperationException, the type of the exception caught on the main thread is AggregateException. Also, as expected, to catch the exception requires an AggregateException catch block.

The aggregate exception is so called because it may contain many exceptions collected from one or more faulted tasks. Imagine, for example, asynchronously executing ten tasks in parallel and five of them throwing exceptions. To report all five exceptions and have them handled in a single catch block, the framework uses the AggregateException as a means of collecting the exceptions and reporting them as a single exception. Furthermore, since it is unknown at compile time a worker thread will throw one or more exceptions, an unhandled faulted task will always throw an AggregateException. Listing 19.5 and Output 19.3 demonstrate this behavior.

To examine the exceptions contained within the AggregateException, you can iterate over the InnerExceptions property. Alternatively, as shown in 19.5, you can use the Handle() method, specifying an expression to execute against each exception. One important characteristic of the Handle() method to consider, however, is that it is a predicate. As such, if the predicate returns false for any exception, the Handle() method will throw a new AggregateException that contains such exceptions.

Listing 19.6: Observing Unhandled Exceptions on a Task Using ContinueWith()

```c
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
    }
}
```

```c
task.Start();
continuationTask.Wait();
if (!parentTaskFaulted)
{
    throw new Exception("Parent task should be faulted");
}
if (!task.IsFaulted)
{
    throw new Exception("Task should be faulted");
}
```

```c
task.Exception!.Handle(eachException) =>
{
    Console.WriteLine(
        "$ERROR: {eachException.Message}");
    return true;
}
```

To retrieve the unhandled exception on the original task, we use the Exception property (as well as dereferencing with the null-forgiveness operator, because we know the value will not be null). The result is output identical to Output 19.3.
