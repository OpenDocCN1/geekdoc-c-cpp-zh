# Chapter 23: Platform Interoperability and Unsafe Code

(IntPtr)size,
AllocationType.Reserve | AllocationType.Commit,
(uint)ProtectionOptions.PageExecuteReadWrite;

```
if (codeBytesPtr == IntPtr.Zero)
{
    throw new System.ComponentModel.Win32Exception();
}

uint lpfldOldProtect = 0;
if (!VirtualProtectEx(
    hProcess, codeBytesPtr,
    (IntPtr)size,
    (uint)ProtectionOptions.PageExecuteReadWrite,
    ref lpfldOldProtect))
{
    throw new System.ComponentModel.Win32Exception();
    return codeBytesPtr;
}

public static int AllocExecutionBlock(int size)
{
    return AllocExecutionBlock(
        size, GetCurrentProcessHandle());
}

// ...
```

This code enables developers to provide the custom error checking that each API uses while still reporting the error in a standard manner.

Listing 23.1 and Listing 23.3 declared the P/Invoke methods as internal or private. Except for the simplest of APIs, wrapping methods in wrappers that reduce the complexity of the P/Invoke API calls is a good guideline that increases API usability and moves toward object-oriented type structure. The AllocExecutionBlock() declaration in Listing 23.6 provides a good example of this approach.