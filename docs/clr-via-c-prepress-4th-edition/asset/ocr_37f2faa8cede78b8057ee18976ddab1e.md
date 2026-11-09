```
```csharp
    return XElement.Load(netStream);
}
```
```

Note that the “casting” extension methods provided by the .NET Framework do a little more than just casting under the covers. Specifically, the methods that adapt a WinRT stream to a .NET Framework stream implicitly create a buffer for the WinRT stream in the managed heap. As a result, most operations write to this buffer and do not need to cross the interop boundary thereby improving performance. This is especially significant in scenarios that involve many small I/O operations, such as parsing an XML document.

One of the benefits of using the .NET Framework’s stream projections is that if you use an AsStreamXxx method more than once on the same WinRT stream instance, you do not need to worry that different, disconnected buffers will be created, and data written to one buffer will not be visible in the other. The .NET Framework APIs ensure that every stream object has a unique adapter instance and all users share the same buffer.

While in most cases the default buffering offers a good compromise between performance and memory usage, there are some cases where you may want to tweak the size of your buffer to be different from the 16KB default. The AsStreamXxx methods offer overloads for that. For instance, if you know that you will be working with a very large file for an extended period of time, and that not many other buffered streams will be used at the same time, you can gain some additional performance by requesting a very large buffer for your stream. Conversely, in some network scenarios with low-latency requirements, you may want to ensure that no more bytes are read from the network than were explicitly requested by your application. In such cases, you can disable buffering altogether. If you specify a buffer size of zero bytes to the AsStreamXxx methods, no buffer object will be created.

# Passing Blocks of Data Between the CLR and WinRT

When possible, you should use the stream framework projections as discussed in the previous section, since they have pretty good performance characteristics. However, there may be times when you need to pass raw blocks of data between the CLR and WinRT components. For example, WinRT’s file and socket stream components require you to write and read raw blocks of data. Also, WinRT’s cryptography components encrypt and decrypt blocks of data, and bitmap pixels are maintained in raw blocks of data too.

In the .NET Framework, the usual way to obtain a block of data is either with a byte array (Byte[]) or with a stream (such as when using the MemoryStream class). Of course, byte array and MemoryStream objects can’t be passed to WinRT components directly. So, WinRT defines an IBuffer interface and objects that implement this interface represent raw blocks of data that can be passed to WinRT APIs. The WinRT IBuffer interface is defined like this:

```
```csharp
namespace Windows.Storage.Streams {
    public interface IBuffer {
        UInt32 Capacity { get; }       // Maximum size of the buffer (in bytes)
        UInt32 Length   { get; set; }  // Number of bytes currently in use by the buffer
    }
}
```
```