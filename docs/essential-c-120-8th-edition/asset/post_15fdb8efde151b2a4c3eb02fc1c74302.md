
# Chapter 23: Platform Interoperability and Unsafe Code

```cs
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

Once you declare the P/Invoke functions, you invoke them just as you would to any other class member. The key, however, is that the imported DLL must be in the path, including the executable directory, so that it can be successfully loaded. Listing 23.6 and Listing 23.7 demonstrate this approach. However, they rely on some constants.

Since flAllocationType and flProtect flags, it is a good practice to provide constants or enums for each. Instead of expecting the caller to define these constants or enums, encapsulation suggests that you provide them as part of the API declaration, as shown in Listing 23.8.

# LISTING 23.8: Encapsulating the APIs Together

```cssharp
public class VirtualMemoryManager {
    // ...

    // <summary>
    // The type of memory allocation. This parameter must
    // contain one of the following values.
    // </summary>
    [Flags]
    private enum AllocationType : uint {
        // <summary>
        // Allocates physical storage in memory or in the
        // paging file on disk for the specified reserved
        // memory pages. The function initializes the memory
        // to zero.
        // </summary>
        Commit = 0x1000,
        // <summary>
        // Reserves a range of the process's virtual address
        // space without allocating any actual physical
        // storage in memory or in the paging file on disk.
        // </summary>
        Reserve = 0x2000,
        // <summary>
        // Indicates that data in the memory range specified by
        // lpAddress and dwSize is no longer of interest.
        // pages should not be read or written to the
        // paging file. However, the memory block will be used
        // later, so it should not be decommitted.
        // value cannot be used with any other value.
        // </summary>
        Reset = 0x80000,
        // <summary>
        // Allocates physical memory with read-write access.
        // This value is solely for use with Address Windowing
        // Extensions (AWE) memory.
        // </summary>
        Physical = 0x400000,
    }
```

```cssharp
/// <summary>
/// Allocates memory at the highest possible address.
/// </summary>
TopDown = 0x100000,

/// <summary>
/// The memory protection for the region of pages to be
/// allocated.
/// </summary>
[Flags]
private enum ProtectionOptions : uint
{
/// <summary>
/// Enables execute access to the committed region of
/// pages. An attempt to read or write to the committed
/// region results in an access violation.
/// </summary>
Execute = 0x10,
/// <summary>
/// Enables execute and read access to the committed
/// region of pages. An attempt to write to the
/// committed region results in an access violation.
/// </summary>
PageExecuteRead = 0x20,
/// <summary>
/// Enables execute, read, and write access to the
/// committed region of pages.
/// </summary>
PageExecuteReadWrite = 0x40,
/// ...

/// <summary>
/// The type of freeFree operation.
/// </summary>
[Flags]
private enum MemoryType : uint
{
/// <summary>
/// Decomits the specified region of committed pages.
/// After the operation, the pages are in the reserved
/// state.
/// </summary>
Decommit = 0x4000,
/// <summary>
/// Releases the specified region of pages. After this
```

```cssharp
/// operation, the pages are in the free state.
/// </summary>
Release = 0x8000
}

// ...
}
```

The advantage of enums is that they group together the various values. Furthermore, they can limit the scope to nothing else besides these values.

# Simplifying API Calls with Wrappers

Whether they are focused on error handling, structs, or constant values, one goal of effective API developers is to provide a simplified API that wraps the underlying Win32 API. For example, Listing 23.9 overloads VirtualFreeEx() with public values that simplify the call.

Listing 23.9: Wrapping the Underlying API

```cssharp
public class VirtualMemoryManager
{
    //...

    [DllImport("kernel32.dll", SetLastError = true)]
    static extern bool VirtualFreeEx(
        IntPtr hProcess, IntPtr lpAddress,
        IntPtr dwSize, IntPtr dwFreeType);
    public static bool VirtualFreeEx(
        IntPtr hProcess, IntPtr lpAddress,
        IntPtr dwSize)
    {
        bool result = VirtualFreeEx(
            hProcess, lpAddress, dwSize,
            (IntPtr)MemoryFreeType.Commit);
        if (!result)
        {
            throw new System.ComponentModel.Win32Exception();
        }
        return result;
    }
    public static bool VirtualFreeEx(
        IntPtr lpAddress, IntPtr dwSize)
    }
```

# Chapter 23: Platform Interoperability and Unsafe Code

```cssharp
return VirtualFreeEx(
    GetCurrentProcessHandle(), lpAddress, dwSize);
}

[DllImport("kernel32", SetLastError = true)]
static extern IntPtr VirtualAlloc(
    IntPtr hProcess,
    IntPtr lpAddress,
    IntPtr dwSize,
    AllocationType flAllocationType,
    uint flProtect);

// ...
```

# Function Pointers Map to Delegates

One last key point related to P/Invoke is that function pointers in unmanaged code map to delegates in managed code. To use a timer, for example, you would provide a function pointer that the timer could call back on, once it expired. Specifically, you would pass a delegate instance that matches the signature of the callback.

C# 11 introduced an additional construct for storing pointers to functions. function pointers can provide a performance improvement over using delegates to invoke methods. These are only available in unsafe code which is covered later in this chapter.

# Guidelines

Given the idiosyncies of P/Invoke, there are several guidelines to aid in the process of writing code.

> Guidelines
- DO NOT unnecessarily replicate existing managed classes that already perform the function of the unmanaged API.
- DO declare extern methods as private or internal.
- DO provide public wrapper methods that use managed conventions such as structured exception handling, use of enums for special values, and so on.

# Pointers and Addresses

- DO simplify the wrapper methods by choosing default values for unnecessary parameters.

- DO use the SetLastErrorAttribute on Windows to turn APIs that use SetLastError error codes into methods that throw Win32Exception.

- DO extend SafeHandle or implement IDisposable and create a finalizer to ensure that unmanaged resources can be cleaned effectively.

- DO delegate types that match the signature of the desired method when an unmanaged API requires a function pointer.

- DO use ref parameters rather than pointer types when possible.
