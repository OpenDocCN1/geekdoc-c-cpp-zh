# Chapter 20: Programming the Task-Based Asynchronous Pattern

```
Task.WaitAll(taskB, taskC);
    DisplayStatus("Finished!");
}

private static void DisplayStatus(string message)
{
    string text = $"{{Thread.CurrentThread.ManagedThreadId}}: {message}}";

    Console.WriteLine(text);
}
```

# OUTPUT 20.3

+   1: Before
3: Starting...
4: Continuing A...
3: Continuing C...
4: Continuing B...
1: Finished!

What is noteworthy about this output is that the thread ID changes sometimes and gets repeated at other times. In this kind of plain console application, the synchronization context (accessible from SynchronizationContext.Current) is null—the default synchronization context causes the thread pool to handle thread allocation instead. This explains why the thread ID changes between tasks: Sometimes the thread pool decides that it is more efficient to use a new thread, and sometimes it decides that the best course of action is to use an existing thread.

Fortunately, the synchronization context gets set automatically for types of applications where that is critical. For example, if the code creating tasks is running in a thread created by ASP.NET, the thread will have a synchronization context of AspSynchronizationContext associated with it. In, if your code is running in a Windows UI application—namely, Windows Presentation Foundation (WPF) or Windows Forms—the thread will have an instance of DispatcherSynchronizationContext or WindowsSynchronizationContext, respectively. (For console applications and Windows Services, the thread will have an instance of the default