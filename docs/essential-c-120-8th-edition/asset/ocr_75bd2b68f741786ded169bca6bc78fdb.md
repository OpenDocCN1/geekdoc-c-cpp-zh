will vary depending on the processor. Therefore, instead of mapping types such as

# LISTING 23.3: Declaring the VirtualAllocEx() API in C#

```
using System;
using System.Runtime.InteropServices;
public class VirtualMemoryManager
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

HANDLE and LPVOID simply to ints, you need to map to System.IntPtr,
whose will vary depending on the processor memory layout. This example also uses an AllocationType enum, which we discuss in the section "Simplifying API Calls with Wrappers" later in this chapter.

An interesting point to note about Listing 23.3 is that IntPtr is useful for more
than just pointers—that is, it is useful for other things such as quantities. IntPtr does not mean just "pointer stored in an integer"; it also means "integer that is the size of a pointer." An IntPtr need not contain a pointer but simply needs to contain something the size of a pointer. Lots of things are the size of a pointer but are not actually pointers.

# Native sized integers

C# 9.0 introduced new contextual keywords, nint and nunit that represent native machine-size integers. These are both integers that will either be 32 or 64 bits depending on the running process. Internally nint and nunit are implemented with System.IntPtr and System.UIntPtr. In C# 11 these are updated to simply be aliases for the types they represent.