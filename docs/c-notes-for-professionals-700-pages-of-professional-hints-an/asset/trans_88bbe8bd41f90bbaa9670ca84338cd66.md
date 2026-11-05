
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

### 第 113.4 节：BackgroundWorker

以下是一个简单的示例，说明如何使用 BackgroundWorker 对象在后台线程中执行耗时操作。

你需要：

- 1. 定义一个执行耗时工作的 worker 方法，并从 BackgroundWorker 的 DoWork 事件的处理程序中调用它。
- 2. 使用 RunWorkerAsync 启动执行。DoWork 附加的工作方法所需的任何参数都可以通过 RunWorkerAsync 的 DoWorkEventArgs 参数传入。

除了 DoWork 事件之外，BackgroundWorker 类还定义了两个用于与用户界面交互的事件。这些是可选的。

- RunWorkerCompleted 事件在 DoWork 处理程序完成时触发。
- ProgressChanged 事件在调用 ReportProgress 方法时触发。

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

### 第 113.5 节：Task

以下是一个简单的示例，说明如何使用 Task 在后台进程中执行一些耗时操作。

你需要做的就是将耗时方法包装在 Task.Run() 调用中。

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

### 第 113.6 节：Thread

以下是一个简单的示例，说明如何使用 Thread 在后台进程中执行一些耗时操作。

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

如你所见，我们无法从 TimeIntensiveMethod 返回值，因为 Thread 要求其参数为 void 方法。

要从 Thread 获取返回值，请使用事件或以下方法：

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

## 第 114 章：Async-Await

在 C# 中，声明为 async 的方法在同步进程中不会阻塞，前提是使用基于 I/O 的操作（例如网络访问、工作文件等）。此类标记为 async 的方法的结果可以通过 await 关键字进行等待。

### 第 114.1 节：Await 运算符和 async 关键字

await 运算符和 async 关键字一起使用：

> 使用 await 的异步方法必须由 async 关键字修饰。

反之则不总是成立：你可以在方法体中不使用 await 的情况下将其标记为 async。

await 实际做的是暂停代码的执行，直到被等待的任务完成；任何任务都可以被等待。

注意：你不能等待返回 nothing（void）的 async 方法。

实际上，“暂停”这个词有点误导，因为不仅执行停止，而且线程可能被释放以执行其他操作。在内部，await 是通过编译器的一些魔法实现的：它将方法拆分为两部分——await 之前和之后。后一部分在被等待的任务完成后执行。

如果忽略一些重要细节，编译器大致会为你执行以下操作：

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

任何普通方法都可以通过以下方式转换为 async：

```
await Task.Run(() => YourSyncMethod());
```

当你需要在 UI 线程上执行长时间运行的方法而不冻结

UI 时，这可能很有优势。

但这里有一个非常重要[content]
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

### 第 113.4 节：BackgroundWorker

以下是一个简单的示例，说明如何使用 BackgroundWorker 对象在后台线程中执行耗时操作。

你需要：

- 1. 定义一个执行耗时工作的 worker 方法，并从 BackgroundWorker 的 DoWork 事件的处理程序中调用它。
- 2. 使用 RunWorkerAsync 启动执行。DoWork 附加的工作方法所需的任何参数都可以通过 RunWorkerAsync 的 DoWorkEventArgs 参数传入。

除了 DoWork 事件之外，BackgroundWorker 类还定义了两个用于与用户界面交互的事件。这些是可选的。

- RunWorkerCompleted 事件在 DoWork 处理程序完成时触发。
- ProgressChanged 事件在调用 ReportProgress 方法时触发。

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

### 第 113.5 节：Task

以下是一个简单的示例，说明如何使用 Task 在后台进程中执行一些耗时操作。

你需要做的就是将耗时方法包装在 Task.Run() 调用中。

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

### 第 113.6 节：Thread

以下是一个简单的示例，说明如何使用 Thread 在后台进程中执行一些耗时操作。

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

如你所见，我们无法从 TimeIntensiveMethod 返回值，因为 Thread 要求其参数为 void 方法。

要从 Thread 获取返回值，请使用事件或以下方法：

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

## 第 114 章：Async-Await

在 C# 中，声明为 async 的方法在同步进程中不会阻塞，前提是使用基于 I/O 的操作（例如网络访问、工作文件等）。此类标记为 async 的方法的结果可以通过 await 关键字进行等待。

### 第 114.1 节：Await 运算符和 async 关键字

await 运算符和 async 关键字一起使用：

> 使用 await 的异步方法必须由 async 关键字修饰。

反之则不总是成立：你可以在方法体中不使用 await 的情况下将其标记为 async。

await 实际做的是暂停代码的执行，直到被等待的任务完成；任何任务都可以被等待。

注意：你不能等待返回 nothing（void）的 async 方法。

实际上，“暂停”这个词有点误导，因为不仅执行停止，而且线程可能被释放以执行其他操作。在内部，await 是通过编译器的一些魔法实现的：它将方法拆分为两部分——await 之前和之后。后一部分在被等待的任务完成后执行。

如果忽略一些重要细节，编译器大致会为你执行以下操作：

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

任何普通方法都可以通过以下方式转换为 async：

```
await Task.Run(() => YourSyncMethod());
```

当你需要在 UI 线程上执行长时间运行的方法而不冻结

UI 时，这可能很有优势。

但这里有一个非常重要[content]
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

### 第 113.4 节：BackgroundWorker

以下是一个简单的示例，说明如何使用 BackgroundWorker 对象在后台线程中执行耗时操作。

你需要：

- 1. 定义一个执行耗时工作的 worker 方法，并从 BackgroundWorker 的 DoWork 事件的处理程序中调用它。
- 2. 使用 RunWorkerAsync 启动执行。DoWork 附加的工作方法所需的任何参数都可以通过 RunWorkerAsync 的 DoWorkEventArgs 参数传入。

除了 DoWork 事件之外，BackgroundWorker 类还定义了两个用于与用户界面交互的事件。这些是可选的。

- RunWorkerCompleted 事件在 DoWork 处理程序完成时触发。
- ProgressChanged 事件在调用 ReportProgress 方法时触发。

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

### 第 113.5 节：Task

以下是一个简单的示例，说明如何使用 Task 在后台进程中执行一些耗时操作。

你需要做的就是将耗时方法包装在 Task.Run() 调用中。

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

### 第 113.6 节：Thread

以下是一个简单的示例，说明如何使用 Thread 在后台进程中执行一些耗时操作。

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

如你所见，我们无法从 TimeIntensiveMethod 返回值，因为 Thread 要求其参数为 void 方法。

要从 Thread 获取返回值，请使用事件或以下方法：

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

## 第 114 章：Async-Await

在 C# 中，声明为 async 的方法在同步进程中不会阻塞，前提是使用基于 I/O 的操作（例如网络访问、工作文件等）。此类标记为 async 的方法的结果可以通过 await 关键字进行等待。

### 第 114.1 节：Await 运算符和 async 关键字

await 运算符和 async 关键字一起使用：

> 使用 await 的异步方法必须由 async 关键字修饰。

反之则不总是成立：你可以在方法体中不使用 await 的情况下将其标记为 async。

await 实际做的是暂停代码的执行，直到被等待的任务完成；任何任务都可以被等待。

注意：你不能等待返回 nothing（void）的 async 方法。

实际上，“暂停”这个词有点误导，因为不仅执行停止，而且线程可能被释放以执行其他操作。在内部，await 是通过编译器的一些魔法实现的：它将方法拆分为两部分——await 之前和之后。后一部分在被等待的任务完成后执行。

如果忽略一些重要细节，编译器大致会为你执行以下操作：

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

任何普通方法都可以通过以下方式转换为 async：

```
await Task.Run(() => YourSyncMethod());
```

当你需要在 UI 线程上执行长时间运行的方法而不冻结

UI 时，这可能很有优势。

但这里有一个非常重要[content]
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

### 第 113.4 节：BackgroundWorker

以下是一个简单的示例，说明如何使用 BackgroundWorker 对象在后台线程中执行耗时操作。

你需要：

- 1. 定义一个执行耗时工作的 worker 方法，并从 BackgroundWorker 的 DoWork 事件的处理程序中调用它。
- 2. 使用 RunWorkerAsync 启动执行。DoWork 附加的工作方法所需的任何参数都可以通过 RunWorkerAsync 的 DoWorkEventArgs 参数传入。

除了 DoWork 事件之外，BackgroundWorker 类还定义了两个用于与用户界面交互的事件。这些是可选的。

- RunWorkerCompleted 事件在 DoWork 处理程序完成时触发。
- ProgressChanged 事件在调用 ReportProgress 方法时触发。

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

### 第 113.5 节：Task

以下是一个简单的示例，说明如何使用 Task 在后台进程中执行一些耗时操作。

你需要做的就是将耗时方法包装在 Task.Run() 调用中。

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

### 第 113.6 节：Thread

以下是一个简单的示例，说明如何使用 Thread 在后台进程中执行一些耗时操作。

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

如你所见，我们无法从 TimeIntensiveMethod 返回值，因为 Thread 要求其参数为 void 方法。

要从 Thread 获取返回值，请使用事件或以下方法：

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

## 第 114 章：Async-Await

在 C# 中，声明为 async 的方法在同步进程中不会阻塞，前提是使用基于 I/O 的操作（例如网络访问、工作文件等）。此类标记为 async 的方法的结果可以通过 await 关键字进行等待。

### 第 114.1 节：Await 运算符和 async 关键字

await 运算符和 async 关键字一起使用：

> 使用 await 的异步方法必须由 async 关键字修饰。

反之则不总是成立：你可以在方法体中不使用 await 的情况下将其标记为 async。

await 实际做的是暂停代码的执行，直到被等待的任务完成；任何任务都可以被等待。

注意：你不能等待返回 nothing（void）的 async 方法。

实际上，“暂停”这个词有点误导，因为不仅执行停止，而且线程可能被释放以执行其他操作。在内部，await 是通过编译器的一些魔法实现的：它将方法拆分为两部分——await 之前和之后。后一部分在被等待的任务完成后执行。

如果忽略一些重要细节，编译器大致会为你执行以下操作：

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

任何普通方法都可以通过以下方式转换为 async：

```
await Task.Run(() => YourSyncMethod());
```

当你需要在 UI 线程上执行长时间运行的方法而不冻结

UI 时，这可能很有优势。

但这里有一个非常重要[content]
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

### 第 113.4 节：BackgroundWorker

以下是一个简单的示例，说明如何使用 BackgroundWorker 对象在后台线程中执行耗时操作。

你需要：

- 1. 定义一个执行耗时工作的 worker 方法，并从 BackgroundWorker 的 DoWork 事件的处理程序中调用它。
- 2. 使用 RunWorkerAsync 启动执行。DoWork 附加的工作方法所需的任何参数都可以通过 RunWorkerAsync 的 DoWorkEventArgs 参数传入。

除了 DoWork 事件之外，BackgroundWorker 类还定义了两个用于与用户界面交互的事件。这些是可选的。

- RunWorkerCompleted 事件在 DoWork 处理程序完成时触发。
- ProgressChanged 事件在调用 ReportProgress 方法时触发。

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

### 第 113.5 节：Task

以下是一个简单的示例，说明如何使用 Task 在后台进程中执行一些耗时操作。

你需要做的就是将耗时方法包装在 Task.Run() 调用中。

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

### 第 113.6 节：Thread

以下是一个简单的示例，说明如何使用 Thread 在后台进程中执行一些耗时操作。

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

如你所见，我们无法从 TimeIntensiveMethod 返回值，因为 Thread 要求其参数为 void 方法。

要从 Thread 获取返回值，请使用事件或以下方法：

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

## 第 114 章：Async-Await

在 C# 中，声明为 async 的方法在同步进程中不会阻塞，前提是使用基于 I/O 的操作（例如网络访问、工作文件等）。此类标记为 async 的方法的结果可以通过 await 关键字进行等待。

### 第 114.1 节：Await 运算符和 async 关键字

await 运算符和 async 关键字一起使用：

> 使用 await 的异步方法必须由 async 关键字修饰。

反之则不总是成立：你可以在方法体中不使用 await 的情况下将其标记为 async。

await 实际做的是暂停代码的执行，直到被等待的任务完成；任何任务都可以被等待。

注意：你不能等待返回 nothing（void）的 async 方法。

实际上，“暂停”这个词有点误导，因为不仅执行停止，而且线程可能被释放以执行其他操作。在内部，await 是通过编译器的一些魔法实现的：它将方法拆分为两部分——await 之前和之后。后一部分在被等待的任务完成后执行。

如果忽略一些重要细节，编译器大致会为你执行以下操作：

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

任何普通方法都可以通过以下方式转换为 async：

```
await Task.Run(() => YourSyncMethod());
```

当你需要在 UI 线程上执行长时间运行的方法而不冻结

UI 时，这可能很有优势。

但这里有一个非常重要[content]
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

### 第 113.4 节：BackgroundWorker

以下是一个简单的示例，说明如何使用 BackgroundWorker 对象在后台线程中执行耗时操作。

你需要：

- 1. 定义一个执行耗时工作的 worker 方法，并从 BackgroundWorker 的 DoWork 事件的处理程序中调用它。
- 2. 使用 RunWorkerAsync 启动执行。DoWork 附加的工作方法所需的任何参数都可以通过 RunWorkerAsync 的 DoWorkEventArgs 参数传入。

除了 DoWork 事件之外，BackgroundWorker 类还定义了两个用于与用户界面交互的事件。这些是可选的。

- RunWorkerCompleted 事件在 DoWork 处理程序完成时触发。
- ProgressChanged 事件在调用 ReportProgress 方法时触发。

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

### 第 113.5 节：Task

以下是一个简单的示例，说明如何使用 Task 在后台进程中执行一些耗时操作。

你需要做的就是将耗时方法包装在 Task.Run() 调用中。

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

### 第 113.6 节：Thread

以下是一个简单的示例，说明如何使用 Thread 在后台进程中执行一些耗时操作。

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

如你所见，我们无法从 TimeIntensiveMethod 返回值，因为 Thread 要求其参数为 void 方法。

要从 Thread 获取返回值，请使用事件或以下方法：

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

## 第 114 章：Async-Await

在 C# 中，声明为 async 的方法在同步进程中不会阻塞，前提是使用基于 I/O 的操作（例如网络访问、工作文件等）。此类标记为 async 的方法的结果可以通过 await 关键字进行等待。

### 第 114.1 节：Await 运算符和 async 关键字

await 运算符和 async 关键字一起使用：

> 使用 await 的异步方法必须由 async 关键字修饰。

反之则不总是成立：你可以在方法体中不使用 await 的情况下将其标记为 async。

await 实际做的是暂停代码的执行，直到被等待的任务完成；任何任务都可以被等待。

注意：你不能等待返回 nothing（void）的 async 方法。

实际上，“暂停”这个词有点误导，因为不仅执行停止，而且线程可能被释放以执行其他操作。在内部，await 是通过编译器的一些魔法实现的：它将方法拆分为两部分——await 之前和之后。后一部分在被等待的任务完成后执行。

如果忽略一些重要细节，编译器大致会为你执行以下操作：

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

任何普通方法都可以通过以下方式转换为 async：

```
await Task.Run(() => YourSyncMethod());
```

当你需要在 UI 线程上执行长时间运行的方法而不冻结

UI 时，这可能很有优势。

但这里有一个非常重要[content]
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

### 第 113.4 节：BackgroundWorker

以下是一个简单的示例，说明如何使用 BackgroundWorker 对象在后台线程中执行耗时操作。

你需要：

- 1. 定义一个执行耗时工作的 worker 方法，并从 BackgroundWorker 的 DoWork 事件的处理程序中调用它。
- 2. 使用 RunWorkerAsync 启动执行。DoWork 附加的工作方法所需的任何参数都可以通过 RunWorkerAsync 的 DoWorkEventArgs 参数传入。

除了 DoWork 事件之外，BackgroundWorker 类还定义了两个用于与用户界面交互的事件。这些是可选的。

- RunWorkerCompleted 事件在 DoWork 处理程序完成时触发。
- ProgressChanged 事件在调用 ReportProgress 方法时触发。

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

### 第 113.5 节：Task

以下是一个简单的示例，说明如何使用 Task 在后台进程中执行一些耗时操作。

你需要做的就是将耗时方法包装在 Task.Run() 调用中。

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

### 第 113.6 节：Thread

以下是一个简单的示例，说明如何使用 Thread 在后台进程中执行一些耗时操作。

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

如你所见，我们无法从 TimeIntensiveMethod 返回值，因为 Thread 要求其参数为 void 方法。

要从 Thread 获取返回值，请使用事件或以下方法：

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

## 第 114 章：Async-Await

在 C# 中，声明为 async 的方法在同步进程中不会阻塞，前提是使用基于 I/O 的操作（例如网络访问、工作文件等）。此类标记为 async 的方法的结果可以通过 await 关键字进行等待。

### 第 114.1 节：Await 运算符和 async 关键字

await 运算符和 async 关键字一起使用：

> 使用 await 的异步方法必须由 async 关键字修饰。

反之则不总是成立：你可以在方法体中不使用 await 的情况下将其标记为 async。

await 实际做的是暂停代码的执行，直到被等待的任务完成；任何任务都可以被等待。

注意：你不能等待返回 nothing（void）的 async 方法。

实际上，“暂停”这个词有点误导，因为不仅执行停止，而且线程可能被释放以执行其他操作。在内部，await 是通过编译器的一些魔法实现的：它将方法拆分为两部分——await 之前和之后。后一部分在被等待的任务完成后执行。

如果忽略一些重要细节，编译器大致会为你执行以下操作：

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

任何普通方法都可以通过以下方式转换为 async：

```
await Task.Run(() => YourSyncMethod());
```

当你需要在 UI 线程上执行长时间运行的方法而不冻结

UI 时，这可能很有优势。

但这里有一个非常重要[content]
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

### 第 113.4 节：BackgroundWorker

以下是一个简单的示例，说明如何使用 BackgroundWorker 对象在后台线程中执行耗时操作。

你需要：

- 1. 定义一个执行耗时工作的 worker 方法，并从 BackgroundWorker 的 DoWork 事件的处理程序中调用它。
- 2. 使用 RunWorkerAsync 启动执行。DoWork 附加的工作方法所需的任何参数都可以通过 RunWorkerAsync 的 DoWorkEventArgs 参数传入。

除了 DoWork 事件之外，BackgroundWorker 类还定义了两个用于与用户界面交互的事件。这些是可选的。

- RunWorkerCompleted 事件在 DoWork 处理程序完成时触发。
- ProgressChanged 事件在调用 ReportProgress 方法时触发。

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

### 第 113.5 节：Task

以下是一个简单的示例，说明如何使用 Task 在后台进程中执行一些耗时操作。

你需要做的就是将耗时方法包装在 Task.Run() 调用中。

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

### 第 113.6 节：Thread

以下是一个简单的示例，说明如何使用 Thread 在后台进程中执行一些耗时操作。

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

如你所见，我们无法从 TimeIntensiveMethod 返回值，因为 Thread 要求其参数为 void 方法。

要从 Thread 获取返回值，请使用事件或以下方法：

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

## 第 114 章：Async-Await

在 C# 中，声明为 async 的方法在同步进程中不会阻塞，前提是使用基于 I/O 的操作（例如网络访问、工作文件等）。此类标记为 async 的方法的结果可以通过 await 关键字进行等待。

### 第 114.1 节：Await 运算符和 async 关键字

await 运算符和 async 关键字一起使用：

> 使用 await 的异步方法必须由 async 关键字修饰。

反之则不总是成立：你可以在方法体中不使用 await 的情况下将其标记为 async。

await 实际做的是暂停代码的执行，直到被等待的任务完成；任何任务都可以被等待。

注意：你不能等待返回 nothing（void）的 async 方法。

实际上，“暂停”这个词有点误导，因为不仅执行停止，而且线程可能被释放以执行其他操作。在内部，await 是通过编译器的一些魔法实现的：它将方法拆分为两部分——await 之前和之后。后一部分在被等待的任务完成后执行。

如果忽略一些重要细节，编译器大致会为你执行以下操作：

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

任何普通方法都可以通过以下方式转换为 async：

```
await Task.Run(() => YourSyncMethod());
```

当你需要在 UI 线程上执行长时间运行的方法而不冻结

UI 时，这可能很有优势。

但这里有一个非常重要[content]
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

### 第 113.4 节：BackgroundWorker

以下是一个简单的示例，说明如何使用 BackgroundWorker 对象在后台线程中执行耗时操作。

你需要：

- 1. 定义一个执行耗时工作的 worker 方法，并从 BackgroundWorker 的 DoWork 事件的处理程序中调用它。
- 2. 使用 RunWorkerAsync 启动执行。DoWork 附加的工作方法所需的任何参数都可以通过 RunWorkerAsync 的 DoWorkEventArgs 参数传入。

除了 DoWork 事件之外，BackgroundWorker 类还定义了两个用于与用户界面交互的事件。这些是可选的。

- RunWorkerCompleted 事件在 DoWork 处理程序完成时触发。
- ProgressChanged 事件在调用 ReportProgress 方法时触发。

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

### 第 113.5 节：Task

以下是一个简单的示例，说明如何使用 Task 在后台进程中执行一些耗时操作。

你需要做的就是将耗时方法包装在 Task.Run() 调用中。

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

### 第 113.6 节：Thread

以下是一个简单的示例，说明如何使用 Thread 在后台进程中执行一些耗时操作。

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

如你所见，我们无法从 TimeIntensiveMethod 返回值，因为 Thread 要求其参数为 void 方法。

要从 Thread 获取返回值，请使用事件或以下方法：

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

## 第 114 章：Async-Await

在 C# 中，声明为 async 的方法在同步进程中不会阻塞，前提是使用基于 I/O 的操作（例如网络访问、工作文件等）。此类标记为 async 的方法的结果可以通过 await 关键字进行等待。

### 第 114.1 节：Await 运算符和 async 关键字

await 运算符和 async 关键字一起使用：

> 使用 await 的异步方法必须由 async 关键字修饰。

反之则不总是成立：你可以在方法体中不使用 await 的情况下将其标记为 async。

await 实际做的是暂停代码的执行，直到被等待的任务完成；任何任务都可以被等待。

注意：你不能等待返回 nothing（void）的 async 方法。

实际上，“暂停”这个词有点误导，因为不仅执行停止，而且线程可能被释放以执行其他操作。在内部，await 是通过编译器的一些魔法实现的：它将方法拆分为两部分——await 之前和之后。后一部分在被等待的任务完成后执行。

如果忽略一些重要细节，编译器大致会为你执行以下操作：

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

任何普通方法都可以通过以下方式转换为 async：

```
await Task.Run(() => YourSyncMethod());
```

当你需要在 UI 线程上执行长时间运行的方法而不冻结

UI 时，这可能很有优势。

但这里有一个非常重要[content]
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
### 第 113.4 节：BackgroundWorker
以下是一个简单的示例，说明如何使用 BackgroundWorker 对象在后台线程中执行耗时操作。
你需要：
- 1. 定义一个执行耗时工作的 worker 方法，并从 BackgroundWorker 的 DoWork 事件的处理程序中调用它。
- 2. 使用 RunWorkerAsync 启动执行。DoWork 附加的工作方法所需的任何参数都可以通过 RunWorkerAsync 的 DoWorkEventArgs 参数传入。
除了 DoWork 事件之外，BackgroundWorker 类还定义了两个用于与用户界面交互的事件。这些是可选的。
- RunWorkerCompleted 事件在 DoWork 处理程序完成时触发。
- ProgressChanged 事件在调用 ReportProgress 方法时触发。
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
### 第 113.5 节：Task
以下是一个简单的示例，说明如何使用 Task 在后台进程中执行一些耗时操作。
你需要做的就是将耗时方法包装在 Task.Run() 调用中。
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
### 第 113.6 节：Thread
以下是一个简单的示例，说明如何使用 Thread 在后台进程中执行一些耗时操作。
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
如你所见，我们无法从 TimeIntensiveMethod 返回值，因为 Thread 要求其参数为 void 方法。
要从 Thread 获取返回值，请使用事件或以下方法：
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
## 第 114 章：Async-Await
在 C# 中，声明为 async 的方法在同步进程中不会阻塞，前提是使用基于 I/O 的操作（例如网络访问、工作文件等）。此类标记为 async 的方法的结果可以通过 await 关键字进行等待。
### 第 114.1 节：Await 运算符和 async 关键字
await 运算符和 async 关键字一起使用：
> 使用 await 的异步方法必须由 async 关键字修饰。
反之则不总是成立：你可以在方法体中不使用 await 的情况下将其标记为 async。
await 实际做的是暂停代码的执行，直到被等待的任务完成；任何任务都可以被等待。
注意：你不能等待返回 nothing（void）的 async 方法。
实际上，“暂停”这个词有点误导，因为不仅执行停止，而且线程可能被释放以执行其他操作。在内部，await 是通过编译器的一些魔法实现的：它将方法拆分为两部分——await 之前和之后。后一部分在被等待的任务完成后执行。
如果忽略一些重要细节，编译器大致会为你执行以下操作：
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
任何普通方法都可以通过以下方式转换为 async：
```
await Task.Run(() => YourSyncMethod());
```
当你需要在 UI 线程上执行长时间运行的方法而不冻结
UI 时，这可能很有优势。
但这里有一个非常重要[content]
### 第 113.4 节：BackgroundWorker
以下是一个简单的示例，说明如何使用 BackgroundWorker 对象在后台线程中执行耗时操作。
你需要：
- 1. 定义一个执行耗时工作的 worker 方法，并从 BackgroundWorker 的 DoWork 事件的处理程序中调用它。
- 2. 使用 RunWorkerAsync 启动执行。DoWork 附加的工作方法所需的任何参数都可以通过 RunWorkerAsync 的 DoWorkEventArgs 参数传入。
除了 DoWork 事件之外，BackgroundWorker 类还定义了两个用于与用户界面交互的事件。这些是可选的。
- RunWorkerCompleted 事件在 DoWork 处理程序完成时触发。
- ProgressChanged 事件在调用 ReportProgress 方法时触发。
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
### 第 113.5 节：Task
以下是一个简单的示例，说明如何使用 Task 在后台进程中执行一些耗时操作。
你需要做的就是将耗时方法包装在 Task.Run() 调用中。
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
### 第 113.6 节：Thread
以下是一个简单的示例，说明如何使用 Thread 在后台进程中执行一些耗时操作。
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
如你所见，我们无法从 TimeIntensiveMethod 返回值，因为 Thread 要求其参数为 void 方法。
要从 Thread 获取返回值，请使用事件或以下方法：
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
## 第 114 章：Async-Await
在 C# 中，声明为 async 的方法在同步进程中不会阻塞，前提是使用基于 I/O 的操作（例如网络访问、工作文件等）。此类标记为 async 的方法的结果可以通过 await 关键字进行等待。
### 第 114.1 节：Await 运算符和 async 关键字
await 运算符和 async 关键字一起使用：
> 使用 await 的异步方法必须由 async 关键字修饰。
反之则不总是成立：你可以在方法体中不使用 await 的情况下将其标记为 async。
await 实际做的是暂停代码的执行，直到被等待的任务完成；任何任务都可以被等待。
注意：你不能等待返回 nothing（void）的 async 方法。
实际上，“暂停”这个词有点误导，因为不仅执行停止，而且线程可能被释放以执行其他操作。在内部，await 是通过编译器的一些魔法实现的：它将方法拆分为两部分——await 之前和之后。后一部分在被等待的任务完成后执行。
如果忽略一些重要细节，编译器大致会为你执行以下操作：
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
任何普通方法都可以通过以下方式转换为 async：
```
await Task.Run(() => YourSyncMethod());
```
当你需要在 UI 线程上执行长时间运行的方法而不冻结
UI 时，这可能很有优势。
但这里有一个非常重要[content]
### 第 113.4 节：BackgroundWorker
以下是一个简单的示例，说明如何使用 BackgroundWorker 对象在后台线程中执行耗时操作。
你需要：
- 1. 定义一个执行耗时工作的 worker 方法，并从 BackgroundWorker 的 DoWork 事件的处理程序中调用它。
- 2. 使用 RunWorkerAsync 启动执行。DoWork 附加的工作方法所需的任何参数都可以通过 RunWorkerAsync 的 DoWorkEventArgs 参数传入。
除了 DoWork 事件之外，BackgroundWorker 类还定义了两个用于与用户界面交互的事件。这些是可选的。
- RunWorkerCompleted 事件在 DoWork 处理程序完成时触发。
- ProgressChanged 事件在调用 ReportProgress 方法时触发。
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
### 第 113.5 节：Task
以下是一个简单的示例，说明如何使用 Task 在后台进程中执行一些耗时操作。
你需要做的就是将耗时方法包装在 Task.Run() 调用中。
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
### 第 113.6 节：Thread
以下是一个简单的示例，说明如何使用 Thread 在后台进程中执行一些耗时操作。
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
如你所见，我们无法从 TimeIntensiveMethod 返回值，因为 Thread 要求其参数为 void 方法。
要从 Thread 获取返回值，请使用事件或以下方法：
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
## 第 114 章：Async-Await
在 C# 中，声明为 async 的方法在同步进程中不会阻塞，前提是使用基于 I/O 的操作（例如网络访问、工作文件等）。此类标记为 async 的方法的结果可以通过 await 关键字进行等待。
### 第 114.1 节：Await 运算符和 async 关键字
await 运算符和 async 关键字一起使用：
> 使用 await 的异步方法必须由 async 关键字修饰。
反之则不总是成立：你可以在方法体中不使用 await 的情况下将其标记为 async。
await 实际做的是暂停代码的执行，直到被等待的任务完成；任何任务都可以被等待。
注意：你不能等待返回 nothing（void）的 async 方法。
实际上，“暂停”这个词有点误导，因为不仅执行停止，而且线程可能被释放以执行其他操作。在内部，await 是通过编译器的一些魔法实现的：它将方法拆分为两部分——await 之前和之后。后一部分在被等待的任务完成后执行。
如果忽略一些重要细节，编译器大致会为你执行以下操作：
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
任何普通方法都可以通过以下方式转换为 async：
```
await Task.Run(() => YourSyncMethod());
```
当你需要在 UI 线程上执行长时间运行的方法而不冻结
UI 时，这可能很有优势。
但这里有一个很重要的说明：**异步并不总是意味着并发（并行甚至多线程）**。即使在单线程上，async-await 仍然允许异步代码。例如，参见这个自定义任务调度程序。这种“疯狂”的任务调度程序可以简单地将任务转换为在消息循环处理中调用的函数。
我们需要问自己：我们的 DoIt_Continuation 方法的延续将在哪个线程上执行？
默认情况下，await 运算符会使用当前的 SynchronizationContext 调度延续的执行。这意味着默认情况下，对于 WinForms 和 WPF，延续在 UI 线程上运行。如果出于某种原因需要更改此行为，请使用 Task.ConfigureAwait() 方法：
```
await Task.Run(() => YourSyncMethod()).ConfigureAwait(continueOnCapturedContext: false);
```
### 第 114.2 节：并发调用
可以通过先调用可等待的任务然后再等待它们来并发等待多个调用。
```
public async Task RunConcurrentTasks()
{
    var firstTask = DoSomethingAsync();
    var secondTask = DoSomethingElseAsync();
    await firstTask;
    await secondTask;
}
```
另外，可以使用 Task.WhenAll 将多个任务组合成一个 Task，当其传递的所有任务都完成时完成。
```
public async Task RunConcurrentTasks()
{
    var firstTask = DoSomethingAsync();
    var secondTask = DoSomethingElseAsync();
    await Task.WhenAll(firstTask, secondTask);
}
```
你也可以在循环中这样做，例如：
```
List<Task> tasks = new List<Task>();
while (something) {
    // do stuff
    Task someAsyncTask = someAsyncMethod();
    tasks.Add(someAsyncTask);
}
await Task.WhenAll(tasks);
```
要在使用 Task.WhenAll 等待多个任务后获取任务的结果，只需再次等待该任务即可。由于任务已经完成，它只会返回结果
```
var task1 = SomeOpAsync();
var task2 = SomeOtherOpAsync();
```
