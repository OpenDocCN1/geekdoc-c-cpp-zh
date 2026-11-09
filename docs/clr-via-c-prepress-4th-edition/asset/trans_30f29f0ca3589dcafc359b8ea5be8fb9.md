

```csharp
    return XElement.Load(netStream);
}
```

请注意，.NET Framework 提供的“强制转换”扩展方法在底层所做的并不只是强制转换。具体而言，这些将 WinRT 流适配为 .NET Framework 流的方法会隐式在托管堆中为 WinRT 流创建一个缓冲区。因此，大多数操作会写入此缓冲区，而无需跨越互操作边界，从而提高性能。在涉及大量小型 I/O 操作的场景（例如解析 XML 文档）中，这一点尤为重要。

使用 .NET Framework 的流投影的好处之一是，如果你在同一个 WinRT 流实例上多次使用 AsStreamXxx 方法，不必担心会创建彼此不同且互不连通的缓冲区，也不必担心写入一个缓冲区的数据在另一个缓冲区中不可见。.NET Framework API 确保每个流对象都有唯一的适配器实例，并且所有使用者共享同一个缓冲区。

虽然在大多数情况下，默认缓冲在性能和内存使用之间提供了良好的折中，但在某些情况下，你可能希望调整缓冲区大小，使其不同于默认的 16KB。AsStreamXxx 方法为此提供了重载。例如，如果你知道将在很长一段时间内处理一个非常大的文件，并且同时不会使用许多其他缓冲流，那么可以通过为流请求一个非常大的缓冲区来获得一些额外性能。相反，在一些要求低延迟的网络场景中，你可能希望确保从网络读取的字节数不会超过应用程序显式请求的字节数。在这种情况下，你可以完全禁用缓冲。如果向 AsStreamXxx 方法指定零字节的缓冲区大小，则不会创建任何缓冲区对象。

## 在 CLR 和 WinRT 之间传递数据块

在可能的情况下，你应使用上一节讨论的流框架投影，因为它们具有相当好的性能特征。然而，有时你可能需要在 CLR 和 WinRT 组件之间传递原始数据块。例如，WinRT 的文件和套接字流组件要求你写入和读取原始数据块。此外，WinRT 的加密组件会对数据块进行加密和解密，位图像素也保存在原始数据块中。

在 .NET Framework 中，获取数据块的常用方式是使用字节数组（Byte[]）或流（例如使用 MemoryStream 类时）。当然，字节数组和 MemoryStream 对象不能直接传递给 WinRT 组件。因此，WinRT 定义了 IBuffer 接口，实现此接口的对象表示可传递给 WinRT API 的原始数据块。WinRT 的 IBuffer 接口定义如下：

```csharp
namespace Windows.Storage.Streams {
    public interface IBuffer {
        UInt32 Capacity { get; }       // Maximum size of the buffer (in bytes)
        UInt32 Length   { get; set; }  // Number of bytes currently in use by the buffer
    }
}
```

如你所见，IBuffer 对象具有最大大小和长度；奇怪的是，此接口没有提供任何实际读取或写入缓冲区中数据的方法。主要原因在于 WinRT 类型无法在其元数据中表示指针，因为指针无法很好地映射到某些语言（如 JavaScript 或安全 C# 代码）。因此，IBuffer 对象实际上只是一种在 CLR 和 WinRT API 之间传递内存地址的方式。要访问该内存地址处的字节，需要使用名为 IBufferByteAccess 的内部 COM 接口。请注意，此接口是 COM 接口（因为它返回指针），而不是 WinRT 接口。.NET Framework 团队为此 COM 接口定义了一个内部 RCW，如下所示：

```csharp
namespace System.Runtime.InteropServices.WindowsRuntime {
    [Guid("905a0fef-bc53-11df-8c49-001e4fc686da")]
    [InterfaceType(ComInterfaceType.InterfaceIsIUnknown)]
    [ComImport]
    internal interface IBufferByteAccess {
        unsafe Byte* Buffer { get; }
    }
}
```

在内部，CLR 可以接收一个 IBuffer 对象，查询其 IBufferByteAccess 接口，然后查询 Buffer 属性，以获取指向缓冲区中所包含字节的非安全指针。借助该指针，可以直接访问这些字节。

为了避免开发人员编写操作指针的非安全代码，框架类库包含一个 WindowsRuntimeBufferExtensions 类，该类定义了一组扩展方法，.NET Framework 开发人员可以显式调用这些方法，以帮助在 CLR 字节数组和流与 WinRT IBuffer 对象之间传递数据块。若要调用这些扩展方法，请确保在源代码中添加 using System.Runtime.InteropServices.WindowsRuntime; 指令。

```csharp
namespace System.Runtime.InteropServices.WindowsRuntime {
    public static class WindowsRuntimeBufferExtensions {
        public static IBuffer AsBuffer(this Byte[] source);
        public static IBuffer AsBuffer(this Byte[] source, Int32 offset, Int32 length);
        public static IBuffer AsBuffer(this Byte[] source, Int32 offset, Int32 length, Int32 capacity);

        public static IBuffer GetWindowsRuntimeBuffer(this MemoryStream stream);
        public static IBuffer GetWindowsRuntimeBuffer(this MemoryStream stream, Int32 position, Int32 length);
    }
}
```

因此，如果你有一个 Byte[]，并希望将其传递给需要 IBuffer 的 WinRT API，只需对该 Byte[] 数组调用 AsBuffer 即可。这实际上会将指向 Byte[] 的引用包装在一个实现 IBuffer 接口的对象中；不会复制 Byte[] 数组的内容，因此非常高效。类似地，如果你有一个 MemoryStream 对象，其中包装着公开可见的 Byte[] 数组缓冲区，只需对其调用 GetWindowsRuntimeBuffer，即可将指向 MemoryStream 缓冲区的引用包装在一个实现 IBuffer 接口的对象中。同样，缓冲区的内容不会被复制，因此非常高效。以下方法演示了这两种场景：

```csharp
private async Task ByteArrayAndStreamToIBuffer(IRandomAccessStream winRTStream, Int32 count) {
    Byte[] bytes = new Byte[count];
    await winRTStream.ReadAsync(bytes.AsBuffer(), (UInt32)bytes.Length, InputStreamOptions.None);
    Int32 sum = bytes.Sum(b => b);  // Access the bytes read via the Byte[]

    using (var ms = new MemoryStream())
    using (var sw = new StreamWriter(ms)) {
        sw.Write("This string represents data in a stream");
        sw.Flush();
        UInt32 bytesWritten = await winRTStream.WriteAsync(ms.GetWindowsRuntimeBuffer());
    }
}
```

WinRT 的 IRandomAccessStream 接口实现了 WinRT 的 IOutputStream 接口，其定义如下：

```csharp
namespace Windows.Storage.Streams {
    public interface IOutputStream : IDisposable {
        IAsyncOperationWithProgress<UInt32, UInt32> WriteAsync(IBuffer buffer);
    }
}
```

当你在代码中调用 AsBuffer 或 GetWindowsRuntimeBuffer 扩展方法时，这些方法会将源对象包装在一个其类实现 IBuffer 接口的对象中。然后，CLR 会为此对象创建一个 CCW，并将其传递给 WinRT API。当 WinRT API 查询 IBufferByteAccess 接口的 Buffer 属性以获取指向基础字节数组的指针时，该字节数组会被固定，地址会返回给 WinRT API，以便其访问数据。当 WinRT API 在内部对 IBufferByteAccess 接口调用 COM 的 Release 方法时，基础字节数组会被取消固定。

如果你调用某个 WinRT API，而该 API 向你返回一个 IBuffer，那么数据本身很可能位于本机内存中，你需要一种从托管代码访问此数据的方式。为此，我们将使用 WindowsRuntimeBufferExtensions 类定义的其他一些扩展方法：

```csharp
namespace System.Runtime.InteropServices.WindowsRuntime {
    public static class WindowsRuntimeBufferExtensions {
        public static Stream AsStream(this IBuffer source);
        public static Byte[] ToArray(this IBuffer source);
        public static Byte[] ToArray(this IBuffer source, UInt32 sourceIndex, Int32 count);

        // Not shown: CopyTo method with overloads to transfer bytes between an IBuffer and a Byte[]
        // Not shown: GetByte, IsSameData methods
    }
}
```

AsStream 方法会创建一个派生自 Stream 的对象，用于包装源 IBuffer。借助此 Stream 对象，你可以通过调用 Stream 的 Read、Write 及类似方法来访问 IBuffer 中的数据。ToArray 方法会在内部分配一个 Byte[]，然后将源 IBuffer 中的所有字节复制到该 Byte[] 中；请注意，此扩展方法在内存消耗和 CPU 时间方面可能开销较大。

