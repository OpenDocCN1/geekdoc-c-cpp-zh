selected real-time statistics. For an explanation of a particular counter, select the desired counter and then select the Show Description check box.

Another tool for analyzing the memory and performance of your application is PerfView. This tool can collect Event Tracing for Windows (ETW) logs and process them. The best way to acquire this tool is to search the web for PerfView. Finally, you should look into the SOS Debugging Extension (SOS.dll), which can offer great assistance when debugging memory problems and other CLR problems. For memory-related issues, the SOS Debugging Extension allows you to see how much memory is allocated within the process to the managed heap, displays all objects registered for finalization in the finalization queue, displays the entries in the GCHandle table per AppDomain or for the entire process, shows that there are keeping an object alive in the heap, and

# Working with Types Requiring Special Cleanup

At this point, you should have a basic understanding of garbage collection and the managed heap, including how the collector reclaims an object’s memory. Fortunately for us, most types need only memory over. However, some types require more than just memory to be useful; some types require the use of a native resource in addition to memory.

The System.IO.FileStream type, for example, needs to open a file (a native resource) and store its handle. The then’s Read and Write methods use this to manipulate the file. Similarly, the System.Threading.Mutex type opens a Windows kernel object (a native resource) and stores it, using it when the Mutex’s methods are called.

If you wrapping a native resource GC could, the GC will reclaim the memory used by the object in the managed heap; but the native resource, which the GC doesn’t know anything about, will be leaked. This is clearly not desirable, so the CLR offers a mechanism called finalization. Finalization allows you to execute code after the object has been determined to be garbage before the object’s memory is reclaimed from the managed heap. All types that wrap a native resource—such as a file, network connection, socket, or mutex—support finalization. When the CLR determines that one of these is no longer reachable, the GC gets itself finalized, releasing the native resource it wraps, and then, the GC will reclaim the object from the managed heap.

System.Object, the base of everything, defines a protected and virtual method Finalize. When the garbage collector determines that an object is garbage, it calls the object’s Finalize (if it is overridden). Microsoft’s C# team felt Finalize methods were a special kind of method requiring special syntax in the programming language (similar to how C# requires special syntax to define a constructor). So, in C#, you must define a Finalize method by placing a tilde~) in front of the class name, as shown in the following code sample.

```
internal sealed class SomeType {
// This is the Finalize method
  ~SomeType() {
    // The code is inside the Finalize method
  }
}
```