
If a Finalize method throws an unhandled exception, then the process terminates; there is no way to catch this exception.

So, as you can see, there are a lot of caveats related to Finalize methods and they must be used with caution. Specifically, they are designed for releasing native resources. To simplify working with them, it is highly recommended that developers avoid overriding Object's Finalize method; instead, use helper classes that Microsoft now provides in the Framework Class Library (FCL). The helper classes override Finalize and add some special CLR magic I'll talk about as we go on. You will then derive your own classes from the helper classes and inherit the CLR magic.

If you are creating a managed type that wraps a native resource, you should first derive a class from a special base class called System.Runtime.InteropServices.SafeHandle, which looks like the following (I've added comments in the methods to indicate what they do).

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

    // You can explicitly release the resource by calling Dispose
    // This is the IDisposable interface's Dispose method
    public void Dispose() { Dispose(true); }

    // The default Dispose implementation (shown here) is exactly what you want.
    // Overriding this method is strongly discouraged.
    protected virtual void Dispose(Boolean disposing) {
        // The default implementation ignores the disposing argument.
        // If resource already released, return
        // If ownsHandle is false, return
        // Set flag indicating that this resource has been released
        // Call virtual ReleaseHandle method
        // Call GC.SuppressFinalize(this) to prevent Finalize from being called
        // If ReleaseHandle returned true, return
        // If we get here, fire ReleaseHandleFailed Managed Debugging Assistant (MDA)
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

    public abstract Boolean IsInvalid {
        // A derived class overrides this property.
        // The implementation should return true if the handle's value doesn't
        // represent a resource (this usually means that the handle is 0 or -1)
        get;
    }

    // These three methods have to do with security and reference counting;
    // I'll talk about them at the end of this section
    public void DangerousAddRef(ref Boolean success) {...}
    public IntPtr DangerousGetHandle() {...}
    public void DangerousRelease() {...}
}
```

The first thing to notice about the SafeHandle class is that it is derived from CriticalFinalizerObject, which is defined in the System.Runtime.ConstrainedExecution namespace. The CLR treats this class and classes derived from it in a very special manner. In particular, the CLR endows this class with three cool features:

- The first time an object of any CriticalFinalizerObject-derived type is constructed, the CLR immediately JIT-compiles all of the Finalize methods in the inheritance hierarchy. Compiling these methods upon object construction guarantees that the native resource will be released when the object is determined to be garbage. Without this eager compiling of the Finalize method, it would be possible to allocate the native resource and use it, but not to get rid of it. Under low memory conditions, the CLR might not be able to find enough memory to compile the Finalize method, which would prevent it from executing, causing the native resource to leak. Or the resource might not be freed if the Finalize method contained code that referred to a type in another assembly, and the CLR failed to locate this other assembly.
- The CLR calls the Finalize method of CriticalFinalizerObject-derived types after calling the Finalize methods of non-CriticalFinalizerObject-derived types. This ensures that managed resource classes that have a Finalize method can access CriticalFinalizerObject-derived objects within their Finalize methods successfully. For example, the FileStream class's Finalize method can flush data from a memory buffer to an underlying disk with confidence that the disk file has not been closed yet.
- The CLR calls the Finalize method of CriticalFinalizerObject-derived types if an AppDomain is rudely aborted by a host application (such as SQL Server or ASP.NET). This also is part of ensuring that the native resource is released even in a case in which a host application no longer trusts the managed code running inside of it.

The second thing to notice about SafeHandle is that the class is abstract; it is expected that another class will be derived from SafeHandle, and this class will provide a constructor that invokes the protected constructor, the abstract method ReleaseHandle, and the abstract IsInvalid property get accessor method.

Most native resources are manipulated with handles (32-bit values on a 32-bit system and 64-bit values on a 64-bit system). So the SafeHandle class defines a protected IntPtr field called handle. In Windows, most handles are invalid if they have a value of 0 or -1. The Microsoft.Win32.SafeHandles namespace contains another helper class called SafeHandleZeroOrMinusOneIsInvalid, which looks like this.

```csharp
public abstract class SafeHandleZeroOrMinusOneIsInvalid : SafeHandle {
    protected SafeHandleZeroOrMinusOneIsInvalid(Boolean ownsHandle)
        : base(IntPtr.Zero, ownsHandle) {
    }

    public override Boolean IsInvalid {
        get {
            if (base.handle == IntPtr.Zero) return true;
            if (base.handle == (IntPtr) (-1)) return true;
            return false;
        }
    }
}
```

Again, you'll notice that the SafeHandleZeroOrMinusOneIsInvalid class is abstract, and therefore, another class must be derived from this one to override the protected constructor and the abstract method ReleaseHandle. The .NET Framework provides just a few public classes derived from SafeHandleZeroOrMinusOneIsInvalid, including SafeFileHandle, SafeRegistryHandle, SafeWaitHandle, and SafeMemoryMappedViewHandle. Here is what the SafeFileHandle class looks like.

```csharp
public sealed class SafeFileHandle : SafeHandleZeroOrMinusOneIsInvalid {
    public SafeFileHandle(IntPtr preexistingHandle, Boolean ownsHandle)
        : base(ownsHandle) {
        base.SetHandle(preexistingHandle);
    }

    protected override Boolean ReleaseHandle() {
        // Tell Windows that we want the native resource closed.
        return Win32Native.CloseHandle(base.handle);
    }
}
```

The SafeWaitHandle class is implemented similarly to the SafeFileHandle class just shown. The only reason why there are different classes with similar implementations is to achieve type safety; the compiler won't let you use a file handle as an argument to a method that expects a wait handle, and vice versa. The SafeRegistryHandle class's ReleaseHandle method calls the Win32 RegCloseKey function.
