
## Parameter Data Types

Assuming the developer has identified the targeted DLL and exported function, the most difficult step is identified or creating the managed data types that correspond to the unmanaged types in the external function. Listing 20.2 shows a more difficult API.

```
LISTING 20.2: The VirtualAllocEx() API

LPVOID VirtualAllocEx(
 HANDLE hProcess,
 // The handle to a process. The
 // function allocates memory within
 // the virtual address space of this
 // process.
 LPVOID lpAddress,
 // The pointer that specifies a
 // desired starting address for the
 // region of pages that you want to
 // allocate. If lpAddress is NULL,
 // the function determines where to
 // allocate the region.
 SIZE_T dwSize,
 // The size of the region of memory to
 // allocate, in bytes. If lpAddress
 // is NULL, the function rounds dwSize
 // up to the next page boundary.
 DWORD flAllocationType,
 // The type of memory allocation.
 DWORD flProtect); // The type of memory allocation.
```

VirtualAllocEx() allocates virtual memory that the operating system specifically designates for execution or data. To call it, you also need corresponding definitions in managed code for each data type; although common in Win32 programming, HANDLE, LPVOID, SIZE_T, and DWORD are undefined in the CLI managed code. The declaration in C# for VirtualAllocEx(), therefore, is shown in Listing 20.3.

```
LISTING 20.3: Declaring the VirtualAllocEx() API in C#

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

- One particularly helpful resource for declaring Win32 APIs is www.pinvoke.net. This provides a great starting point for many APIs, helping to avoid some of the subtle problems that can arise when coding an external API call from scratch.

## Using ref Rather Than Pointers

Frequently, unmanaged code uses pointers for pass-by-reference parameters. In these cases, P/Invoke doesn’t require that you map the data type to a pointer in managed code. Instead, you map the corresponding parameter to ref (or out), depending on whether the parameter is in-out or just out. In Listing 20.4, lpflOldProtect, whose data type is PDWORD, is an example that returns the “pointer to a variable that receives the previous access protection of the first page in the specified region of pages.”

### Listing 20.4: Using ref and out Rather Than Pointers

```
class VirtualMemoryManager
{
    // ...
    [DllImport("kernel32.dll", SetLastError = true)]
    static extern bool VirtualProtectEx(
        IntPtr hProcess, IntPtr lpAddress,
        IntPtr dwSize, uint flNewProtect,
        ref uint lpflOldProtect);
}
```

In spite of the fact that lpflOldProtect is documented as [out] (even though the signature doesn’t enforce it), the description goes on to mention that the parameter must point to a valid variable and not NULL. The inconsistency is confusing, but common. The guideline is to use ref rather than out for P/Invoke type parameters since the callee can always ignore the data passed with ref, but the converse will not necessarily succeed.

The other parameters are virtually the same as VirtualAllocEx(), except that the lpAddress is the address returned from VirtualAllocEx(). In addition, flNewProtect specifies the exact type of memory protection: page execute, page read-only, and so on.

## Using StructLayoutAttribute for Sequential Layout

Some APIs involve types that have no corresponding managed type. To call these requires redeclaration of the type in managed code. You declare the unmanaged COLORREF struct, for example, in managed code (see Listing 20.5).

### LISTING 20.5: Declaring Types from Unmanaged Structs

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

Various Microsoft Windows color APIs use COLORREF to represent RGB colors (levels of red, green, and blue).

The key in this declaration is StructLayoutAttribute. By default, managed code can optimize the memory layouts of types, so layouts may not be sequential from one field to the next. To force sequential layouts so that a type maps directly and can be copied bit for bit (blitted) from managed to unmanaged code and vice versa, you add the StructLayoutAttribute with the LayoutKind.Sequential enum value. (This is also useful when writing data to and from filestreams where a sequential layout may be expected.)

Since the unmanaged (C++) definition for struct does not map to the C# definition, there is not a direct mapping of unmanaged struct to managed struct. Instead, developers should follow the usual C# guidelines about whether the type should behave like a value or a reference type, and whether the size is small (approximately less than 16 bytes).

## Error Handling

One inconvenient characteristic of Win32 API programming is the fact that it frequently reports errors in inconsistent ways. For example, some APIs return a value (0, 1, false, and so on) to indicate an error, and others set an out parameter in some way. Furthermore, the details of what went wrong require additional calls to the GetLastError() API and then an additional call to FormatMessage() to retrieve an error message corresponding to the error. In summary, Win32 error reporting in unmanaged code seldom occurs via exceptions.

Fortunately, the P/Invoke designers provided a mechanism for handling this. To enable this, given the SetLastError named parameter of the DllImport attribute is true, it is possible to instantiate a System.ComponentModel.Win32Exception() that is automatically initialized with the Win32 error data immediately following the P/Invoke call (see Listing 20.6).

### LISTING 20.6: Win32 Error Handling

```
class VirtualMemoryManager
{
    [DllImport("kernel32.dll", "", SetLastError = true)]
    private static extern IntPtr VirtualAllocEx(
        IntPtr hProcess,
        IntPtr lpAddress,
        IntPtr dwSize,
        AllocationType flAllocationType,
        uint flProtect);

    // ...

    [DllImport("kernel32.dll", SetLastError = true)]
    static extern bool VirtualProtectEx(
        IntPtr hProcess, IntPtr lpAddress,
        IntPtr dwSize, uint flNewProtect,
        ref uint lpflOldProtect);
}

[Flags]
private enum AllocationType : uint
{
    // ...
}

[Flags]
private enum ProtectionOptions
{
    // ...
}

[Flags]
private enum MemoryFreeType
{
    // ...
}

public static IntPtr AllocExecutionBlock(
    int size, IntPtr hProcess)
{
    IntPtr codeBytesPtr;
    codeBytesPtr = VirtualAllocEx(
        hProcess, IntPtr.Zero,
        (IntPtr)size,
        AllocationType.Reserve | AllocationType.Commit,
        (uint)(ProtectionOptions.PageExecuteReadWrite));
    if (codeBytesPtr == IntPtr.Zero)
    {
        throw new System.ComponentModel.Win32Exception();
    }

    uint lpflOldProtect = 0;
    if (!(VirtualProtectEx(
        hProcess, codeBytesPtr,
        (IntPtr)size,
        (uint)(ProtectionOptions.PageExecuteReadWrite),
        ref lpflOldProtect))
    {
        throw new System.ComponentModel.Win32Exception();
    }
}
