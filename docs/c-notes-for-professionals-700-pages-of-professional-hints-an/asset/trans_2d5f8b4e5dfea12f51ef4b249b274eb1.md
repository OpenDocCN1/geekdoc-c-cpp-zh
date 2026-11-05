
await Task.WhenAll(task1, task2);

var result = await task2;

此外，Task.WhenAny 也可以用于并行执行多个任务，如上面的 Task.WhenAll，区别在于此方法会在提供的任务中任意一个完成时完成。

```
public async Task RunConcurrentTasksWhenAny()
{
    var firstTask = TaskOperation("#firstTask executed");
    var secondTask = TaskOperation("#secondTask executed");
    var thirdTask = TaskOperation("#thirdTask executed");
    await Task.WhenAny(firstTask, secondTask, thirdTask);
}
```

RunConcurrentTasksWhenAny 返回的 Task 会在 firstTask、secondTask 或 thirdTask 中任意一个完成时完成。

## 第 114.3 节：Try/Catch/Finally

版本 ≥ 6.0

自 C# 6.0 起，await 关键字现在可以在 catch 和 finally 块中使用。

```
try {
    var client = new AsyncClient();
    await client.DoSomething();
} catch (MyException ex) {
    await client.LogExceptionAsync();
    throw;
} finally {
    await client.CloseAsync();
}
```

版本 ≥ 5.0 版本 < 6.0

在 C# 6.0 之前，你需要做类似以下的操作。注意 6.0 还使用空传播运算符清理了空检查。

```
AsyncClient client;
MyException caughtException;
try {
    client = new AsyncClient();
    await client.DoSomething();
} catch (MyException ex) {
    caughtException = ex;
}

if (client != null) {
    if (caughtException != null) {
        await client.LogExceptionAsync();
    }
    await client.CloseAsync();
    if (caughtException != null) throw caughtException;
}
```

请注意，如果你等待的任务不是由 async 创建的（例如由 Task.Run 创建的任务），某些调试器可能会在任务抛出的异常上中断，即使该异常似乎已被周围的 try/catch 处理。这是因为调试器认为它相对于用户代码未处理。在 Visual Studio 中，有一个名为“Just My Code”的选项，可以将其禁用以防止调试器在这种情况下中断。

## 第 114.4 节：不使用 await 返回 Task

执行异步操作的方法如果满足以下条件则不需要使用 await：

- 方法内部只有一个异步调用
- 异步调用位于方法末尾
- 不需要捕获/处理 Task 中可能发生的异常

考虑以下返回 Task 的方法：

```
public async Task<User> GetUserAsync(int id)
{
    var lookupKey = "Users" + id;

    return await dataStore.GetByKeyAsync(lookupKey);
}
```

如果 GetByKeyAsync 与 GetUserAsync 具有相同的签名（返回 Task<User>），则方法可以简化为：

```
public Task<User> GetUserAsync(int id)
{
    var lookupKey = "Users" + id;

    return dataStore.GetByKeyAsync(lookupKey);
}
```

在这种情况下，即使方法正在执行异步操作，也不需要标记为 async。GetByKeyAsync 返回的 Task 会直接传递给调用方法，在那里会被 await。

Important: Returning the Task instead of awaiting it, changes the exception behavior of the method, as it won't throw the exception inside the method which starts the task but in the method which awaits it.

```
public Task SaveAsync()
{
    try {
        return dataStore.SaveChangesAsync();
    }
    catch(Exception ex)
    {
        // this will never be called
        logger.LogException(ex);
    }
}

// Some other code calling SaveAsync()

// If exception happens, it will be thrown here, not inside SaveAsync()
await SaveAsync();
```

这将提高性能，因为它可以节省编译器生成额外的 async 状态机的开销。

## 第 114.5 节：Async/await 只有在允许机器执行额外工作时才会提高性能

考虑以下代码：

```
~~~csharp
public async Task MethodA()
{
    await MethodB();
    // Do other work
}

public async Task MethodB()
{
    await MethodC();
    // Do other work
}

public async Task MethodC()
{
    // Or await some other async work
    await Task.Delay(100);
}
~~~
```

这不会比以下代码表现更好

```
~~~csharp
public void MethodA()
{
    MethodB();
    // Do other work
}

public void MethodB()
{
    MethodC();
    // Do other work
}

public void MethodC()
{
    Thread.Sleep(100);
}
~~~
```

async/await 的主要目的是允许机器执行额外的工作——例如，在等待某些 I/O 操作的结果时允许调用线程执行其他工作。在这种情况下，调用线程永远不会比原本能够做的更多，所以与简单地同步调用 MethodA()、MethodB() 和 MethodC() 相比，没有性能提升。

## 第 114.6 节：Web.config 设置以针对 4.5 实现正确的 async 行为

web.config 中的 system.web.httpRuntime 必须以 4.5 为目标，以确保在恢复你的 async 方法之前线程会重新进入请求上下文。

```
~~~xml
<httpRuntime targetFramework="4.5" />
~~~
```

在 4.5 之前的 ASP.NET 上，Async 和 await 具有未定义的行为。Async / await 将在任意线程上恢复，该线程可能没有请求上下文。在负载下，应用程序在 await 之后访问 HttpContext 时会随机失败并出现空引用异常。由于 async，在 WebApi 中使用 HttpContext.Current 是危险的

## 第 114.7 节：简单的连续调用

```
~~~csharp
public async Task<JobResult> GetDataFromWebAsync()
{
var nextJob = await _database.GetNextJobAsync();
var response = await _httpClient.GetAsync(nextJob.Uri);
var pageContents = await response.Content.ReadAsStringAsync();
return await _database.SaveJobResultAsync(pageContents);
}
~~~
```

这里需要注意的主要是，虽然每个被 await 的方法都是异步调用的——并且在该调用期间控制权会交还给系统——但方法内部的流程是线性的，不需要因异步而进行特殊处理。如果调用的任何方法失败，异常将被“按预期”处理，在这种情况下意味着方法执行将被中止，异常会沿调用栈向上抛出。

## 第 114.8 节：在 async 代码上阻塞可能导致死锁

在具有同步上下文的环境中阻塞 async 调用是不良做法，因为它可能导致死锁。最佳做法是“全程”使用 async/await。例如，以下 Windows Forms 代码会导致死锁：

```
private async Task<bool> TryThis()
{
    Trace.TraceInformation("Starting TryThis");
    await Task.Run(() =>
    {
        Trace.TraceInformation("In TryThis task");
        for (int i = 0; i < 100; i++)
        {
            // This runs successfully - the loop runs to completion
            Trace.TraceInformation("For loop " + i);
            System.Threading.Thread.Sleep(10);
        }
    });

    // This never happens due to the deadlock
    Trace.TraceInformation("About to return");
    return true;
}

// Button click event handler
private void button1_Click(object sender, EventArgs e)
{
    // .Result causes this to block on the asynchronous call
    bool result = TryThis().Result;
    // Never actually gets here
    Trace.TraceInformation("Done with result");
}
```

本质上，一旦 async 调用完成，它就会等待同步上下文可用。然而，事件处理程序在等待 TryThis() 方法完成的同时“持有”同步上下文，从而导致循环等待。

为修复此问题，代码应修改为

```
private async void button1_Click(object sender, EventArgs e)
{
    bool result = await TryThis();
    Trace.TraceInformation("Done with result");
}
```

Note: event handlers are the only place where async void should be used (because you can't await an async void method).

## 第 115 章：Async-Await 中的同步上下文

### 第 115.1 节：async/await 关键字的伪代码

考虑一个简单的异步方法：

```
async Task Foo()
{
    Bar();
    await Baz();
    Qux();
}
```

简化来说，我们可以说这段代码实际上意味着以下内容：

```
Task Foo()
{
    Bar();
    Task t = Baz();
    var context = SynchronizationContext.Current;
    t.ContinueWith(task => {
        if (context == null)
            Qux();
        else
            context.Post((obj) => Qux(), null);
    }, TaskScheduler.Current);
    return t;
}
```

这意味着 async/await 关键字如果存在则使用当前同步上下文。也就是说，你可以编写在 UI、Web 和控制台应用程序中都能正确工作的库代码。

Source article.

### 第 115.2 节：禁用同步上下文

要禁用同步上下文，你应该调用 ConfigureAwait 方法：

```
async Task Foo()
{
    await Task.Run(() => Console.WriteLine("Test"));
}
```

```
Foo().ConfigureAwait(false);
```

> ConfigureAwait 提供了一种避免默认 SynchronizationContext 捕获行为的方法；将 flowContext 参数传递为 false 可防止在 await 之后使用 SynchronizationContext 恢复执行。
