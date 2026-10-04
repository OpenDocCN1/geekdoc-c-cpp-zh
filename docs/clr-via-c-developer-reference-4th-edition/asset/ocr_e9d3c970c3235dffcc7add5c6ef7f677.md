```
// Set flag indicating that this resource has been released
// GC.SuppressFinalize(this) to prevent Finalize from being called
}
```

```
public Boolean IsClosed
  {
    // Returns flag indicating whether resource was released
  }
```

```
public abstract Boolean IsValid
  // A derived class overrides this property.
  // The implementation should return true if the handle's value doesn't
  // represent a resource (usually means that the handle is 0 or -1)
  }
```

```
// These three methods have to do with security and reference counting;
// I'll talk about them at the end of this section
public void IntPtr DangerousAddRef(SafeHandle handle, bool success) {...}
public void DangerousRelease() {...}
```

The first thing to notice is the SafeHandle class that is derived from CriticalFinalizer-Object, which is defined in the System.Runtime.ConstrainedExecutionspace. The CLR treats this class and classes derived from it in a very special manner. In particular, the CLR enhances this class with three core features:

+   * The first time an object of any CriticalFinalizerObject-derived type is constructed, the CLR immediately-compiles all of the JIT methods in the inheritance hierarchy. Compiling these methods upon object construction guarantees that the native resource will be released when the object is determined to be garbage. Without this compiling of the Finalize method, it would be possible to allocate the native resource and use it, but not to get rid of it. Under low memory conditions, the CL might not be able to find enough memory to compile the Finalize method, which would prevent it from executing, causing the native resource leak. The resource might not be freed if the Finalize method contained code that referred to it in another assembly, and the CLR failed to locate this other.

+   * The CLR calls the Finalize method of CriticalFinalizerObject-derived types after calling the Finalize methods of non-CriticalFinalizerObject-derived types. This ensures that managed resource classes have a Finalize method can access Critical-FinalizerObject-derived objects within their Finalize methods successfully. For example, the FileStream class's Finalize method can flush data from a memory buffer to an under-lying disk if the file has not been closed.

+   * The CLR calls the Finalize method of CriticalFinalizerObject-derived types if an AppDomain is rudely aborted by a host application (such as SQL Server or ASP.NET). This is also part of ensuring that the native resource is released even in a case where a host application no longer trusts the managed code running inside of it.