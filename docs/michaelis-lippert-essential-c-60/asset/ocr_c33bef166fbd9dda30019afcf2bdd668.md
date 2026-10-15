```
{
    return virtualMemoryPointer.AllocatedPointer;
}

// SafeHandle abstract member
public override bool IsInvalid
{
    get
    {
        return Disposed;
    }
}

// SafeHandle abstract member
protected override bool ReleaseHandle()
{
    if (!Disposed)
    {
        Disposed = true;
        GC.SuppressFinalize(this);
        VirtualMemoryManager.VirtualFreeEx(ProcessHandle,
            AllocatedPointer, MemorySize);
    }
    return true;
}
```

System.Runtime.InteropServices.SafeHandle includes the abstract members IsInvalid and ReleaseHandle(). You place your cleanup code in the latter; the former indicates whether this code has executed yet.

With VirtualMemoryPtr, you can allocate memory simply by instantiating the type and specifying the needed memory allocation.

# Calling External Functions

Once you declare the P/Invoke functions, you invoke them just as you would any other class member. The key, however, is that the imported DLL must be in the path, including the executable directory, so that it can be successfully loaded. Listing 20.6 and Listing 20.7 provide demonstrations of this approach. However, they rely on some constants.

Since flAllocationType and flProtect are flags, it is a good practice to provide constants or enums for each. Instead of expecting the caller to define these constants or enums, encapsulation suggests you provide them as part of the API declaration, as shown in Listing 20.8.