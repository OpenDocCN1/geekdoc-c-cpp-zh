
## `System.IO.WindowsRuntimeStorageExtensions`

```cs
namespace System.IO {
    // 定义在 System.Windows.Runtime.dll 中
    public static class WindowsRuntimeStorageExtensions {
        public static Task<Stream> OpenStreamForReadAsync(this IStorageFile file);
        public static Task<Stream> OpenStreamForWriteAsync(this IStorageFile file);

        public static Task<Stream> OpenStreamForReadAsync(this IStorageFolder rootDirectory,
            String relativePath);
        public static Task<Stream> OpenStreamForWriteAsync(this IStorageFolder rootDirectory,
            String relativePath, CreationCollisionOption creationCollisionOption);
    }
}
```

这是一个使用其中一个扩展方法来打开 WinRT `StorageFile` 并将其内容读取到 .NET Framework `XElement` 对象的示例。

```cs
async Task<XElement>FromStorageToFileXElement(StorageFile file) {
    using (Stream stream = await file.OpenStreamForReadAsync()) {
        return XElement.Load(stream);
    }
}
```

最后，`System.IO.WindowsRuntimeStreamExtensions` 提供了扩展方法，这些方法可以将 WinRT 流接口（作为 `IRandomAccessStream`、`IInputStream` 或 `IOutputStream`）“强制转换”为 .NET Framework 的流类型，反之亦然。

```cs
namespace System.IO { // 定义在 System.Runtime.dll 中
    public static class WindowsRuntimeStreamExtensions {
        public static Stream AsStream(this IRandomAccessStream winRTStream);
        public static Stream AsStream(this IRandomAccessStream winRTStream, Int32 bufferSize);

        public static Stream AsStreamForRead(this IInputStream winRTStream);
        public static Stream AsStreamForRead(this IInputStream winRTStream, Int32 bufferSize);

        public static Stream AsStreamForWrite(this IOutputStream winRTStream);
        public static Stream AsStreamForWrite(this IOutputStream winRTStream, Int32 bufferSize);

        public static IInputStream AsStream(this Stream stream);
        public static IOutputStream AsStream(this Stream stream);
    }
}
```

这是一个使用其中一个扩展方法将 WinRT `IInputStream` “强制转换”为 .NET Framework `Stream` 对象的示例。

```cs
XElement FromWinRTStreamToXElement(IInputStream winRTStream) {
    Stream netStream = winRTStream.AsStreamForRead();
    return XElement.Load(netStream);
}
```

请注意，.NET Framework 提供的“强制转换”扩展方法在底层执行的工作不仅仅是强制转换。具体而言，那些将 WinRT 流适配到 .NET Framework 流的方法会隐式地在托管堆中为 WinRT 流创建一个缓冲区。因此，大多数操作都会写入到此缓冲区，而不需要跨越互操作边界，从而提高了性能。这在涉及许多小型 I/O 操作的场景中（例如解析 XML 文档）尤为显著。

使用 .NET Framework 流投影的用处之一，如果你在同一个 WinRT 流实例上多次使用 `AsXXX` 方法，你就不需要担心创建不同的、不相连的缓冲区，并且写入一个缓冲区的数据不会在另一个缓冲区中可见。.NET Framework 的 API 确保每个对象都有唯一的适配器实例，且所有用户共享同一个缓冲区。

尽管在大多数情况下，默认缓冲在性能和内存使用之间提供了很好的折中，但在某些情况下，你可能希望调整缓冲区的大小，使其与 16-KB 的默认值不同。`AsStreamXxx` 方法提供了重载。例如，如果你知道你将长时间处理一个非常大的文件，并且同时没有使用许多其他缓冲流，你可以通过请求较大的缓冲区来获得额外的性能。相反，在某些对延迟有要求的场景中，你可能希望确保从网络读取的字节少于应用程序请求的。在这种情况下，你可以完全禁用缓冲。如果向 `AsStreamXxx` 方法传递零字节的缓冲区，则不会创建对象。

## 在 CLR 和 WinRT 之间传递数据块

可能的情况下，你应该使用上一节讨论的流投影，因为它们具有良好的性能。但在某些时候，你需要在 CLR 和 WinRT 组件之间传递原始数据块。例如，WinRT 的文件和套接流组件需要读写原始数据块。此外，字体组件加密和解密数据，位像素也以原始数据块的形式维护。

在 .NET Framework 中，获取数据块的方法是使用字节数组（`[]`）或流（使用 `MemoryStream` 类）。当然，字节数组和 `MemoryStream` 对象无法直接传递给 WinRT 组件。因此，WinRT 定义了一个 `IBuffer` 接口，实现该接口的对象表示可以传递给 WinRT API 的原始数据块。WinRT 接口如下：

```cs
namespace Windows.Storage.Streams {
 public IBuffer {
  UInt32 Capacity { get; } //缓冲区的最大大小（字节）
  UInt32 Length { get; set; } //缓冲区当前使用的字节数
}
}
```

如你所见，`IBuffer` 对象有一个最大尺寸和长度；奇怪的是，此接口并没有提供任何从缓冲区读取或向其写入数据的方法。主要原因是 WinRT 类型在元数据中不能包含指针，因为指针无法很好到某些语言（如 JavaScript 或 C# 代码）。因此，`IBuffer` 对象实际上只是在 CLR 和 WinRT API 之间传递内存地址的一种。为了访问内存地址处的字节，使用了名为 `IBufferByteAccess` 的内部 COM 接口。注意，这是一个 COM 接口（因为它返回指针），而不是 WinRT 接口。.NET Framework 团队为此接口定义了一个内部 RCW，如下所示：

```cs
namespace System.Runtime.Interop.WindowsRuntime {
 [Guid("905a0aef-bc53-11df-dc49-001e4fc686da")]
 [InterfaceType(ComInterfaceType.InterfaceIsUnknown)]
 interface IBufferByteAccess {
 unsafe Byte* Buffer { get; }
}
}
```

在内部，CLR 可以获取一个 `IBuffer` 对象，查询其 `IBufferByte` 接口，然后查询 `Buffer` 属性以获取缓冲区内包含字节的不安全指针（unsafe pointer）。有了指针后，可以直接访问这些字节。

为了避免开发者编写操作指针的不安全代码，框架类库（FCL）包含一个 `RuntimeExtensions` 类，该类定义了一系列扩展方法，.NET 开发者显式调用这些方法来帮助将从 CLR 字节数组和流传递块到 WinRT 对象。要调用这些扩展方法，请确保在源代码中使用了 `System.Runtime.InteropServices.WindowsRuntime;` 指令。

```c
namespace System.Runtime.InteropServices.WindowsRuntime {
    public static class WindowsBufferExtensions {
        public static IBuffer AsBuffer(this Byte[] source);
        public static IBuffer AsBuffer(this Byte[] source, Int32 offset, Int32 length);
        public static IBuffer AsBuffer(this Byte[] source, Int32 offset, Int32 length, Int32 capacity);
    }
}
```

```c
public static IBuffer GetWindowsRuntimeBuffer(MemoryStream stream);
public static IBuffer GetWindowsRuntimeBuffer(MemoryStream stream);
```

因此，如果你有一个 `Byte[]` 并且想通过 `IBuffer` 将其传递给 WinRT API，只需在 `Byte[]` 上调用 `AsBuffer` 即可。这有效地将 `Byte[]` 的引用封装在一个实现 `IBuffer` 接口的对象内部；`Byte[]` 的内容不会被复制，因此这非常高效。同样，如果你有一个封装了可见 `Byte[]` 数组且未复制的 `MemoryStream` 对象，可以对其调用 `GetWindowsRuntimeBuffer`，将 `MemoryStream` 缓冲区的引用封装在一个实现 `IBuffer` 接口的对象内部。缓冲区的内容不会被复制，因此这非常高效。以下方法演示了这些场景。

```csharp
private async Task ByteArrayAndStreamToBuffer(IRandomAccessStream winRT, Int32 count) {
    Byte[] bytes = new Byte[count];
    await winRT.ReadAsync(bytes.AsBuffer(), (Int32)bytes.Length, InputStreamOptions.None);
    Int32 sum = bytes.Sum(b => b); // 通过 Byte[] 访问读取的字节
```

```csharp
using (var ms = new MemoryStream()) {
    using (var sw = new StreamWriter(ms)) {
        sw.Write("This string represents data in a stream");
        sw.Flush();
        UInt32 bytesWritten = await winRT.WriteAsync(ms.GetWindowsRuntimeBuffer());
    }
}
```

`IRandomAccessStream` 接口实现 WinRT `IInputStream` 接口的方式如下。

```csharp
namespace Windows.Storage.Streams {
    public interface IOutputStream : IDisposable {
        IAAsyncOperationWithProgress<UInt32, UInt32> WriteAsync(IBuffer buffer);
    }
}
```

当你在代码中调用 `AsBuffer` 或 `GetWindowsRuntime` 方法时，这些方法会将源对象封装在一个实现 `IBuffer` 接口的对象中。CLR 为其创建一个 CCW 并将其传递给 WinRT API。WinRT API 查询 `IBufferAccess` 接口的 `Buffer` 以获取指向底层字节数组的指针，该数组被固定（pinned），地址返回给 WinRT API 以便其访问数据。当 WinRT API 在内部调用 `IBufferAccess` 接口上的 COM `Release` 方法时，数据会被取消固定。

如果你调用了返回 `IBuffer` 给你的 WinRT API，数据本身可能在原生内存中，你将需要从托管代码访问这些数据。为了实现这一点，我们将转向 `WindowsRuntimeBufferClasses` 定义的其他扩展方法。

```csharp
namespace System.Interop.WindowsRuntime {
    public static class WindowsRuntimeExtensions {
        public static Stream AsStream(IBuffer source);
        public static Byte[] ToArray(IBuffer source);
        public static Byte[] ToArray(IBuffer source, UInt32 sourceIndex, Int32 count);

        // 未显示：CopyTo 方法，用于在 IBuffer 和 Byte[] 之间传输字节
        // 未显示：GetByte, IsSameData 方法
    }
}
```

`AsStream` 方法创建了一个由 `Stream` 驱动的对象，封装了源 `IBuffer`。通过该对象，你可以调用 `Stream.Read` 类似的方法访问 `IBuffer` 中的数据。`ToArray` 方法在内部将从源 `IBuffer` 的所有字节分配到 `Byte[]` 中；请注意，该扩展方法在内存消耗和 CPU 时间方面可能开销较大。

`WindowsRuntimeBufferExtensions` 类还有几个 `CopyTo` 方法的重载，可以在 `IBuffer` 和 `Byte[]` 之间复制字节。它还有一个 `GetByte` 方法，可以从 `IBuffer` 中一次检索一个字节，以及一个 `IsSameData` 方法，用于比较两个 `IBuffer` 对象的内容以查看其内容是否相同。对于大多数应用程序，你不太可能调用所有这些方法。

我想指出的是，.NET Framework 定义了一个 `System.Interop.Runtime.WindowsRuntimeBuffer` 类，它允许你创建一个字节位于托管堆中的 `IBuffer`。同样，还有一个对名为 `Windows.Storage.Streams.Buffer` 的 WinRT 组件，它允许你创建一个字节位于原生堆中的 `IBuffer`。对于大多数 .NET 开发者来说，可能不需要在代码中显式地使用其中任何一个类。

## 在 C# 中定义 WinRT 组件

到本章为止，我一直关注于如何从 C# 消费 WinRT 组件。然后这些组件可以被 C/C++、C#/Visual Basic、JavaScript 以及可能的其他语言使用。虽然这是可行的，但我们需要考虑这种做法真正有意义的场景。例如，在 C# 中定义 WinRT 组件毫无意义，如果该组件的唯一消费者是运行在 CLR 之上的其他托管语言。这是因为 WinRT 类型的功能少得多，这使其比 CLR 的类型系统要严格得多。

我不认为用 C# 实现一个可以被原生 C/C++ 代码消费的 WinRT 组件是有意义的。使用原生 C/C++ 实现应用程序的开发者可能是因为他们非常关注性能/或内存消耗。他们不太可能利用用托管代码实现的 WinRT 组件，因为这迫使 CLR 加载到他们的进程中，并由于垃圾收集和代码即时编译（JIT）增加了他们的内存需求并影响了性能。由于这些原因，大多数 WinRT 组件（如 Windows 自身的组件）都是用原生代码实现的。当然，原生 C++ 应用中可能某些部分对性能不敏感，在此时，利用 .NET Framework 功能来提高生产力是有意义的。例如，Bing Maps 使用原生 C++ 使用 DirectX 绘制其 UI，但也使用 C# 处理其业务逻辑。

因此对我来说，C# 实现组件的黄金平衡点是：Windows Store 应用开发者，他们希望使用 HTML 构建用户界面，然后使用 JavaScript 作为胶水代码，将 UI 与在 C# WinRT 组件中实现的业务逻辑连接起来。另一个场景是从 HTML/JavaScript 应用中利用框架类库功能（如 Windows Communication）。处理 HTML 和 JavaScript 的开发者已经愿意接受浏览器引擎带来的性能和内存消耗，并且可能愿意进一步接受 CLR 带来的额外性能和内存消耗。
