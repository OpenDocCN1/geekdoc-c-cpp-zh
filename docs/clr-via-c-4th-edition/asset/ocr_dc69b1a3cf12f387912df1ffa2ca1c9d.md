```
```csharp
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
```

The first thing to notice about the SafeHandle class is that it is derived from CriticalFinalizerObject, which is defined in the System.Runtime.ConstrainedExecution namespace. The CLR treats this class and classes derived from it in a very special manner. In particular, the CLR endows this class with three cool features:

+   - The first time an object of any CriticalFinalizerObject-derived type is constructed, the CLR immediately JIT-compiles all of the Finalize methods in the inheritance hierarchy. Compiling these methods upon object construction guarantees that the native resource will be released when the object is determined to be garbage. Without this eager compiling of the Finalize method, it would be possible to allocate the native resource and use it, but not to get rid of it. Under low memory conditions, the CLR might not be able to find enough memory to compile the Finalize method, which would prevent it from executing, causing the native resource to leak. Or the resource might not be freed if the Finalize method contained code that referred to a type in another assembly, and the CLR failed to locate this other assembly.
+   - The CLR calls the Finalize method of CriticalFinalizerObject-derived types after calling the Finalize methods of non-CriticalFinalizerObject-derived types. This ensures that managed resource classes that have a Finalize method can access CriticalFinalizerObject-derived objects within their Finalize methods successfully. For example, the FileStream class's Finalize method can flush data from a memory buffer to an underlying disk with confidence that the disk file has not been closed yet.
+   - The CLR calls the Finalize method of CriticalFinalizerObject-derived types if an AppDomain is rudely aborted by a host application (such as SQL Server or ASP.NET). This also is part of ensuring that the native resource is released even in a case in which a host application no longer trusts the managed code running inside of it.