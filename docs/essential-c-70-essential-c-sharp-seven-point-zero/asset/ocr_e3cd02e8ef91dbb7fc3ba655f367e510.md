```
public readonly IntPtr AllocatedPointer;
readonly IntPtr ProcessHandle;
readonly IntPtr MemorySize;
bool Disposed;
public static implicit operator IntPtr(
VirtualMemoryPtr virtualMemoryPointer)
{
return virtualMemoryPointer.AllocatedPointer;
}
// SafeHandle abstract member
public override bool IsValid
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

System.Runtime.InteropServices.SafeHandle includes the abstract members IsValid and ReleaseHandle(). You place your cleanup code in the latter; the former indicates whether this code has executed yet. With VirtualMemoryPtr, you can allocate memory simply by instantiating the type and specifying the needed memory allocation.

# Calling External Functions

Once you declare the P/Invoke functions, you invoke them just as you would any other class member. The key, however, is that the imported DLL must be in the path, including the executable directory, so that it can be successfully loaded. Listings 21.6 and 21.7 demonstrate this approach. However, they rely on some constants.