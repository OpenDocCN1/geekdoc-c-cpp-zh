```
~~~csharp
    m_cts = null;
} else { // An operation is not in flight, start it
    Text = "Operation running";
    m_cts = new CancellationTokenSource();

    // This task uses the default task scheduler and executes on a thread pool thread
    Task<int> t = Task.Run(() => Sum(m_cts.Token, 20000), m_cts.Token);

    // These tasks use the sync context task scheduler and execute on the GUI thread
    t.ContinueWith(task => Text = "Result: " + task.Result,
        CancellationToken.None, TaskContinuationOptions.OnlyOnRanToCompletion,
        m_syncContextTaskScheduler);

    t.ContinueWith(task => Text = "Operation canceled",
        CancellationToken.None, TaskContinuationOptions.OnlyOnCanceled,
        m_syncContextTaskScheduler);

    t.ContinueWith(task => Text = "Operation faulted",
        CancellationToken.None, TaskContinuationOptions.OnlyOnFaulted,
        m_syncContextTaskScheduler);
    }
base.OnMouseClick(e);
}
}
~~~
```

When you click in the client area of this form, a compute-bound task will start executing on a thread pool thread. This is good because the GUI thread is not blocked during this time and can therefore respond to other UI operations. However, the code executed by the thread pool thread should not attempt to update UI components or else an InvalidOperationException will be thrown.

When the compute-bound task is done, one of the three continue-with tasks will execute. These tasks are all issued against the synchronization context task scheduler corresponding to the GUI thread, and this task scheduler queues the tasks to the GUI thread, allowing the code executed by these tasks to update UI components successfully. All of these tasks update the form's caption via the inherited Text property.

Because the compute-bound work (Sum) is running on a thread pool thread, the user can interact with the UI to cancel the operation. In my simple code example, I allow the user to cancel the operation by clicking in the form's client area while an operation is running.

You can, of course, define your own class derived from TaskScheduler if you have special task scheduling needs. Microsoft has provided a bunch of sample code for tasks and includes the source code for a bunch of task schedulers in the Parallel Extensions Extras package, which can be downloaded from here: [http://code.msdn.microsoft.com/ParExtSamples](http://code.msdn.microsoft.com/ParExtSamples). Here are some of the task schedulers included in this package:

+   - IOTaskScheduler  This task scheduler queues tasks to the thread pool's I/O threads instead of its worker threads.
+   - LimitedConcurrencyLevelTaskScheduler  This task scheduler allows no more than *n* (a constructor parameter) tasks to execute simultaneously.