# Chapter 23: Platform Interoperability and Unsafe Code

```
{
    return virtualMemoryPointer.AllocatedPointer;
}

// SafeHandle abstract member
public override bool IsInvalid
{
    get {
        return _Disposed;
    }
}

// SafeHandle abstract member
protected override bool ReleaseHandle()
{
    if (!Disposed)
{
        _Disposed = true;
        GC.SuppressFinalize(this);
        VirtualMemoryManager.VirtualFree(_ProcessHandle, _AllocatedPointer, _MemorySize);
    }
    return true;
}
```

System.Runtime.InteropServices.SafeHandle includes the abstract members IsInvalid and ReleaseHandle(). You place your cleanup code in the latter; the former indicates this code has executed yet.

With VirtualMemoryPtr, you can allocate memory simply by instantiating the type and specifying the needed memory allocation.

# Calling External Functions

Once you declare the P/Invoke functions, you invoke them just as you would any other class member. The key, however, is that the imported DLL must be in the path, including the executable directory, so that it can be successfully loaded. Listing 23.6 and Listing 23.7 demonstrate this approach. However, they rely on some constants.