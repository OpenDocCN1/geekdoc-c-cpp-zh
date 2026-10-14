# More info

For more information about the *TaskCreationOptions* enumeration, consult the documentation describing the .NET Framework class library that is provided with Visual Studio.

Creating and running a task is a very common process, and the *Task* class provides the static *Run* method with which you can combine these operations. The *Run* method takes an *Action* delegate specifying the operation to perform (like the *Task* constructor), but starts the task running immediately. It returns a reference to the *Task* object. You can use it like this:

Click here to view code image

```
Task task = Task.Run(() => doWork());
```

When the method run by the task completes, the task finishes, and the thread used to run the task can be recycled to execute another task.

When a task completes, you can arrange for another task to be scheduled immediately by creating a *continuation*. To do this, call the *ContinueWith* method of a *Task* object. When the action performed by the *Task* object completes, the scheduler automatically creates a new *Task* object to run the action specified by the *ContinueWith* method. The method specified by the continuation expects a *Task* parameter, and the scheduler passes into the method a reference to the task that completed. The value returned by *ContinueWith* is a reference to the new *Task* object. The following code example creates a *Task* object that runs the *doWork* method and specifies a continuation that runs the *doMoreWork* method in a new task when the first task completes:

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
...
private void doMoreWork(Task task)
{
    // The continuation runs this code when doWork completes
    ...
}
```

The *ContinueWith* method is heavily overloaded, and you can provide a