
*Finalization* is a mechanism offered by the CLR that allows an object to perform some graceful cleanup prior to the garbage collector reclaiming the object's memory. Any type that wraps a native resource, such as a file, network connection, socket, mutex, or other type, must support finalization. Basically, the type implements a method named **Finalize**. When the garbage collector determines that an object is garbage, it calls the object's **Finalize** method (if it exists). I think of it this way: Any type that implements the **Finalize** method is in effect stating that all of its objects want a last meal before they are killed.

Microsoft's C# team felt that **Finalize** methods were a special kind of method requiring special syntax in the programming language (similar to how C# requires special syntax to define a constructor). So, in C#, you must define a **Finalize** method by placing a tilde symbol (~) in front of the class name, as shown in the following code sample:

```
internal sealed class SomeType {
    // This is the Finalize method
    ~SomeType() {
        // The code here is inside the Finalize method
    }
}
```

If you were to compile this code and examine the resulting assembly with ILDasm.exe, you'd see that the C# compiler did, in fact, emit a **protected override** method named **Finalize** into the module's metadata. If you examined the **Finalize** method's IL code, you'd also see that the code inside the method's body is emitted into a **try** block, and that a call to **base.Finalize** is emitted into a **finally** block.

> **Important** If you're familiar with C++, you'll notice that the special syntax C# requires for defining a **Finalize** method looks just like the syntax you'd use to define a C++ destructor. In fact, the C# Programming Language Specification calls this method a *destructor*. However, a **Finalize** method doesn't work like an unmanaged C++ destructor at all, and this has caused a great deal of confusion for developers migrating from one language to another.
>
> The problem is that developers mistakenly believe that using the C# destructor syntax means that the type's objects will be deterministically destructed, just as they would be in C++. However, the CLR doesn't support deterministic destruction, preventing C# from providing this mechanism.

A **Finalize** method is usually implemented to call the Win32 **CloseHandle** function, passing in the handle of the native resource. The **FileStream** type defines a file handle field, which identifies the native resource. The **FileStream** type also defines a **Finalize** method, which internally calls **CloseHandle**, passing it the file handle field; this ensures that the native file handle is closed when the managed **FileStream** object is determined to be garbage. If a type that wraps a native resource fails to define a **Finalize** method, the native resource won't be closed and will cause a resource leak that will exist until the process terminates, at which time the operating system will reclaim the native resources.

## Guaranteed Finalization Using CriticalFinalizerObject Types

To make things simpler for developers, the `System.Runtime.ConstrainedExecution` namespace defines a `CriticalFinalizerObject` class that looks like this:

```
    public abstract class CriticalFinalizerObject {
        protected CriticalFinalizerObject() { /* there is no code in here */ }

        // This is the Finalize method
        ~CriticalFinalizerObject() { /* there is no code in here */ }
    }
```

I know that you're thinking that this class doesn't look too exciting, but the CLR treats this class and classes derived from it in a very special manner. In particular, the CLR endows this class with three cool features:

- The first time an object of any `CriticalFinalizerObject`-derived type is constructed, the CLR immediately JIT-compiles all of the `Finalize` methods in the inheritance hierarchy. Compiling these methods upon object construction guarantees that the native resource will be released when the object is determined to be garbage. Without this eager compiling of the `Finalize` method, it would be possible to allocate the native resource and use it, but not to get rid of it. Under low memory conditions, the CLR might not be able to find enough memory to compile the `Finalize` method, which would prevent it from executing, causing the native resource to leak. Or the resource might not be freed if the `Finalize` method contained code that referred to a type in another assembly, and the CLR failed to locate this other assembly.
- The CLR calls the `Finalize` method of `CriticalFinalizerObject`-derived types after calling the `Finalize` methods of non-`CriticalFinalizerObject`-derived types. This ensures that managed resource classes that have a `Finalize` method can access `CriticalFinalizerObject`-derived objects within their `Finalize` methods successfully. For example, the `FileStream` class's `Finalize` method can flush data from a memory buffer to an underlying disk with confidence that the disk file has not been closed yet.
- The CLR calls the `Finalize` method of `CriticalFinalizerObject`-derived types if an `AppDomain` is rudely aborted by a host application (such as Microsoft SQL Server or Microsoft ASP.NET). This also is part of ensuring that the native resource is released even in a case in which a host application no longer trusts the managed code running inside of it.

## SafeHandle and Its Derived Types

Now, Microsoft realizes that the most-used native resources are those resources provided by Windows. And Microsoft also realizes that most Windows resources are manipulated with handles (32-bit values on a 32-bit system and 64-bit values on a 64-bit system). Again, to make life easier and safer for developers, the **System.Runtime.InteropServices** namespace includes a class called **SafeHandle**, which looks like this (I've added comments in the methods to indicate what they do):

```csharp
public abstract class SafeHandle : CriticalFinalizerObject, IDisposable {
   // This is the handle to the native resource
   protected IntPtr handle;

   protected SafeHandle(IntPtr invalidHandleValue, Boolean ownsHandle) {
      this.handle = invalidHandleValue;
      // If ownsHandle is true, then the native resource is closed when
      // this SafeHandle-derived object is collected
   }

   protected void SetHandle(IntPtr handle) {
      this.handle = handle;
   }

   // You can explicitly release the resource by calling Dispose or Close
   public void Dispose() { Dispose(true); }
   public void Close() { Dispose(true); }

   // The default Dispose implementation (shown here) is exactly what you want.
   // Overriding this method is strongly discouraged.
   protected virtual void Dispose(Boolean disposing) {
      // The default implementation ignores the disposing argument.
      // If resource was already released, just return
      // If ownsHandle is false, return
      // Set flag indicating that this resource has been released
      // Call the virtual ReleaseHandle method
      // Call GC.SuppressFinalize(this) to prevent Finalize from being called
      // If ReleaseHandle returned true, return
      // Fire the ReleaseHandleFailed Managed Debugging Assistant (MDA)
   }

   // The default Finalize implementation (shown here) is exactly what you want.
   // Overriding this method is very strongly discouraged.
   ~SafeHandle() { Dispose(false); }

   // A derived class overrides this method to implement the code that releases the resource
   protected abstract Boolean ReleaseHandle();

   public void SetHandleAsInvalid() {
      // Set flag indicating that this resource has been released
      // Call GC.SuppressFinalize(this) to prevent Finalize from being called
   }

   public Boolean IsClosed {
      get {
         // Returns flag indicating whether resource was released
      }
   }
}
```
