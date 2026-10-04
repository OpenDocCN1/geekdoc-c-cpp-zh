How was Microsoft to solve this problem? Making garbage collector finalize objects in a specific order would have been impossible because objects could references to each other, and there would be no way for the garbage collector to correctly guess the order in which to finalize these objects. Here is Microsoft's solution: the StreamWriter type does not support the underlying File1Stream object. This means that if you forget to call Dispose on the StreamWriter object, data is guaranteed to be lost. Microsoft expects developers to see this consistent loss of data and fix the code by inserting an explicit call to Dispose.

> Note .NET Framework offers a feature called Managed Debugging Assistants (MDAs). When an MDA is enabled, the .NET Framework looks for common programmer errors and a corresponding MDA. In the debugger, it looks like an exception has been thrown. There is an MDA available to detect when StreamWriter object is collected without previously being explicitly disposed. To enable this MDA in Microsoft Visual Studio, open your project and start the Debug.Exceptions menu node and scroll to the bottom. You will see the StreamWriterBufferedDataList MDA. Select the Check box to have the Visual Studio debugger whenever a StreamWriter object's data is lost.

# Other GC Features for Use with Native Resources

Sometimes, a native resource consumes all of memory, the managed object wrapping that occupies very little memory. The quintessential example of this is the bitmap. A bitmap can occupy several megabytes of native memory, the managed object is tiny because it contains only an HBITMAP (a 4-byte or 8-byte value). From the CLR's perspective, a process could allocate hundreds of bitmaps (using little managed memory) before performing a collection. If the process is manipulating many bitmaps, the process's memory consumption will grow at a phenomenal rate. To fix this situation, the GC class offers the following two methods.

```
public static void AddMemoryPressure(Int64 bytesAllocated);
public static void RemoveMemoryPressure(Int64 bytesAllocated);
```

A class that wraps a potentially large native resource should use these methods to give the garbage collector a hint as to how much memory is really being consumed. The garbage collector monitors this pressure, and when it gets high, a garbage collection is forced.

There are some native resources that are fixed in number. For example, Windows formerly had a restriction that it could create only five device contexts. There had also a restriction on the number of files that an application could open. Again, from the CLR's perspective, a process could allocate hundreds of objects (that use little memory) before performing a collection. If the number of native resources is limited, attempting to use more than are available will typically result in exceptions being thrown.