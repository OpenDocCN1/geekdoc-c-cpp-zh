
WinRT optimizes the number of threads required to implement a set of concurrent tasks and schedules them efficiently according to the number of available processors. It implements a queuing mechanism to distribute the workload across a set of threads allocated to a thread pool (implemented by using a ThreadPool object). When a program creates a Task object, the task is added to a global queue. When a thread becomes available, the task is removed from the global queue and is executed by that thread. The ThreadPool class implements a number of optimizations and uses a work-stealing algorithm to ensure that threads are scheduled efficiently.

The number of threads created to handle your tasks is not necessarily the same as the number of processors. Depending on the nature of the workload, one or more processors may be busy performing high-priority work for other applications and services. Consequently, the optimal number of threads for your application may be less than the number of processors in the machine. Alternatively, one or more threads in an application may be waiting for long-running memory access, I/O, or network operation to complete, leaving the corresponding processors free. In this, the optimal number of threads might be more than the number of available processors. WinRT follows an iterative strategy, known as a hill-climbing algorithm, to dynamically determine the ideal number of threads for the current workload.

The important point is that all you have to do in your code is divide, or partition, your application into tasks that WinRT takes responsibility for creating the appropriate number of threads based on your computer's processor architecture and workload, associating your tasks with arranging for them to be run efficiently.

> Note
It doesn't matter if you partition your work into too many tasks because WinRT will attempt to run only as many concurrent threads as is practical. In fact, you're encouraged to overpartition your work because this will help ensure that your application scales if you move it to a computer with more processors available.

# Creating, running, and controlling tasks

You can create Task objects by using the Task constructor. This constructor is overloaded, but all versions expect you to provide an Action delegate as a parameter. Chapter 20, "Decoupling application logic and handling events," illustrated that an Action delegate references a method that does not return a value. A Task object invokes this delegate when it is scheduled to run. The following example creates a Task object that uses a delegate to run the method called doWork:

Click here to view code image

```
Task task = new Task(doWork);
...
private void doWork()
{
  // The task runs this code when it is started
}
```

> Tip
The default Action type references a method that takes no parameters. Other overloads of the Task constructor take an Action<object> parameter representing a delegate that refers to a method that takes a single object parameter. With these overloads, you can pass data into the method run by the task. The following code shows an example:

Click here to view code image

```
Action<object> action;
action = doWorkWithObject;
object parameterData = ...;
Task task = new Task(action, parameterData);
...
private void doWorkWithObject(object o)
{
  ...
}
```

After you create a Task object, you can run it using the Start method, like this:

```
Task task = new Task(...);
task.Start();
```

The Start method is overloaded, and you can optionally specify a TaskCreationOptions object to provide hints about how to schedule and run the task.

# More Info

> For more information about the TaskCreationOptions enumeration, consult the documentation describing the .NET class library that is provided with Visual Studio.

Creating and running a task is a very common process, and the Task class provides the static Run method with which you can combine these operations. The Run method takes an Action delegate specifying the operation to perform (like the Task constructor) but runs the task immediately. It returns a reference to the Task object. You can use it like this:

Click here to view code image

```
Task task = Task.Run(() => doWork());
```

When the method run by the task completes, the task finishes, and the thread used to run the task can be recycled to execute another task.

When a task completes, you can arrange for another task to be scheduled immediately by creating a continuation. To this, you call the ContinueWith method of a Task object. When the action performed by the Task object completes, the scheduler automatically creates a new Task object to run the action specified by the ContinueWith method. The method specified by the continuation expects a Task parameter, and the scheduler passes into the method a reference to the task that completed. The value returned by ContinueWith is a reference to the new Task object. The following code example creates a Task object that runs the doWork method and specifies a continuation that runs the doMoreWork method in a new task when the first task completes:

Click here to view code image

```
Task task = new Task(doWork);
task.Start();
Task newTask = task.ContinueWith(doMoreWork);
...
private void doWork()
{
    // The task runs this code when it is started
    ...
}
private void doMoreWork(Task task)
{
    // The continuation runs this code when doWork completes
    ...
}
```

The ContinueWith method is heavily overloaded, and you can provide parameters that specify additional items, including a TaskContinuationOptions value. The TaskContinuationOptions type is an enumeration that contains a superset of the tasks in the TaskCreationOptions enumeration. The additional values include the following:

- NotOnCanceled and OnlyOnCanceled The NotOnCanceled option specifies that the continuation should run only if the previous action completes and is not canceled. The OnlyOnCanceled option specifies that the continuation should run only if the previous action is canceled. The section "Canceling tasks and handling exceptions" later in this chapter describes how to cancel a task.

- NotOnFaulted and OnlyOnFaulted The NotOnFaulted option indicates that the continuation should run only if the previous action completes and does not throw an unhandled exception. The OnlyOnFaulted option causes the continuation to run only if the previous action throws an unhandled exception. The section "Canceling tasks and handling exceptions" provides more information on how to manage exceptions in a task.

- NotRanToCompletion and OnlyRanToCompletion The NotRanToCompletion option specifies that the continuation should run only if the previous action does not complete successfully; it must be canceled or throw an exception. OnlyRanToCompletion causes the continuation to run only if the previous action completes successfully.

The following code example shows how to add a continuation to a task that runs only if the initial action does not throw an unhandled exception:

Click here to view code image

```
Task task2 = ...
task2.Start();
task2.Wait(); // Wait at this point until task2 completes
```

A common requirement of applications that invoke operations in parallel is to synchronize tasks. The Task class provides the Wait method, which implements a simple task-coordination mechanism. Using this method, you can suspend execution of the current thread until the specified task completes, like this:

```
Task task2 = ...
task2.Start();
task2.Wait(); // Wait at this point until task2 completes
```

You can wait for a set of tasks by the static WaitAll and WaitAny methods of the Task class. Both methods take a params array containing a set of Task objects. The WaitAll method waits until all specified tasks have completed, and WaitAny stops until at least one of the specified tasks has finished. You use them like this:

```
Task.WaitAll(task, task2); // Wait for both task and task2 to complete
Task.WaitAny(task, task2); // Wait for either task or task2 to complete

# Using the Task class to implement parallelism

In the next example, you'll use the Task class to parallelize processor-intensive code in an application, and you'll see how this parallelization reduces the time taken for the application to run by spreading the computations across multiple processor cores. The application, called GraphDemo, consists of a page that use an Image control to display a graph. The application plots the points for the graph by performing a complex calculation.

> The exercises in this chapter are intended to be run on a computer with a multicore processor. If you have a single-core CPU, you won't observe the
