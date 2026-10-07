# Chapter 20: Programming the Task-Based Asynchronous Pattern

```
process.Start();

cancellationToken.Register(() =>
{
    Process.GetProcessById(process.Id).Kill();
});
```

```
return taskCS.Task;
//...
}
```

Ignore the highlighting for the moment and instead focus on the pattern of using an event for notification when the process completes. Since System Diagnostics.Process includes a notification upon exit, we register for this notification and use it as a callback from which we can invoke TaskCompletionSource.SetResult(). The code in Listing 20.11 follows a fairly pattern that you can use to create an asynchronous method without having to resort to Task.Run().

Another important characteristic that an async method might require is cancellation. TAP relies on the same methods for cancellation the TPL does—namely, a System.Threading.CancellationToken. Listing 20.11 highlights the code necessary to support cancellation. In this example, we allow for canceling before the process starts, as well as an attempt to close the application’s main window (if there is one). A more aggressive approach would be to call Process .Kill(), but this method could potentially cause problems for the program that is executing.

Notice that we don't register for the cancellation event until after the process is started. This avoids any race conditions that might occur if cancellation is triggered before the process actually begins.

One last feature to consider supporting is a progress update. Listing 20.12 is the full version of RunProcessAsync() with just such an update.

# Listing 20.12: Implementing a Custom Asynchronous Method with Progress Support

```
using System;
using System.Diagnostics;
using System.Threading;
using System.Threading.Tasks;
```