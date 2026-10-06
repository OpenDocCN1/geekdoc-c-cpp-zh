

# 示例 171 在独立任务中执行耗时计算

长时间运行的计算或对 Web 服务器、数据库或其他远程服务的访问可以作为独立任务执行，以避免阻塞用户界面，或允许其他活动当前进行。这里 `SlowFibTask` 创建并启动了一个异步执行耗时计算的任务。任务的结果可以通过 `task.Result` 获取。

```
public static double SlowFib(int n) { ... n=43 时，计算耗时 10 秒 ... }
public static Task<double> SlowFibTask(int n) {
    return Task.Run(() => SlowFib(n));
}

Task<double> task = SlowFibTask(); // 返回一个正在运行的任务
Console.Write("[task is running ]");
Console.WriteLine(task.Result);
```

# 示例 172 使用 Task 延续实现异步 Web 数据检索

假设想为 170 中的 `NbiEntrez` 和 `NbiProtein` 方法创建异步版本，返回 `Task<String>` 而不是 `String`。使用异步版本 `DownloadDataAsync` 代替 `DownloadData` 方法，它返回 `Task<byte[]>`。当该任务完成时，使用类 `<T>` 中的中的 `ContinueWith`（第 22.2 节）为下载任务附加一个延续（作为 Lambda 表达式），将字节数组转换为 `String`。示例 176 展示了明显更好但功能等价的方法。

```
public static Task<String> NbiEntrezTask(String query) {
    return new WebClient().DownloadAsync(new Uri(server + query))
    .ContinueWith((Task<byte[]> task) =>
        ASCII.Encoding.GetString(task.Result));
}
```

```
public static Task<String> NbiProteinTask(String id) {
    return NbiEntrezTask("effetch.cgi?retry=fasta&retmode=text&db=" + id);
}
```

ShowResult(NbiProteinTask("P01308").Result);

# 示例 173 实现超时

可以使用 `WhenAny` 实现任务超时，以判断指定的 `SlowFibTask`（示例 171）或特定的 `Delay` 是否完成。`WhenAny` 创建并启动任务，当其完成时，它将绑定到延续的参数 `task`。获取完成的任务的结果，因此可以测试它是否是 `SlowFibTask`，如果是则返回其结果，否则返回某些虚拟值。示例 179 显示了如何更自然地表达这种方式。

```
public static Task<double> SlowFibTimeout(int n) {
    Task<double> slowFib = SlowFib(n);
    return Task.WhenAny(slowFib, Task.Delay(1000))
    .ContinueWith<double>((Task<double> task) =>
        task.Result == slowFib ? slowFib.Result : -1);
}
```

# 2.2.2 类 Task<T>

来自 `System.Threading.Tasks` 命名空间的 `Task<T>` 类表示产生 T 类型结果的计算；它是 `Task` 的子类，并具有以下附加成员：

- *构造函数 Task<T>(Func<T> func)* 创建一个任务，该任务在启动时将执行 `func()`。
- *Task ContinueWith(Action<Task<T>> cont)* 创建并启动一个任务，其中给的任务将通过计算 `cont` 继续；当任务完成时，将调用 `cont(task)`。
- *Task<U> ContinueWith<U>(Func<Task<T>, U> cont)* 类似，其中延续产生类型为 U 的结果。重载版本可接受取消令牌、任务延续选项和任务调度器作为参数。
- *只读属性 Result* 阻塞直到任务完成并返回其结果。如果任务抛出异常或被取消，则会抛出 `AggregateException`。

# 2.2.3 任务取消

创建任务时，可以向其传递一个 `CallbackContext`。该令牌（token）随后可用于告诉任务它可能会中止。任务可以通过抛出带有 `token` 参数的 `OperationCanceledException` 来确认取消请求（并将任务移动到取消状态，第141页）。单个取消令牌可以传递给多个任务，以便这些任务可以通过调用 `Cancel()` 被取消。来自 `System.Threading` 命名空间的 `CallbackContext` 类型为已创建令牌的任务提供了以下操作：

- *只读属性 IsCancellationRequested* 如果在取消令牌源上请求了取消，则返回 `true`。
- *void ThrowIfCancellationRequested()* 如果 `IsCancellationRequested` 为 `true`，则抛出带有 `ct` 参数的 `OperationCanceledException`；否则什么都不做。

来自 `System.Threading` 命名空间的 `CancellationTokenSource` 类用于创建取消令牌：

- *构造函数 CancellationTokenSource()* 创建一个新的令牌源。
- *void Cancel()* 通过关联的取消令牌请求取消。
- *static CancellationTokenSource CreateLinkedSource(params cts)* 只要给出了任何取消令牌源，就会创建一个请求取消的令牌源。
- *只读属性 bool IsCancellationRequested* 如果请求了取消，则返回 `true`。
- *只读属性 CancellationToken* 返回取消令牌。

许多与其他取消相关的类型在 .Net 类库中描述。

# 任务库 (C# 4.0) 141

### 示例 174 任务取消
为了允许任务取消，必须创建一个令牌源 `cts` 并 `cts.Token` 传递给创建任务的方法。此外，任务本身必须抛出带有 `token` 参数的 `OperationCanceledException` 来确认取消；如果删取消请求，任务将继续运行并最终到达 `RanToCompletion`。

```
public static void ComputeTaskWithAcknowledgement(CancellationToken token) {
    for (int i=0; i<100000; i++) token.ThrowIfCancellationRequested();
}

CancellationTokenSource cts = new CancellationTokenSource();
CancellationToken token = cts.Token;
Task task = Task.Run(() => ComputeTaskWithAcknowledgement(token)); // 运行
cts.Cancel(); // 已取消
task.Wait(); // 将抛出 AggregateException
```

### 示例 175 任务中的异常
如果运行的任务抛出异常（确认取消的 `OperationCanceledException` 外），将在 `Faulted` 状态完成。在任务上调用 `Wait()` 或 `Result` 将抛出一个包含任务抛出的异常的 `AggregateException`。

```
Task task = new Task(() { throw new Exception("died"); }); // 创建
task.Start(); // Waiting 或 Faulted
task.Wait(); // 将抛出包含 Exception("died")
```

任务状态与转换。来自 `System.Threading.Tasks` 命名空间的 `TaskStatus` 枚举描述任务状态。任务在最后三个状态之一完成，在最后一个状态下发生故障。

| 任务状态 | 含义 |
|---|---|
| Created | 由 Task 构造函数创建，但未启动 |
| WaitingForActivation | 等待激活并内部调度 |
| WaitingToRun | 已调度但尚未运行 |
| Running | 正在运行但尚未完成 |
| RanToCompletion | 成功完成 |
| Canceled | 在运行前取消或确认了取消 |
| Faulted | 因未处理的异常而完成 |

![](img/089571d2f186cd73b49fccec3a97f1f_153_0.png)

# 异步方法：async 和 await (C# 5.0)

# 异步方法：async 和 await (C# 5.0)

异步方法基于 `Task` 和 `Task<T>` 类，简化远程服务器、用户交互和密集计算等操作的定义和组合。

`async` 方法修饰符用于声明（第10.7 节）异步方法：

```
async method-modifiers rentype Task
```

异步方法必须返回 `Task` 或 `Task<T>`（第 22.2 节）或 `out` 参数。按照习惯，异步方法的名称应以 `Async` 结尾。

同样，`async` 关键字之前的委托或 Lambda 表达式是异步的。

对异步方法的调用从调用者的线程开始同步执行，直到在 `e` 不是已完成的任务时评估 `await` 表达式（见下文）。在此处，异步方法返回给调用者，而由 `e` 产生的任务正在异步执行。

返回 `Task<T>` 的异步方法只能返回 `e`，其中表达式类型为 `T`。`e` 的返回值可以使用异步方法产生的任务的 `Result` 属性检索。返回 `Task` 或 `void` 的异步方法可能包含 `return` 语句，但这些语句不能有表达式参数。

异步方法的形式如下：

```
await e
```

其中 `e` 是 `Task` 或 `Task<T>` 表达式且必须非空。当 `e` 类型为 `Task<T>` 时，`await` 表达式类型为 `T`；当 `e` 类型为 `Task` 时，`await` 表达式类型为 `void`。`await` 表达式的效果是创建并启动一个任务，该任务 (1) 将 `e` 求值为已启动的任务，(2) 等待该任务完成，(3) 继续执行异步方法的剩余部分。

C# 编译器将 `await` 替换为表达式 `e.ContinueWith(result)`，其中 `result` 是代表异步方法剩余部分的委托。例如，示例 7 等同于第 172 页的内容。这种解释过于简单，因为 `await` 表达式可能在一个或多个循环中。为了涵盖这些情况，异步方法被实现为状态机。

`await` 表达式只能出现在异步方法、委托或 Lambda 表达式内部，不能出现在 `catch` 或 `finally` 块、`lock` 语句或嵌套的同步委托或 Lambda 表达式中。

异步方法抛出的异常不会传播给调用者，而对异步方法返回的任务调用 `Wait` 或 `Result` 时，会被封装在 `AggregateException` 中。`void` 异步方法抛出的异常可能无法被报告。

有关异步方法的更多信息，请参阅第 34 节的资源，

