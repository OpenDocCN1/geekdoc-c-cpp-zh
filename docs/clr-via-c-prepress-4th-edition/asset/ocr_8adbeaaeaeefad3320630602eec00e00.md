```
WaitingForChildrenToComplete,

// A task's final state is one of these:
RanToCompletion,
Canceled,
Faulted
}
```

When you first construct a Task object, its status is Created. Later, when the task is started, its status changes to WaitingToRun. When the Task is actually running on a thread, its status changes to Running. When the task stops running and is waiting for any child tasks, the status changes to WaitingForChildrenToComplete. When a task is completely finished, it enters one of three final states: RanToCompletion, Canceled, or Faulted. When a Task<TResult> runs to completion, you can query the task’s result via Task<TResult>'s Result property. When a Task or Task<TResult> faults, you can obtain the unhandled exception that the task threw by querying Task’s Exception property; which always returns an AggregateException object whose collection contains the set of unhandled exceptions.

For convenience, Task offers several read-only, Boolean properties: IsCanceled, IsFaulted, and IsCompleted. Note that IsCompleted returns true when the Task is in the RanToCompletion, Canceled, or Faulted state. The easiest way to determine if a Task completed successfully is to use code like this:

```
if (task.Status == TaskStatus.RanToCompletion) ...
```

A Task object is in the WaitingForActivation state if that Task is created by calling one of these functions: ContinueWith, ContinueWhenAll, ContinueWhenAny, or FromAsync. A Task created by constructing a TaskCompletionSource<TResult> object is also created in the WaitingForActivation state. This state means that the Task’s scheduling is controlled by the task infrastructure. For example, you cannot explicitly start a Task object that was created by calling ContinueWith. This Task will start automatically when its antecedent task has finished executing.

# Task Factories

Occasionally, you might want to create a bunch of Task objects that share the same configuration. To keep you from having to pass the same parameters to each Task’s constructor over and over again, you can create a task factory that encapsulates the common configuration. The System.Threading.Tasks namespace defines a TaskFactory type as well as a TaskFactory<TResult> type. Both of these types are derived from System.Object; that is, they are peers of each other.

If you want to create a bunch of tasks that return void, then you will construct a TaskFactory. If you want to create a bunch of tasks that have a specific return type, then you will construct a TaskFactory<TResult> where you pass the task’s desired return type for the generic TResult argument. When you create one of these task factory classes, you pass to its constructor the defaults that you want the task factory creates to have. Specifically, you pass to the task factory the