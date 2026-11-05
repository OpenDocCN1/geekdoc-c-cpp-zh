
// Wait for TimeintensiveMethod to complete and get its result
int x = await task;
Console.WriteLine("Count: " + x);
}

private async Task<int> TimeintensiveMethod(object file)
{
    Console.WriteLine("Start TimeintensiveMethod.");

    // Do some time intensive calculations...
    using (StreamReader reader = new StreamReader(file.ToString()))
    {
        string s = await reader.ReadToEndAsync();

        for (int i = 0; i < 1000; i++)
            s.GetHashCode();
    }
    Console.WriteLine("End TimeintensiveMethod.");

    // return something as a "result"
    return new Random().Next(100);
}

### Section 113.4: BackgroundWorker

See below for a simple example of how to use a BackgroundWorker object to perform time-intensive operations in a background thread.

You need to:

- 1. Define a worker method that does the time-intensive work and call it from an event handler for the DoWork event of a BackgroundWorker.
- 2. Start the execution with RunWorkerAsync. Any argument required by the worker method attached to DoWork can be passed in via the DoWorkEventArgs parameter to RunWorkerAsync.

In addition to the DoWork event the BackgroundWorker class also defines two events that should be used for interacting with the user interface. These are optional.

- The RunWorkerCompleted event is triggered when the DoWork handlers have completed.
- The ProgressChanged event is triggered when the ReportProgress method is called.

```
public void ProcessDataAsync()
{
    // Start the time intensive method
    BackgroundWorker bw = new BackgroundWorker();
    bw.DoWork += BwDoWork;
    bw.RunWorkerCompleted += BwRunWorkerCompleted;
    bw.RunWorkerAsync("@PATH_TO_SOME_FILE");

    // Control returns here before TimeintensiveMethod returns
    Console.WriteLine("You can read this while TimeintensiveMethod is still running.");
}

// Method that will be called after BwDoWork exits
private void BwRunWorkerCompleted(object sender, RunWorkerCompletedEventArgs e)
{
    // we can access possible return values of our Method via the Parameter e
    Console.WriteLine("Count: " + e.Result);
}
```

```
// execution of our time intensive Method
private void BwDoWork(object sender, DoWorkEventArgs e)
{
    e.Result = TimeintensiveMethod(e.Argument);
}

private int TimeintensiveMethod(object file)
{
    Console.WriteLine("Start TimeintensiveMethod.");

    // Do some time intensive calculations...
    using (StreamReader reader = new StreamReader(file.ToString()))
    {
        string s = reader.ReadToEnd();

        for (int i = 0; i < 10000; i++)
            s.GetHashCode();
    }
    Console.WriteLine("End TimeintensiveMethod.");

    // return something as a "result"
    return new Random().Next(100);
}
```

### Section 113.5: Task

See below for a simple example of how to use a Task to do some time intensive stuff in a background process.

All you need to do is wrap your time intensive method in a Task.Run() call.

```
public void ProcessDataAsync()
{
    // Start the time intensive method
    Task<int> t = Task.Run(() => TimeintensiveMethod(@"PATH_TO_SOME_FILE"));

    // Control returns here before TimeintensiveMethod returns
    Console.WriteLine("You can read this while TimeintensiveMethod is still running.");

    Console.WriteLine("Count: " + t.Result);
}
```

```
private int TimeintensiveMethod(object file)
{
    Console.WriteLine("Start TimeintensiveMethod.");

    // Do some time intensive calculations...
    using (StreamReader reader = new StreamReader(file.ToString()))
    {
        string s = reader.ReadToEnd();

        for (int i = 0; i < 10000; i++)
            s.GetHashCode();
    }
    Console.WriteLine("End TimeintensiveMethod.");

    // return something as a "result"
    return new Random().Next(100);
}
```

### Section 113.6: Thread

See below for a simple example of how to use a Thread to do some time intensive stuff in a background process.

```
public async void ProcessDataAsync()
{
    // Start the time intensive method
    Thread t = new Thread(TimeintensiveMethod);

    // Control returns here before TimeintensiveMethod returns
    Console.WriteLine("You can read this while TimeintensiveMethod is still running.");
}

private void TimeintensiveMethod()
{
    Console.WriteLine("Start TimeintensiveMethod.");

    // Do some time intensive calculations...
    using (StreamReader reader = new StreamReader(@"PATH_TO_SOME_FILE"))
    {
        string v = reader.ReadToEnd();

        for (int i = 0; i < 10000; i++)
            v.GetHashCode();
    }
    Console.WriteLine("End TimeintensiveMethod.");
}
```

As you can see we can not return a value from our TimeIntensiveMethod because Thread expects a void Method as its parameter.

To get a return value from a Thread use either an event or the following:

```
int ret;
Thread t = new Thread(() =>
{
    Console.WriteLine("Start TimeintensiveMethod.");

    // Do some time intensive calculations...
    using (StreamReader reader = new StreamReader(file))
    {
        string s = reader.ReadToEnd();

        for (int i = 0; i < 10000; i++)
            s.GetHashCode();
    }
    Console.WriteLine("End TimeintensiveMethod.");

    // return something to demonstrate the coolness of await-async
    ret = new Random().Next(100);
});

t.Start();
t.Join(1000);
Console.WriteLine("Count: " + ret);
```

## Chapter 114: Async-Await

In C#, a method declared async won't block within a synchronous process, in case you're using I/O based operations (e.g. web access, working with files, ...). The result of such async marked methods may be awaited via the use of the await keyword.

### Section 114.1: Await operator and async keyword

await operator and async keyword come together:

> The asynchronous method in which await is used must be modified by the async keyword.

The opposite is not always true: you can mark a method as async without using await in its body.

What await actually does is to suspend execution of the code until the awaited task completes; any task can be awaited.

Note: you cannot await for async method which returns nothing (void).

Actually, the word 'suspends' is a bit misleading because not only the execution stops, but the thread may become free for executing other operations. Under the hood, await is implemented by a bit of compiler magic: it splits a method into two parts - before and after await. The latter part is executed when the awaited task completes.

If we ignore some important details, the compiler roughly does this for you:

```
public async Task<TResult> DoIt()
{
    // do something and acquire someTask of type Task<TSomeResult>
    var awaitedResult = await someTask;
    // ... do something more and produce result of type TResult
    return result;
}
```

becomes:

```
public Task<TResult> DoIt()
{
    // ...
    return someTask.ContinueWith(task => {
        var result = ((Task<TSomeResult>)task).Result;
        return DoIt_Continuation(result);
    });
}
private TResult DoIt_Continuation(TSomeResult awaitedResult)
{
    // ...
}
```

Any usual method can be turned into async in the following way:

```
await Task.Run(() => YourSyncMethod());
```

This can be advantageous when you need to execute a long running method on the UI thread without freezing the

UI.

But there is a very important remark here: **Asynchronous does not always mean concurrent (parallel or even multi-threaded)**. Even on a single thread, async-await still allows for asynchronous code. For example, see this custom task scheduler. Such a 'crazy' task scheduler can simply turn tasks into functions which are called within message loop processing.

We need to ask ourselves: What thread will execute the continuation of our method DoIt_Continuation?

By default the await operator schedules the execution of continuation with the current Synchronization context. It means that by default for WinForms and WPF continuation runs in the UI thread. If, for some reason, you need to change this behavior, use method Task.ConfigureAwait():

```
await Task.Run(() => YourSyncMethod()).ConfigureAwait(continueOnCapturedContext: false);
```

### Section 114.2: Concurrent calls

It is possible to await multiple calls concurrently by first invoking the awaitable tasks and then awaiting them.

```
public async Task RunConcurrentTasks()
{
    var firstTask = DoSomethingAsync();
    var secondTask = DoSomethingElseAsync();

    await firstTask;
    await secondTask;
}
```

Alternatively, Task.WhenAll can be used to group multiple tasks into a single Task, which completes when all of its passed tasks are complete.

```
public async Task RunConcurrentTasks()
{
    var firstTask = DoSomethingAsync();
    var secondTask = DoSomethingElseAsync();

    await Task.WhenAll(firstTask, secondTask);
}
```

You can also do this inside a loop, for example:

```
List<Task> tasks = new List<Task>();
while (something) {
    // do stuff
    Task someAsyncTask = someAsyncMethod();
    tasks.Add(someAsyncTask);
}
await Task.WhenAll(tasks);
```

To get results from a task after awaiting multiple tasks with Task.WhenAll, simply await the task again. Since the task is already completed it will just return the result back

```
var task1 = SomeOpAsync();
var task2 = SomeOtherOpAsync();
```
