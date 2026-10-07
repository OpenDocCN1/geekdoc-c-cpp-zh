
IDisposable

```c
CancellationTokenSource
Sealed Class
  Properties
    IsCancellationRequested
    Token
  Methods
    Cancel (+ 1 overload)
    CancellationTokenSource
    CreateLinkedTokenSource (+ 1 overload)
    Dispose
```

```c
CancellationToken
Struct
  Properties
    CanBeCanceled
    IsCancellationRequested
    None
    WaitHandle
  Methods
    CancellationToken
    Equals(+ 1 overload)
    operator =
    Register (+ 3 overloads)
    ThrowCancellation
```

Figure 19.3: CancellationTokenSource and CancellationToken class diagrams

We guarantee that the code is responsive to cancellation requests by polling frequently.

One other point to note about the CancellationToken is the overloaded Register() method. Via this method, you can register an action that will be invoked whenever the token is canceled. In other words, calling the Register() method subscribes to a listener delegate on the corresponding CancellationTokenSource's Cancel().

Given that canceling before completing is the expected behavior in this program, the code in Line 19.7 does not throw a System.Threading.Tasks.TaskCanceledException. As a consequence, task.Status will return TaskStatus.RanToCompletion—providing no indication that the work of the task was in, canceled. In this example, there is no need for such an indication; the TPL includes the capability to do this. If the cancel call were disruptive in some way—preventing a valid result from returning, for example—throwing a TaskCanceledException (which derives from System.OperationCanceledException) would be for reporting it. Instead of throwing the exception, CancellationToken includes a

ThrowIfCancellationRequested() method to report the exception more easily, assuming an instance of CancellationToken is available.

If you attempt to call Wait() (or obtain the Result) on a task that threw TaskCanceledException, the behavior is the same as if other exception had been thrown in the task: The call will throw an AggregateException. The exception is means of communicating that the state of execution following the task is potentially incomplete. Unlike a successfully completed task in which all expected work executed successfully, a canceled task is potentially incomplete.

In this example, there is no need for such an indication; the TPL includes the capability to do this. If the cancel call were disruptive in some way—preventing a valid result from returning, for example—throwing a TaskCanceledException (which derives from System.OperationCanceledException) would be for reporting it. Instead of throwing the exception, CancellationToken includes a

ThrowIfCancellationRequested() method to report the exception more easily, assuming an instance of CancellationToken is available.

If you attempt to call Wait() (or obtain the Result) on a task that threw TaskCanceledException, the behavior is the same as if other exception had been thrown in the task: The call will throw an AggregateException. The exception is means of communicating that the state of execution following the task is potentially incomplete. Unlike a successfully completed task in which all expected work executed successfully, a canceled task is potentially incomplete.

In this example, there is no need for such an indication; the TPL includes the capability to do this. If the cancel call were disruptive in some way—preventing a valid result from returning, for example—throwing a ...

We guarantee that the code is responsive to cancellation requests by polling frequently.

One other point to note about the CancellationToken is the overloaded Register() method. Via this method, you can register an action that will be invoked whenever the token is canceled. In other words, calling the Register() method subscribes to a listener delegate on the corresponding CancellationTokenSource's Cancel().

Given that canceling before completing is the expected behavior in this program, the code in Line 19.7 does not throw a System.Threading.Tasks.TaskCanceledException. As a consequence, task.Status will return TaskStatus.RanToCompletion—providing no indication that the work of the task was in, canceled. In this example, there is no need for such an indication; the TPL includes the capability to do this. If the cancel call were disruptive in some way—preventing a valid result from returning, for example—throwing a TaskCanceledException (which derives from System.OperationCanceledException) would be for reporting it. Instead of throwing the exception, CancellationToken includes a

ThrowIfCancellationRequested() method to report the exception more easily, assuming an instance of CancellationToken is available.

If you attempt to call Wait() (or obtain the Result) on a task that threw TaskCanceledException, the behavior is the same as if other exception had been thrown in the task: The call will throw an AggregateException. The exception is means of communicating that the state of execution following the task is potentially incomplete. Unlike a successfully completed task in which all expected work executed successfully, a canceled task is potentially incomplete.

In this example, there is no need for such an indication; the TPL includes the capability to do this. If the cancel call were disruptive in some way—preventing a valid result from returning, for example—throwing a ...

We guarantee that the code is responsive to cancellation requests by polling frequently.

One other point to note about the CancellationToken is the overloaded Register() method. Via this method, you can register an action that will be invoked whenever the token is canceled. In other words, calling the Register() method subscribes to a listener delegate on the corresponding CancellationTokenSource's Cancel().

Given that canceling before completing is the expected behavior in this program, the code in Line 19.7 does not throw a System.Threading.Tasks.TaskCanceledException. As a consequence, task.Status will return TaskStatus.RanToCompletion—providing no indication that the work of the task was in, canceled. In this example, there is no need for such an ... ...

We guarantee that the code is responsive to cancellation requests by polling frequently.

One other point to note about the CancellationToken is the overloaded Register() method. Via this method, you can register an action that will be invoked whenever the token is canceled. In other words, calling the Register() method subscribes to a listener delegate on the corresponding CancellationTokenSource's Cancel().

Given that canceling before completing is the expected behavior in this program, the code in Line 19.7 does not throw a System.Threading.Tasks.TaskCanceledException. As a consequence, task.Status will return TaskStatus.RanToCompletion—providing no indication that the work of the task was in, canceled. In this example, there is no need for such an indication; the TPL includes the capability to do this. If the cancel call were disruptive in some way—preventing a valid result from returning, for example—throwing a ...

We guarantee that the code is responsive to cancellation requests by polling frequently.

One other point to note about the CancellationToken is the overloaded Register() method. Via this method, you can register an action that will be invoked whenever the token is canceled. In other words, calling the Register() method subscribes to a listener delegate on the corresponding CancellationTokenSource's Cancel().

Given that canceling before completing is the expected behavior in this program, the code in Line 19.7 does not throw a System.Threading.Tasks.TaskCanceledException. As a consequence, task.Status will return TaskStatus.RanToCompletion—providing no indication that the work of the task was in, canceled. In this example, there is no need for such an indication; the TPL includes the capability to do this. If the cancel call were disruptive in some way—preventing a valid result from returning, for example—throwing a ...

We guarantee that the code is responsive to cancellation requests by polling frequently.

One other point to note about the CancellationToken is the overloaded Register() method. Via this method, you can register an action that will be invoked whenever the token is canceled. In other words, calling the Register() method subscribes to a listener delegate on the corresponding CancellationTokenSource's Cancel().

Given that canceling before completing is the expected behavior in this program, the code in Line 19.7 does not throw a System.Threading.Tasks.TaskCanceledException. As a consequence, task.Status will return TaskStatus.RanToCompletion—providing no indication that the work of the task was in, canceled. In this example, there is no need for such an indication; the TPL includes the capability to do this. If the cancel call were disruptive in some way—preventing a valid result from returning, for example—throwing a ...

We guarantee that the code is responsive to cancellation requests by polling frequently.

One other point to note about the CancellationToken is the overloaded Register() method. Via this method, you can register an action that will be invoked whenever the token is canceled. In other words, calling the Register() method subscribes to a listener delegate on the corresponding CancellationTokenSource's Cancel().

Given that canceling before completing is the expected behavior in this program, the code in Line 19.7 does not throw a System.Threading.Tasks.TaskCanceledException. As a consequence, task.Status will return TaskStatus.RanToCompletion—providing no indication that the work of the task was in, canceled. In this example, there is no need for such an indication; the TPL ...

This example demonstrates how a long-running task-bound can respond to cancellation. In this example, there is no need for such an indication; the TPL includes the capability to do this. If the cancel call were disruptive in some way—preventing a valid result from returning, for example—throwing a TaskCanceledException (which derives from System.OperationCanceledException) would be for reporting it. Instead of throwing the exception, CancellationToken includes a

ThrowIfCancellationRequested() method to report the exception more easily, assuming an instance of CancellationToken is available.

If you attempt to call Wait() (or obtain the Result) on a task that threw TaskCanceledException, the behavior is the same as if other exception had been thrown in the task: The call will throw an AggregateException. The exception is means of communicating that the state of execution following the task is potentially incomplete. Unlike a successfully completed task in which all expected work executed successfully, a canceled task is potentially incomplete.

In this example, there is no need for such an indication; the TPL includes the capability to do this. If the cancel call were disruptive in some way—preventing a valid result from returning, for example—throwing a TaskCanceledException (which derives from System.OperationCanceledException) would be for reporting it. Instead of throwing the exception, CancellationToken includes a

ThrowIfCancellationRequested() method to report the exception more easily, assuming an instance of CancellationToken is available.

If you attempt to call Wait() (or obtain the Result) on a task that threw TaskCanceledException, the behavior is the same as if other exception had been thrown in the task: The call will throw an AggregateException. The exception is means of communicating that the state of execution following the task is potentially incomplete. Unlike a successfully completed task in which all expected work executed successfully, a canceled task is potentially incomplete.

This example demonstrates how a long-running task-bound can respond to cancellation. In this example, there is no need for such an indication; the TPL includes the capability to do this. If the cancel call were disruptive in some way—preventing a valid result from returning, for example—throwing a ...

This example demonstrates how a long-running task-bound can respond to cancellation. In this example, there is no need for such an indication; the TPL includes the capability to do this. If the cancel call ...

assuming an instance of CancellationToken is available.

If you attempt to call Wait() (or obtain the Result) on a task that threw TaskCanceledException, the behavior is the same as if other exception had been thrown in the task: The call will throw an AggregateException. The exception is means of communicating that the state of execution following the task is potentially incomplete. Unlike a successfully completed task in which all expected work executed successfully, a canceled task is potentially incomplete.

This example demonstrates how a long-running task-bound can respond to cancellation. In this example, there is no need for such an indication; the TPL includes the capability to do this. If the cancel call ...

assuming an instance of CancellationToken is available.

If you attempt to call Wait() (or obtain the Result) on a task that threw TaskCanceledException, the behavior is the same as if other exception had been thrown in the task: The call will throw an AggregateException. The exception is means of communicating that the state of execution following the task is potentially incomplete. Unlike a successfully completed task in which all expected work executed successfully, a canceled task is potentially incomplete.

This example demonstrates how a long-running task-bound can respond to cancellation. In this example, there is no need for such an indication; the TPL includes the capability to do this. If the cancel call ...

assuming an instance of CancellationToken is available.

If you attempt to call Wait() (or obtain the Result) on a task that threw TaskCanceledException, the behavior is the same as if other exception had been thrown in the task: The call will throw an AggregateException. The exception is means of communicating that the state of execution following the task is potentially incomplete. Unlike a successfully completed task in which all expected work executed successfully, a canceled task is potentially incomplete.

This example demonstrates how a long-running task-bound can respond to cancellation. In this example, there is no need for such an indication; the TPL includes the capability to do this. If the cancel call ...

assuming an instance of CancellationToken is available.

If you attempt to call Wait() (or obtain the Result) on a task that threw TaskCanceledException, the behavior is the same as if other exception had been thrown in the task: The call will throw an AggregateException. The exception is means of communicating that the state of execution following the task is potentially incomplete. Unlike a successfully completed task in which all expected work executed successfully, a canceled task is potentially incomplete.

This example demonstrates how a long-running task-bound can respond to cancellation. In this example, there is no need for such an indication; the TPL includes the capability to do this. If the cancel call were- ...

assuming an instance of CancellationToken is available.

If you attempt to call Wait() (or obtain the Result) on a task that threw TaskCanceledException, the behavior is the same as if other exception had been thrown in the task: The call will throw an AggregateException. The exception is means of communicating that the state of execution following the task is potentially incomplete. Unlike a successfully completed task in which all expected work executed successfully, a canceled task is potentially incomplete.

This example demonstrates how a long-running task-bound can respond to cancellation. In this example, there is no need for such an indication; the TPL includes the capability ...

One other point to note about the CancellationToken is the overloaded Register() method. Via this method, you can register an action that will be invoked whenever the token is canceled. In other words, calling the Register() method subscribes to a listener delegate on the corresponding CancellationTokenSource's Cancel().

Given that canceling before completing is the expected behavior in this program, the code in Line 19.7 does not throw a System.Threading.Tasks.TaskCanceledException. As a consequence, task.Status will return TaskStatus.RanToCompletion—providing no indication that the work of the task was in, canceled. In this example, there is no need for such an indication; the TPL includes the capability to do this. If the cancel call were disruptive in some way—preventing a valid result from returning, for example—throwing a TaskCanceledException (which derives from System.OperationCanceledException) would be for reporting it. Instead of throwing the exception, CancellationToken includes a

ThrowIfCancellationRequested() method to report the exception more easily, assuming an instance of CancellationToken is available.

If you attempt to call Wait() (or obtain the Result) on a task that threw TaskCanceledException, the behavior is the same as if other exception had been thrown in the task: The call will throw an AggregateException. The exception is means of communicating that the state of execution following the task is potentially incomplete. Unlike a successfully completed task in which all expected work executed successfully, a canceled task is potentially incomplete.

This example demonstrates how a long-running task-bound can respond to cancellation. In this example, there is no need for such an indication; the TPL includes the capability to do this. If the cancel call were disruptive in some way—preventing a valid result from returning, for example—throwing a TaskCanceledException (which derives from System.OperationCanceledException) would be for reporting it. Instead of throwing the exception, CancellationToken includes a

ThrowIfCancellationRequested() method to report the exception more easily, assuming an instance of CancellationToken is available.

If you attempt to call Wait() (or obtain the Result) on a task that threw TaskCanceledException, the behavior is the same as if other exception had been thrown in the task: The call will throw an AggregateException. The exception is means of communicating that the state of execution following the task is potentially incomplete. Unlike a successfully completed task in which all expected work executed successfully, a canceled task is potentially incomplete.

This example demonstrates how a long-running task-bound can respond to cancellation. In this example, there is no need for such an indication; the TPL includes the capability to do this. If the cancel call were disruptive in some way—preventing a valid result from returning, for example—throwing a ...

This example demonstrates how a long-running task-bound can respond to cancellation. In this example, there is no need for such an indication; the TPL includes the capability to do this. If the cancel call were disruptive in some way—preventing a valid result from returning, for example—throwing a TaskCanceledException (which derives from System.OperationCanceledException) would be for reporting it. Instead of throwing the exception, CancellationToken includes a

ThrowIfCancellationRequested() method to report the exception more easily, assuming an instance of CancellationToken is available.

If you attempt to call Wait() (or obtain the Result) on a task that threw TaskCanceledException, the behavior is the same as if other exception had been thrown in the task: The call will throw an AggregateException. The exception is means of communicating that the state of execution following the task is potentially incomplete. Unlike a successfully completed task in which all expected work executed successfully, a canceled task is potentially incomplete.

This example demonstrates how a long-running task-bound can respond to cancellation. In this example, there is no need for such an indication; the TPL includes the capability to do this. If the cancel call were disruptive in some way—preventing a valid result from returning, for example—throwing a ...

This example demonstrates how a long-running task-bound can respond to cancellation. In this example, there is no need for such an indication; the TPL includes the capability to do this. If the cancel call were disruptive in some way—preventing a valid result from returning, for example—throwing a TaskCanceledException (which derives from System.OperationCanceledException) would be for reporting it. Instead of throwing the exception, CancellationToken includes a

ThrowIfCancellationRequested() method to report the exception more easily, assuming an instance of CancellationToken is available.

If you attempt to call Wait() (or obtain the Result) on a task that threw TaskCanceledException, the behavior is the same as if other exception had been thrown in the task: The call will throw an AggregateException. The exception is means of communicating that the state of execution following the task is potentially incomplete. Unlike a successfully completed task in which all expected work executed successfully, a canceled task is potentially incomplete.

This example demonstrates how a long-running task-bound can respond to cancellation. In this example, there is no need for such an indication; the TPL includes the capability to do this. If the cancel call were disruptive in some way—preventing a valid result from returning, for example—throwing a TaskCanceledException (which derives from System.OperationCanceledException) would be for reporting it. Instead of throwing the exception, CancellationToken includes a

ThrowIfCancellationRequested() method to report the exception more easily, assuming an instance of CancellationToken is available.

If you attempt to call Wait() (or obtain the Result) on a task that threw TaskCanceledException, the behavior is the same as if other exception had been thrown in the task: The call will throw an AggregateException. The exception is means of communicating that the state of execution following the task is potentially incomplete. Unlike a successfully completed task in which all expected work executed successfully, a canceled task is potentially incomplete.

This example demonstrates how a long-running task-bound can respond to cancellation. In this example, there is no need for such an indication; the TPL includes the capability to do this. If the cancel call were disruptive in some way—preventing a valid result from returning, for example—throwing a ...

This example demonstrates how a long-running task-bound can respond to cancellation. In this example, there is no need for such an indication; the TPL includes the capability to do this. If the cancel call were disruptive in some way—preventing a valid result from returning, for example—throwing a TaskCanceledException (which derives from System.OperationCanceledException) would be for reporting it. Instead of throwing the exception, CancellationToken includes a

ThrowIfCancellationRequested() method to report the exception more easily, assuming an instance of CancellationToken is available.

If you attempt to call Wait() (or obtain the Result) on a task that threw TaskCanceledException, the behavior is the same as if other exception had been thrown in the task: The call will throw an AggregateException. The exception is means of communicating that the state of execution following the task is potentially incomplete. Unlike a successfully completed task in which all expected work executed successfully, a canceled task is potentially incomplete.

This example demonstrates how a long-running task-bound can respond to cancellation. In this example, there is no need for such an indication; the TPL includes the capability to do this. If the cancel call were disruptive in some way—preventing a valid result from returning, for example—throwing a TaskCanceledException (which derives from System.OperationCanceledException) would be for reporting it. Instead of throwing the exception, CancellationToken includes a

ThrowIfCancellationRequested() method to report the exception more easily, assuming an instance of CancellationToken is available.

If you attempt to call Wait() (or obtain the Result) on a task that threw TaskCanceledException, the behavior is the same as if other exception had been thrown in the task: The call will throw an AggregateException. The exception is means of communicating that the state of execution following the task is potentially incomplete. Unlike a successfully completed task in which all expected work executed successfully, a canceled task is potentially incomplete.

This example demonstrates how a long-running task-bound can respond to cancellation. In this example, there is no need for such an indication; the TPL includes the capability to do this. If the cancel call were disruptive in some way—preventing a valid result from returning, for example—throwing a ...

This example demonstrates how a long-running task-bound can respond to cancellation. In this example, there is no need for such an indication; the TPL includes the capability to do this. If the cancel call were disruptive in some way—preventing a valid result from returning, for example—throwing a TaskCanceledException (which derives from System.OperationCanceledException) would be for reporting it. Instead of throwing the exception, CancellationToken includes a

ThrowIfCancellationRequested() method to report the exception more easily, assuming an instance of CancellationToken is available.

If you attempt to call Wait() (or obtain the Result) on a task that threw TaskCanceledException, the behavior is the same as if other exception had been thrown in the task: The call will throw an AggregateException. The exception is means of communicating that the state of execution following the task is potentially incomplete. Unlike a successfully completed task in which all expected work executed successfully, a canceled task is potentially incomplete.

This example demonstrates how a long-running task-bound can respond to cancellation. In this example, there is no need for such an indication; the TPL includes the capability to do this. If the cancel call were disruptive in some way—preventing a valid result from returning, for example—throwing a TaskCanceledException (which derives from System.OperationCanceledException) would be for reporting it. Instead of throwing the exception, CancellationToken includes a

ThrowIfCancellationRequested() method to report the exception more easily, assuming an instance of CancellationToken is available.

If you attempt to call Wait() (or obtain the Result) on a task that threw TaskCanceledException, the behavior is the same as if other exception had been thrown in the task: The call will throw an AggregateException. The exception is means of communicating that the state of execution following the task is potentially incomplete. Unlike a successfully completed task in which all expected work executed successfully, a canceled task is potentially incomplete.

This example demonstrates how a long-running task-bound can respond to cancellation. In this example, there is no need for such an indication; the TPL includes the capability to do this. If the cancel call were disruptive in some way—preventing a valid result from returning, for example—throwing a ...
