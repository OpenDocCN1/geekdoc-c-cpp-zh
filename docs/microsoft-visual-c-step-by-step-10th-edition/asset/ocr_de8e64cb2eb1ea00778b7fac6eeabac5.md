```
}
}
```

The Thread.Sleep method simply causes the current thread to wait for the specified period of time. This modification simulates performing additional processing on a thread. It also affects how the Parallel class schedules the tasks, which now run on different threads, resulting in a different sequence that calculates a different value. If you run the app several times, you'll get a different result time.

The general rule is to use Parallel.For and Parallel.ForEach only if you can guarantee that each iteration of the loop is independent and to test your code thoroughly. A similar consideration applies to Parallel.Invoke; use this construct to make method calls only if they're independent and the application doesn't depend on them running in a particular sequence.

# Canceling tasks and handling exceptions

A common requirement of applications that perform long-running operations is the ability to stop those operations if necessary. However, you shouldn't simply abort a task, as this could leave the data in your application in an indeterminate state. Instead, the Task class implements a cooperative cancellation strategy.

Cooperative cancellation enables a task to select a convenient point at which to stop processing and enables it to undo any work it has performed prior to cancellation if necessary.

# The mechanics of cooperative cancellation

Cooperative cancellation is based on the notion of a cancellation token. A cancellation token is a structure that represents a request to cancel one or more tasks.

The method task runs should include a System.Threading.CancellationToken parameter. An application that wants to cancel the tasks sets the Boolean IsRequested property of this parameter to true. The method running in the task can query this property at various points during its processing. If the property is true at any point, it knows that the application has requested the task to be canceled. Also, the method knows what it has done so far, so it can undo any changes if necessary and then finish. Alternatively, the method can simply ignore the request and continue running.