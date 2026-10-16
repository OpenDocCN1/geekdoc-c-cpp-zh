```
CancellationToken = cts.Token,
},
x =>
{
    WriteLine($"loop {x} started");
    int sum = 0;
    for (int i = 0; i < 100; i++)
    {
        Task.Delay(2).Wait();
        sum += i;
    }
    WriteLine($"loop {x} finished");
});
}
catch (OperationCanceledException ex)
{
    WriteLine(ex.Message);
}
}
```

When you run the application, you get output similar to the following. Iteration 0, 50, 25, 75, and 1 were all started. This is on a system with a quad-core CPU. With the cancellation, all other iterations were canceled before starting. The iterations that were started are allowed to finish because cancellation is always done in a cooperative way to avoid the risk of resource leaks when iterations are canceled somewhere in between:

```
loop 0 started
loop 50 started
loop 25 started
loop 75 started
loop 1 started
*** token cancelled
loop 75 finished
loop 50 finished
loop 1 finished
loop 0 finished
loop 25 finished
The operation was canceled.
```

# Cancellation of Tasks

The same cancellation pattern is used with tasks. First, a new CancellationTokenSource is created. If you need just one cancellation token, you can use a default token by accessing Task.Factory.CancellationToken. Then, similar to the previous code, the task is canceled after 500 milliseconds. The task doing the major work within a loop receives the cancellation token via the TaskFactory object. The cancellation token is assigned to the TaskFactory by setting it in the constructor. This cancellation token is used by the task to check whether cancellation is requested by checking the IsCancellationRequested property of the CancellationToken (code file CancellationSamples/Program.cs):

```
public void CancelTask()
{
    var cts = new CancellationTokenSource();
```