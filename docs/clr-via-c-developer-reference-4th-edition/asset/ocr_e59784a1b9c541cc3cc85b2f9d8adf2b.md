When you call the AsBuffer or GetWindowsRuntime methods in your code, these methods wrap the source object inside an object which implements the IBuffer interface. The CLR creates a CCW for it and passes it to the WinRT API. The WinRT API queries the IBufferAccess interface's Buffer to obtain a pointer to the underlying byte array, the array is pinned, and the address is returned to the WinRT API so it can access the data. The data is unpinned when the WinRT API internally calls COM's Release method on the IBufferAccess interface.

If you call a WinRT API that returns an IBuffer to you, the data itself is probably in native memory, and you'll need a access to this data from managed code. For this, we'll turn to some other extension methods defined by the WindowsRuntimeBufferClasses.

```
namespace System.Interop.WindowsRuntime {
    public static class WindowsRuntimeExtensions {
        public static Stream AsStream(IBuffer source);
        public static Byte[] ToArray(IBuffer source);
        public static Byte[] ToArray(IBuffer source, UInt32 sourceIndex, Int32 count);

        // Not shown: CopyTo method to transfer bytes between IBuffer and a Byte[]
        // Not shown: GetByte, IsSameData methods
    }
}
```

The AsStream method creates a Stream-driven object that wraps the source IBuffer. With this object, you can access the data in the IBuffer by calling Stream.Read, and similar methods. The ToArray method internally allocates all the bytes from the source IBuffer into the Byte[]; be aware that this extension method is potentially expensive in terms of memory consumption and CPU time.

The WindowsRuntimeBufferExtensions class also has several overloads of a CopyTo method that can copy bytes between an IBuffer and a Byte[]; It also has a GetByte method that retrieves a single byte at a time from an IBuffer and an IsSameData method that compares the contents of two IBuffer objects to see if their contents are identical. For most applications, it is unlikely that you will need to call all of these.

I'd like to point out that the .NET Framework defines a System.Interop.Runtime.WindowsRuntimeBuffer class that allows you to create an IBuffer whose bytes are in the managed heap. Similarly, there is a WinRT component called Windows.Storage.Streams.Buffer that allows you to create an IBuffer whose bytes are in the native heap. For most .NET developers, there should be no need to use either of these classes explicitly in your code.

# Defining WinRT Components in C#

So far in this chapter, I've been focusing on how to consume WinRT components from C#. and then these components can be used by C/C++, C#/Visual Basic, JavaScript, and potentially other languages too. Although this is possible to, we need to think about the scenarios where this actually makes sense. For example, it makes no