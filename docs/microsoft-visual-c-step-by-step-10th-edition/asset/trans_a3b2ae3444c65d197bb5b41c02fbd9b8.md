
# 总结

在本章中，你学习了如何使用 `async` 修饰符和 `await` 运算符来定义异步方法。异步方法基于任务（tasks），而 `await` 运算符指定了可以使用任务来执行异步处理的时间点。

你还学习了一些关于 PLINQ 的知识，以及如何使用 `AsParallel` 方法来使某些 LINQ 查询并行化。然而，PLINQ 本身是一个庞大的课题，本章仅向你展示了如何入门。欲了解更多信息，请参阅 Visual Studio 提供的文档中的“并行 LINQ (PLINQ)”主题。

本章还向你展示了如何在并发任务中同步数据访问，正如你看到了如何使用并发集合类来以线程安全的方式维护数据集合。

- 如果你想继续阅读下一章，请保持 Visual Studio 2022 运行，并转到第 25 章“为通用 Windows 平台应用实现用户界面”。
- 如果你想现在退出 Visual Studio 2022，请在“文件”菜单上选择“退出”。如果看到“保存”对话框，请选择“是”并保存项目。

# 快速参考

|  | 执行操作 |
| :--- | :--- |
| 实现异步方法 | 使用 `async` 修饰符定义方法，并将方法的类型更改为返回 `Task` 对象（或 `void`）。在方法体中，使用 `await` 运算符来指定可以执行异步处理的时间点。例如：

点击此处查看代码图像

```csharp
private async Task<int> calculateValueAsync(...)
{
    // 使用 Task 调用 calculateValue
    Task<int> generateResultTask =
    Task.Run(() => calculateValue(...));
    await generateResultTask;
    return generateResultTask;
}
```

| 将 LINQ 查询并行化 | 在查询中的数据源上指定 `AsParallel` 扩展方法。例如：

点击此处查看代码图像

```csharp
var over100 = from n in numbers.AsParallel()
where ...
select n;
```

| 在 PLINQ 查询中启用取消 | 在 PLINQ 查询中使用 `ParallelQuery` 类的 `WithCancellation` 方法并指定取消令牌。例如：

点击此处查看代码图像

```csharp
CancellationToken tok = ...;
...
var orderInfoQuery =
from c in CustomersInMemory.Customers.
AsParallel().WithCancellation(tok)
join o in OrdersInMemory.Orders.AsParallel()
on ...
``` | 同步一个或多个任务以实现对共享数据的线程安全独占访问 | 使用 `lock` 语句来保证对数据的独占访问。例如：

点击此处查看代码图像
```csharp
object myLockObject = new object();
...
lock (myLockObject)
{
    // 需要对共享资源
    // string独占访问的代码
...
}
``` | 同步线程并让它们等待事件 | 使用 `ManualResetEventSlim` 对象同步不确定数量的线程。使用 `CountdownEvent` 对象等待事件被信号指定的次数。使用 `Barrier` 对象协调指定数量的线程并在操作的特定点对它们进行同步。 | 同步对共享资源池的访问 | 使用 `SemaphoreSlim` 对象。在构造函数中指定池中的项目数量。在访问共享池中的资源之前调用 `Wait` 方法。在完成资源后调用 `Release` 方法。例如：

点击此处查看代码图像
```csharp
SemaphoreSlim semaphore = new SemaphoreSlim(3);
...
semaphore.Wait();
// 从池中访问资源
...
semaphore.Release();
``` | | 为资源提供独占写访问但共享读访问 | 使用 `ReaderWriterLockSlim` 对象。在读取共享资源之前，调用 `EnterReadLock` 方法。完成后调用 `ExitReadLock` 方法。在写入共享资源之前，调用 `EnterWriteLock` 方法。在完成写入操作后调用 `ExitWriteLock` 方法。例如：

点击此处查看代码图像
```csharp
ReaderWriterLockSlim readerWriterLock = new ReaderWriterLockSlim();

Task readerTask = Task.Factory.StartNew(() => {
    readerWriterLock.EnterReadLock();
    // 读取共享资源
    readerWriterLock.ExitReadLock();
});

Task writerTask = Task.Factory.StartNew(() => {
    readerWriterLock.EnterWriteLock();
    // 写入共享资源
    readerWriterLock.ExitWriteLock();
});
``` | | 取消阻塞操作 | 从 `CancellationSource` 对象创建取消令牌，并将此令牌作为等待操作的参数。要取消等待操作，请调用 `CancellationSource` 对象的 `Cancel` 方法。例如：

点击此处查看代码图像

```csharp
CancellationTokenSource cancellationSource = new
CancellationTokenSource();
CancellationToken cancellation = cancellationSource.Token;
...
// 保护3个资源池的信号量
SemaphoreSlim semaphore = new SemaphoreSlim(3);

// 等待信号量，如果
// 另一个线程取消则抛出
// OperationCanceledException
semaphore.Wait(cancellation);
``` | # 为通用 Windows 平台应用实现用户界面

完成本章后，你将能够：