
## LISTING 20.1: Declaring an External Method

```
using System;
using System.Runtime.InteropServices;
class VirtualMemoryManager
{
    [DllImport("kernel32.dll", EntryPoint="GetCurrentProcess")]
    internal static extern IntPtr GetCurrentProcessHandle();
}
```

In this case, the class is VirtualMemoryManager, because it will contain functions associated with managing memory. (This particular function is available directly off the System.Diagnostics.Processor class, so there is no need to declare it in real code.) Note that the method returns an IntPtr; this type is explained in the next section.

The extern methods never include any body and are (almost) always static. Instead of a method body, the DllImport attribute, which accompanies the method declaration, points to the implementation. At a minimum, the attribute needs the name of the DLL that defines the function. The runtime determines the function name from the method name, although you can override this default using the EntryPoint named parameter to provide the function name. (The .NET platform will automatically attempt calls to the Unicode [...]W or ASCII [...]A API version.)

In this case, the external function, GetCurrentProcess(), retrieves a pseudohandle for the current process that you will use in the call for virtual memory allocation. Here’s the unmanaged declaration:

```
HANDLE GetCurrentProcess();
```

## Parameter Data Types

Assuming the developer has identified the targeted DLL and exported function, the most difficult step is identifying or creating the managed data types that correspond to the unmanaged types in the external function.¹ Listing 20.2 shows a more difficult API.

## LISTING 20.2: The VirtualAllocEx() API

```
LPVOID VirtualAllocEx(
    HANDLE hProcess,    // The handle to a process. The
```

> 1. One particularly helpful resource for declaring Win32 APIs is www.pinvoke.net. It provides a great starting point for many APIs, helping you avoid some of the subtle problems that can arise when coding an external API call from scratch.

// function allocates memory within
// the virtual address space of this
// process.
LPVOID lpAddress, // The pointer that specifies a
// desired starting address for the
// region of pages that you want to
// allocate. If lpAddress is NULL,
// the function determines where to
// allocate the region.
SIZE_T dwSize, // The size of the region of memory to
// allocate, in bytes. If lpAddress
// is NULL, the function rounds dwSize
// up to the next page boundary.
DWORD flAllocationType, // The type of memory allocation.
DWORD flProtect); // The type of memory allocation.

VirtualAllocEx() allocates virtual memory that the operating system specifically designates for execution or data. To call it, you need corresponding definitions in managed code for each data type; although common in Win32 programming, HANDLE, LPVOID, SIZE_T, and DWORD are undefined in the CLI managed code. The declaration in C# for VirtualAllocEx(), therefore, is shown in Listing 20.3.

## LISTING 20.3: Declaring the VirtualAllocEx() API in C#

```
using System;
using System.Runtime.InteropServices;
class VirtualMemoryManager
{
    [DllImport("kernel32.dll")]
    internal static extern IntPtr GetCurrentProcess();

    [DllImport("kernel32.dll", SetLastError = true)]
    private static extern IntPtr VirtualAllocEx(
        IntPtr hProcess,
        IntPtr lpAddress,
        IntPtr dwSize,
        AllocationType flAllocationType,
        uint flProtect);
}
```

One distinct characteristic of managed code is that primitive data types such as int do not change their size based on the processor. Whether the processor is 16, 32, or 64 bits, int is always 32 bits. In unmanaged code, however, memory pointers will vary depending on the processor. Therefore, instead of mapping types such as HANDLE and LPVOID simply to ints, you need to map to System.IntPtr, whose size will vary depending on the

addition, flNewProtect specifies the exact type of memory protection: page execute, page read-only, and so on.

## Using StructLayoutAttribute for Sequential Layout

Some APIs involve types that have no corresponding managed type. Calling these types requires redeclaration of the type in managed code. You declare the unmanaged COLORREF struct, for example, in managed code (see Listing 20.5).

## LISTING 20.5: Declaring Types from Unmanaged Structs

```
[StructLayout(LayoutKind.Sequential)]
struct ColorRef
{
    public byte Red;
    public byte Green;
    public byte Blue;
    // Turn off warning about not accessing Unused.
    #pragma warning disable 414
    private byte Unused;
    #pragma warning restore 414

    public ColorRef(byte red, byte green, byte blue)
    {
        Blue = blue;
        Green = green;
        Red = red;
        Unused = 0;
    }
}
```

Various Microsoft Windows color APIs use COLORREF to represent RGB colors (that is, levels of red, green, and blue).

The key in this declaration is StructLayoutAttribute. By default, managed code can optimize the memory layouts of types, so layouts may not be sequential from one field to the next. To force sequential layouts so that a type maps directly and can be copied bit for bit (blitted) from managed to unmanaged code, and vice versa, you add the StructLayoutAttribute with the LayoutKind.Sequential enum value. (This is also useful when writing data to and from filestreams where a sequential layout may be expected.)

Since the unmanaged (C++) definition for struct does not map to the C# definition, there is not a direct mapping of unmanaged struct to managed struct. Instead, developers should follow the usual C# guidelines

```
{  // ... }
[Flags]
private enum MemoryFreeType
{  // ... }
public static IntPtr AllocExecutionBlock(
    int size, IntPtr hProcess)
{
    IntPtr codeBytesPtr;
    codeBytesPtr = VirtualAllocEx(
        hProcess, IntPtr.Zero,
        (IntPtr)size,
        AllocationType.Reserve | AllocationType.Commit,
        (uint)ProtectionOptions.PageExecuteReadWrite);

    if (codeBytesPtr == IntPtr.Zero)
    {
        throw new System.ComponentModel.Win32Exception();
    }

    uint lpflOldProtect = 0;
    if (!VirtualProtectEx(
        hProcess, codeBytesPtr,
        (IntPtr)size,
        (uint)ProtectionOptions.PageExecuteReadWrite,
        ref lpflOldProtect))
    {
        throw new System.ComponentModel.Win32Exception();
    }
    return codeBytesPtr;
}
public static IntPtr AllocExecutionBlock(int size)
{
    return AllocExecutionBlock(
        size, GetCurrentProcessHandle());
}
```

This code enables developers to provide the custom error checking that each API uses while still reporting the error in a standard manner.

Listing 20.1 and Listing 20.3 declared the P/Invoke methods as internal or private. Except for the simplest of APIs, wrapping methods in public wrappers that reduce the complexity of the P/Invoke API calls is a good guideline that increases API usability and moves toward object-oriented

type structure. The AllocExecutionBlock() declaration in Listing 20.6 provides a good example of this approach.

## Guidelines

- DO create public managed wrappers around unmanaged methods that use the conventions of managed code, such as structured exception handling.

## Using SafeHandle

Frequently, P/Invoke involves a resource, such as a window handle, that code needs to clean up after using. Instead of requiring developers to remember this step is necessary and manually code it each time, it is helpful to provide a class that implements IDisposable and a finalizer. In Listing 20.7, for example, the address returned after VirtualAllocEx() and VirtualProtectEx() requires a follow-up call to VirtualFreeEx(). To provide built-in support for this process, you define a VirtualMemoryPtr class that derives from System.Runtime.InteropServices.SafeHandle.

## LISTING 20.7: Managed Resources Using SafeHandle

```
public class VirtualMemoryPtr :
    System.Runtime.InteropServices.SafeHandle
{
    public VirtualMemoryPtr(int memorySize) :
        base(IntPtr.Zero, true)
    {
        ProcessHandle =
            VirtualMemoryManager.GetCurrentProcessHandle();
        MemorySize = (IntPtr)memorySize;
        AllocatedPointer =
            VirtualMemoryManager.AllocExecutionBlock(
                memorySize, ProcessHandle);
        Disposed = false;
    }

    public readonly IntPtr AllocatedPointer;
    readonly IntPtr ProcessHandle;
    readonly IntPtr MemorySize;
    bool Disposed;

    public static implicit operator IntPtr(
        VirtualMemoryPtr virtualMemoryPointer)
```
