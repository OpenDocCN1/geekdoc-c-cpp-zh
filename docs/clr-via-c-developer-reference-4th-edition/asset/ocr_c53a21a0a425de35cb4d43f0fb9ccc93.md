```
m_cts = null;
} else { An operation is not in flight, start it
Text = "Operation running";
m_cts = new CancellationTokenSource();

// This task uses the default task scheduler and executes on a thread pool thread pool thread
Task<int32> t = Task.Run(() => Sum(m_cts.Token, 20000), m_cts.Token);

// These tasks use the sync context task scheduler and execute on the GUI thread
t.ContinueWith(task => Text = "Result: " + task.Result,
CancellationToken.None, ContinuationOptions.OnlyOnRanToCompletion,
m_syncContextTaskScheduler());

t.ContinueWith(task => Text = "Operation canceled",
CancellationToken.None, ContinuationOptions.OnlyOnCanceled,
m_syncContextTaskScheduler());

t.ContinueWith(task => Text = "Operation faulted",
CancellationToken.None, ContinuationOptions.OnlyOnFaulted,
m_syncContextTaskScheduler());
}
base.OnMouseClicked(e);
```

When you click in the client area of this form, a compute-bound task will start executing on a thread pool. This is good because the GUI thread is not blocked by this time and can respond to other UI operations. However, the code executed by the thread pool should not attempt to update UI components or an InvalidOperationException will be thrown.

When the compute-bound task is done, one of the three continue-with tasks will execute. The tasks are all issued against the synchronization context task scheduler corresponding to the GUI thread, and this scheduler queues the tasks to the GUI thread, allowing the code executed by these tasks to update UI components successfully. All of these tasks update the form's caption via the inherited property.

Because the compute-bound task (Sum) is running on a thread pool, the user can interact with the UI to cancel the operation. In my simple code example, I allow the user to cancel the operation by clicking the form's client area while an operation is running.

You can, of course, define your own class derived from TaskScheduler if you have special task scheduling needs. Microsoft has provided bunch of sample code for tasks and includes the source code for a bunch of task schedulers in the Parallel Extensions Extras package which can be downloaded from: http://msdn.microsoft.com/ParExtExamples. Here are some of the task schedulers included in this package:

+   - IOTScheduler This task scheduler queues tasks to the thread pool's I/O threads instead of its workers threads.

+   - LimitedConcurrencyLevelTaskScheduler This task scheduler allows more than n (a constructor parameter) tasks to execute simultaneously.