

# 注意事项

严格来说，`PickSingleFileAsync` 方法返回一个类型为 `IAsyncOperation<StorageFile>` 的对象。WinRT 使用自己的异步操作抽象，并将 .NET `Task` 对象映射到此抽象上；`Task` 实现了 `IAsyncOperation` 接口。如果你使用 C# 编程，你的代码不受此转换的影响，你可以直接使用 `Task` 对象，而无需担心它们是如何映射到 WinRT 异步操作的。

文件输入/输出 (I/O) 是另一个可能导致操作缓慢的来源。`StorageFile` 类实现了多个异步方法，通过这些方法，可以在不影响应用程序响应能力的情况下执行操作。例如，在第 5 章中，用户使用 `FileOpenPicker` 对象选择文件后，代码将以异步方式打开该文件进行读取：

点击此处查看代码

```
StorageFile file = await fp.PickSingleFileAsync();
var fileStream = await file.OpenAsync(FileAccessMode.Read);
```

有一个示例直接适用于你在本章中看到的练习，以及之前关于向流写入的考虑。你可能注意到，尽管报告生成图表数据的时间只有几秒钟，但图表实际出现可能需要花费两倍的时间。这是由于数据写入位图的方式造成的。位图在 `WriteableBitmap` 对象的缓冲区中作为数据渲染数据，而 `AsStream` 扩展方法为该缓冲区提供了一个 `Stream` 接口。数据通过此流使用 `Write` 方法写入缓冲区，如下：

点击此处查看代码

```
Stream pixelStream = graphBitmap.PixelBuffer.AsStream();
pixelStream.Seek(0, SeekOrigin.Begin);
```

pixelStream.Write(data, 0, data.Length);
...

除非你减小了 `pixelWidth` 和 `pixel` 字段的值以节省内存，否则写入缓冲区的数据值略高于 570 MB (15,000 * 10,000 * 4 字节)，因此此 `Write` 操作可能需要几秒钟。为了提高响应时间，你可以使用 `WriteAsync` 方法异步执行此操作：

点击此处查看代码

```
await pixelStream.WriteAsync(data, 0, data.Length);
```

总而言之，当你为 Windows 构建应用程序时，应该尽可能寻求利用异步性。

# 任务、内存分配与效率

仅仅因为一个方法被标记为 `async`，并不意味着它总是异步执行的。考虑以下方法：

点击此处查看代码

```
public async Task<int> FindValueAsync(string key)
{
    bool foundLocally = GetCachedValue(key, out int result);
    if (foundLocally)
        return result;

    result = await RetrieveValue(key); // 可能需要很长时间
    AddItemToLocalCache(key, result);
    return result;
}
```

此方法的目的是查找与字符串键关联的整数值。例如，你可能根据客户名称查找客户 ID，或者可能根据包含加密密钥的字符串检索一段数据。`FindValueAsync` 方法实现了缓存旁路模式（Cache-Aside pattern，关于此模式的详细讨论请参见 https://docs.microsoft.com/en-us/azure/patterns/cache-aside），该模式在执行可能耗时的计算或查找操作时，将结果在执行时缓存到缓存中，以防在不久的将来再次需要。如果将相同的键值传递给 `FindValueAsync` 的后续调用，则可以检索缓存数据。

缓存旁路模式使用以下辅助方法（这些方法的实现未显示）：

- * GetCachedValue* 此方法检查缓存中是否存在具有指定键的项，如果该项可用，则通过 `out` 参数将其传回。如果在缓存中找到数据，则方法的返回值为 `true`，否则为 `false`。
- *RetrieveValue* 如果在缓存中未找到项，则运行此方法。它执行查找数据所需的计算或查找并返回它。此方法的运行可能需要很长时间，因此它是异步执行的。
- * AddItemLocalCache* 如果再次请求指定的项，则此方法将该项添加到本地缓存中。这将避免应用程序执行昂贵的 `RetrieveValue` 操作。

在理想世界中，缓存将涵盖应用程序生命周期内请求的大部分数据，而需要调用 `RetrieveValue` 的次数将变得微乎其微。

现在考虑每当你的代码调用 `FindValueAsync` 方法时会发生什么。在大多数情况下，工作将同步执行。（它在缓存中找到数据。）数据在缓存中找到。数据在 `Task<int>` 对象中。创建此对象并从该对象检索数据比简单返回返回 `int` 需要更多的精力和内存分配。C# 通过提供 `ValueTask` 类型来应对这种情况：

点击此处查看代码

```
public async ValueTask<int> FindValueAsync(string key)
{
    bool foundLocally = GetCachedValue(key, out int result);
    if (foundLocally)
        return result;

    result = await RetrieveValue(key); // 可能需要很长时间
    AddItemToLocalCache(key, result);
    return result;
}
```

这并不意味着你应该始终使用 `ValueTask` 而不是 `Task`。如果异步方法的绝大多数调用可能是同步执行的，请考虑返回 `ValueTask`；否则，请坚持使用 `Task`。

> 注意
> 要使用 `ValueTask` 类型，你必须使用 NuGet 包管理器将 `System.Threading.Tasks.Extensions` 包添加到你的项目中。

# .NET 早期版本的 IAsyncResult 设计模式

异步性长期以来被认为是构建 .NET 响应式应用程序的关键元素，该概念早于 .NET Framework 4.0 版本引入 `Task` 类。微软引入了基于 `AsyncCallback` 委托类型的 `IAsyncResult` 设计模式来处理这些情况。

该模式如何工作的精确细节超出了本书的范围，从程序员的角度来看，该模式的实现意味着 .NET 类库中经常以两种方式暴露长耗时操作：

- 由单个方法组成的同步形式
- 使用一对命名为 `BeginOperationName` 和 `EndOperationName` 的方法的异步形式，其中 `OperationName` 指定正在执行的操作

例如，`System.IO` 命名空间下的 `MemoryStream` 类提供了 `Write` 方法将数据同步写入内存流，但它还提供了 `BeginWrite` 和 `EndWrite` 方法来异步执行相同的操作。`BeginWrite` 方法启动在新线程上执行的写入操作。`BeginWrite` 方法期望程序员提供指向在操作完成后运行的回调方法的引用；该引用是 `AsyncCallback` 委托的形式。在该方法中，程序员应该实现任何适当的清理并调用 `EndWrite` 方法以表示操作完成。以下代码示例展示了该模式的操作：

点击此处查看代码

```
Byte[] buffer = ...; // 填充了要写入 MemoryStream 的数据
MemoryStream ms = new MemoryStream();
AsyncCallback callback = new AsyncCallback(handleWriteCompleted);
ms.BeginWrite(buffer, 0, buffer.Length, callback, ms);

private void handleWriteCompleted(IAsyncResult ar)
{
    MemoryStream ms = ar.AsyncState as MemoryStream;
    // 执行任何必要的清理
    ms.EndWrite(ar);
}
```

虽然这个序列可以工作，但它是一种模糊了你正在执行的操作的混乱范式。操作代码被分成了两个部分

