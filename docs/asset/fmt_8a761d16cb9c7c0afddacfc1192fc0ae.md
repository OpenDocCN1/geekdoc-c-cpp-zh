
- 10. 在 `try` 块中修改 `plotButton_Click` 方法中生成图表数据的语句，使其异步调用 `generateGraphDataAsync` 方法，如下所示加粗：

Click here to view code image

```
try
{
    await generateGraphDataAsync(data, 0, pixelWidth / 2, token);
    duration.Text = $"Duration (ms): {watch.ElapsedMilliseconds}";
}
...
```

- 11. 在 `Debug` 菜单上，指向 `Windows`，然后单击 `Exception Settings`。
  在 `Exception Settings` 窗口中，清除 `Common Language Runtime Exceptions` 的复选框。右键单击 `Common Language Runtime Exceptions`，然后确保 `Continue When Unhandled In User Code` 已启用。
- 12. 在 `Debug` 菜单上，单击 `Start Debugging`。
- 13. 在 `GraphDemo` 窗口中，单击 `Plot Graph` 并验证应用程序是否正确生成图表。
- 14. 单击 `Plot Graph`，然后在数据生成期间单击 `Cancel`。
  这次，用户界面应保持响应。仅生成部分图表，并且 `duration TextBlock` 应显示消息“`The operation was cancelled.`”

![](img/16f6e3fe08f01ddadb2741a92c392b0e_665_0.png)

- 15. 返回到 Visual Studio 并停止调试。

## Defining asynchronous methods that return values

到目前为止，你所看到的所有示例都使用 `Task` 对象来执行不返回值的工作。然而，你也使用任务来运行计算结果的方法。为此，你使用泛型 `Task<TResult>` 类，其中

类型参数 `TResult` 指定结果的类型。

你创建并启动 `Task<TResult>` 对象的方式与普通 `Task` 类类似。主要区别在于你执行的代码应返回一个值。例如，下文代码示例中名为 `calculateValue` 的方法会生成一个整数结果。要通过任务调用此方法，你需要创建并运行一个 `Task<int>` 对象。你可以通过查询 `Task<int>` 对象的 `Result` 属性来获取方法返回的值。如果任务尚未运行完方法且结果尚未可用，`Result` 属性会阻塞调用者。这意味着你无需自行执行任何同步操作，并且当 `Result` 属性返回一个值时，你可以确定任务已完成其工作。

Click here to view code image

```
Task<int> calculateValueTask = Task.Run(() => calculateValue(...));
...
int calculatedData = calculateValueTask.Result; // Block until
calculateValueTask completes
...
private int calculateValue(...)
{
    int someValue;
    // Perform calculation and populate someValue
    ...
    return someValue;
}
```

泛型 `Task<TResult>` 类型也是定义返回值的异步方法的机制的基础。在之前的示例中，你看到过通过返回 `Task` 来实现异步 `void` 方法。如果异步方法确实生成了一个结果，它应返回 `Task<TResult>`，如下例所示，该示例创建了 `calculateValue` 方法的异步版本：

Click here to view code image

```
private async Task<int> calculateValueAsync(...)
{
    // Invoke calculateValue using a Task
    Task<int> generateResultTask = Task.Run(() =>
calculateValue(...));
    await generateResultTask;
    return generateResultTask.Result;
}
```

此方法看起来有些令人困惑，因为返回类型指定为 `Task<int>`，但 `return` 语句实际上返回的是一个 `int`。请记住，当你定义 `async` 方法时，编译器会对你的代码进行一些重构，它本质上返回对 `Task` 的引用，该 `Task` 运行语句 `return generateResultTask.Result;` 的延续。此延续返回的表达式的类型为 `int`，因此该方法的返回类型为 `Task<int>`。

要调用返回值的异步方法，请使用 `await` 运算符，如下所示：

Click here to view code image

```
int result = await calculateValueAsync(...);
```

`await` 运算符从 `calculateValueAsync` 方法返回的 `Task` 中提取值，并在此例中将其赋给 `result` 变量。

## Asynchronous method gotchas

`async` 和 `await` 运算符一直让程序员感到困惑。重要的是要理解：

- 将方法标记为 `async` 并不意味着它会异步运行。它意味着该方法可以包含可能异步运行的语句。
- `await` 运算符表示应由单独的任务运行方法，并且调用代码会被挂起，直到方法调用完成。调用代码使用的线程会被释放并可被重用。如果该线程是用户界面线程，这一点很重要，因为它使用户界面保持响应。
- `await` 运算符与使用任务的 `Wait` 方法不同。`Wait` 方法始终阻塞当前线程，并且在任务完成之前不允许重用该线程。
- 默认情况下，`await` 运算符之后恢复执行的代码会尝试获取用于调用异步方法调用的原始线程。如果此线程忙，代码将被阻塞。你可以使用 `ConfigureAwait(false)` 方法指定代码可以在任何可用线程上恢复，从而降低阻塞的可能性。这对于可能需要处理数千个并发请求的 Web 应用程序和服务尤其有用。
- 如果 `await` 运算符之后运行的代码必须在原始线程上执行，就不应该使用 `ConfigureAwait(false)`。在前面讨论的示例中，在每个 `awaited` 操作上添加 `ConfigureAwait(false)` 将导致编译器生成的延续很可能在单独的线程上运行。这包括尝试为 `message` 设置 `Text` 属性的延续，这将再次导致异常“应用程序调用了为不同线程 marshaled 的接口”。

Click here to view code image

```
private async void slowMethod()
{
    await doFirstLongRunningOperation().ConfigureAwait(false);
    await doSecondLongRunningOperation().ConfigureAwait(false);
    await doThirdLongRunningOperation().ConfigureAwait(false);
    message.Text = "Processing Complete";
}
```

不慎使用在用户界面线程上运行并返回结果的异步方法可能会产生死锁，导致应用程序冻结。请考虑以下示例：

Click here to view code image

```
private async void myMethod()
{
    var data = generateResult();
    ...
    message.Text = $"result: {data.Result}";
}
private async Task<string> generateResult()
{
    string result;
    ...
    result = ...
    return result;
}
```

在此代码中，`generateResult` 方法返回一个字符串值。然而，`myMethod` 方法要到尝试访问 `data.Result` 属性时才会真正启动运行 `generateResult` 方法的任务；`data` 是对任务的引用，如果 `Result` 属性不可用，因为任务尚未运行，则访问此属性将阻塞当前线程，直到 `generateResult` 方法完成。此外，用于运行 `generateResult` 方法的任务在方法完成时尝试在调用它的线程上恢复，该线程是用户界面线程，但此时该线程已被阻塞。结果是 `myMethod` 方法无法在 `generateResult` 方法完成之前结束，而 `generateResult` 方法也无法在 `myMethod` 方法完成之前结束。

解决此问题的办法是等待运行 `generateResult` 方法的任务。你可以按如下方式执行：

Click here to view code image

```
private async void myMethod()
{
    var data = generateResult();
    ...
    message.Text = $"result: {await data}";
}
```

## Asynchronous methods and the Windows Runtime APIs

Windows 8 及更高版本的的设计者希望确保应用程序尽可能具有响应性，因此在他们实现 WinRT 时做出了决定，任何可能需要超过 50 毫秒才能完成的操作都应仅通过异步 API 提供。你可能已经在本书中注意到一两个这样的例子。例如，要向用户显示一条消息，你可以使用 `MessageDialog` 对象。然而，当你显示此消息时，你必须使用 `ShowAsync` 方法，如下所示：

Click here to view code image

```
using Windows.UI.Popups;
...
MessageDialog dlg = new MessageDialog("Message to user");
await dlg.ShowAsync();
```

`MessageDialog` 对象显示消息并等待用户单击此对话框中出现的 Close 按钮。任何形式的

硬盘上文件的抽象，通过使用此类，你可以打开文件并从中读取或写入。

## Note

严格来说，`PickSingleFileAsync` 方法返回类型为 `IAsyncOperation<StorageFile>` 的对象。WinRT 使用其自身的异步操作抽象，并将 .NET Framework `Task` 对象映射到该抽象；`Task` 类实现了 `IAsyncOperation` 接口。如果你使用 C# 编程，你的代码不受此转换的影响，可以直接使用 `Task` 对象，而无需关心它们如何映射到 WinRT 异步操作。

文件输入/输出（I/O）是另一个可能导致操作缓慢的来源，而 `StorageFile` 类实现了大量异步方法，可在不影响应用程序响应性的情况下执行这些操作。例如，在第 5 章中，用户使用 `FileOpenPicker` 对象选择文件后，代码随后以异步方式打开该文件进行读取：

Click here to view code image

```
StorageFile file = await fp.PickSingleFileAsync();
...
var fileStream = await file.OpenAsync(FileAccessMode.Read);
```

下面是一个与本章和上一章中你所见的练习直接相关的最终示例，涉及向流写入数据。你可能已经注意到，虽然生成图表数据的报告时间为几秒钟，但图表实际出现可能需要多达两倍的时间。这是因为数据写入位图的方式。位图将 `WriteableBitmap` 对象中缓冲区保存的数据渲染出来，而 `AsStream` 扩展方法为此缓冲区提供 `Stream` 接口。数据通过此流使用 `Write` 方法写入缓冲区，如下所示：

Click here to view code image

```
...
Stream pixelStream = graphBitmap.PixelBuffer.AsStream();
pixelStream.Seek(0, SeekOrigin.Begin);
pixelStream.Write(data, 0, data.Length);
...
```

除非你已将 `pixelWidth` 和 `pixelHeight` 字段的值降低以节省内存，否则写入缓冲区的數據量略高于 570 MB（15,000 * 10,000 * 4 字节），因此此 `Write` 操作可能需要几秒钟。为了提高响应时间，你可以使用 `WriteAsync` 方法以异步方式执行此操作：

Click here to view code image

```
await pixelStream.WriteAsync(data, 0, data.Length);
```

总之，当你为 Windows 构建应用程序时，应尽可能利用异步性。

## .NET Framework 早期版本中的 IAsyncResult 设计模式

异步性长期以来被认为是使用 .NET Framework 构建响应式应用程序的关键要素，并且该概念早于 .NET Framework 4.0 中引入 `Task` 类。Microsoft 引入了基于 `AsyncCallback` 委托类型的 `IAsyncResult` 设计模式来处理这些情况。该模式的工作细节在此书中不作详述，但从程序员的角度来看，该模式的实现意味着 .NET Framework 类库中的许多类型以两种方式公开长时间运行的操作：同步形式由单个方法组成，以及异步形式使用一对方法，命名为 `BeginOperationName` 和 `EndOperationName`，其中 `OperationName` 指定正在执行的操作。例如，`System.IO` 命名空间中的 `MemoryStream` 类提供 `Write` 方法以同步方式向内存流写入数据，但它也提供 `BeginWrite` 和 `EndWrite` 方法以异步方式执行相同操作。`BeginWrite` 方法在新线程上启动写入操作。`BeginWrite` 方法期望程序员提供一个回调方法的引用，该方法在写入操作完成后运行；此引用采用 `AsyncCallback` 委托的形式。在此方法中，程序员应执行适当的清理工作并调用 `EndWrite` 方法以表示操作已完成。以下代码示例展示了该模式的实际应用：

Click here to view code image

```
...
Byte[] buffer = ...; // populated with data to write to the MemoryStream
MemoryStream ms = new MemoryStream();
AsyncCallback callback = new AsyncCallback(handleWriteCompleted);
ms.BeginWrite(buffer, 0, buffer.Length, callback, ms);
...
private void handleWriteCompleted(IAsyncResult ar)
{
    MemoryStream ms = ar.AsyncState as MemoryStream;
    ... // Perform any appropriate tidying up
    ms.EndWrite(ar);
}
```
