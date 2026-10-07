.Win32Exception() that is automatically initialized with the Win32 error data immediately following the P/Invoke call (see Listing 23.6).

# LISTING 23.6: Win32 Error Handling

```
public class VirtualMemoryManager
{
    [DllImport("kernel32.dll", SetLastError = true)]
    private static extern IntPtr VirtualAllocEx(
        IntPtr hProcess,
        IntPtr lpAddress,
        uint dwSize,
        AllocationType fAllocationType,
        uint lProtect);
    // ...
    [DllImport("kernel32.dll", SetLastError = true)]
    static extern bool VirtualProtectEx(
        IntPtr hProcess, IntPtr lpAddress,
        IntPtr dwSize, uint flNewProtect,
        ref uint lpflOldProtect);

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
    private enum MemoryFree
    {
        // ...
    }
    public static IntPtr AllocExecutionBlock(
        int size, IntPtr hProcess)
    {
        IntPtr codeBytesPtr;
        codeBytesPtr = VirtualAllocEx(
            hProcess, IntPtr.Zero,
```