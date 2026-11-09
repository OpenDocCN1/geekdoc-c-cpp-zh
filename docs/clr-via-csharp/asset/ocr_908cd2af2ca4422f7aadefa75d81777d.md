```
```csharp
public abstract Boolean IsInvalid {
    get {
        // A derived class overrides this property.
        // The implementation should return true if the handle's value doesn't
        // represent a resource (this usually means that the handle is 0 or -1).
    }
}

// These three methods have to do with security and reference counting;
// I'll talk about them at the end of this section
public void DangerousAddRef(ref Boolean success) {...}
public IntPtr DangerousGetHandle() {...}
public void DangerousRelease() {...}
}
```
```

The first thing to notice about the **SafeHandle** class is that it is derived from **CriticalFinalizerObject**; this ensures it gets the CLR's special treatment. The second thing to notice is that the class is abstract; it is expected that another class will be derived from **SafeHandle**, and this class will override the protected constructor, the abstract method **ReleaseHandle**, and the abstract **IsInvalid** property **get** accessor method.

In Windows, most handles are invalid if they have a value of 0 or -1. The **Microsoft.Win32.SafeHandles** namespace contains another helper class called **SafeHandleZeroOrMinusOneIsInvalid**, which looks like this:

```
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
```

Again, you'll notice that the **SafeHandleZeroOrMinusOneIsInvalid** class is abstract, and therefore, another class must be derived from this one to override the protected constructor and the abstract method **ReleaseHandle**. The .NET Framework provides just a few public classes derived from **SafeHandleZeroOrMinusOneIsInvalid**, including **SafeFileHandle**, **SafeRegistryHandle**, **SafeWaitHandle**, and **SafeBuffer**. Here is what the **SafeFileHandle** class looks like:

```
```csharp
public sealed class SafeFileHandle : SafeHandleZeroOrMinusOneIsInvalid {
    public SafeFileHandle(IntPtr preexistingHandle, Boolean ownsHandle)
        : base(ownsHandle) {
        base.SetHandle(preexistingHandle);
    }
}
```
```