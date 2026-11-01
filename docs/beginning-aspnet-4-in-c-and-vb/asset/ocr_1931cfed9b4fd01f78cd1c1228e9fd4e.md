```
SetHandle(preexistingHandle);
}
[ResourceExposure(ResourceScope.Machine)]
[ResourceConsumption(ResourceScope.Machine)]
protected override bool ReleaseHandle()
{
    return NativeMethods.CloseHandle(handle);
}
}
```

# code snippet FileSystemTransactions/SafeTransactionHandle.cs

All native methods used from .NET are defined with the class NativeMethods shown here. With the sample, the native APIs needed are CreateFileTransacted() and CloseHandle(), which are defined as static members of the class. The methods are declared extern because there is no C# implementation. Instead, the implementation is found in the native DLL as defined by the attribute DllImport. Both of these methods can be found in the native DLL Kernel32.dll. With the method declaration, the parameters defined with the Windows API call are mapped to .NET data types. The parameter txHandle represents a handle to a transaction and is of the previously defined type SafeTransactionHandle:

```
using System;
using System.Runtime.ConstrainedExecution;
using System.Runtime.InteropServices;
using System.Runtime.Versioning;
using Microsoft.Win32.SafeHandles;

namespace Wrox.ProCSharp.Transactions
{
    internal static class NativeMethods
    {
        [DllImport("Kernel32.dll", CallingConvention = CallingConvention.StdCall,
            CharSet = CharSet.Unicode)]
        internal static extern SafeFileHandle CreateFileTransacted(
            String lpFileName,
            uint dwDesiredAccess,
            uint dwShareMode,
            IntPtr lpSecurityAttributes,
            uint dwCreationDisposition,
            int dwFlagsAndAttributes,
            IntPtr hTemplateFile,
            SafeTransactionHandle txHandle,
            IntPtr miniVersion,
            IntPtr extendedParameter);

        [DllImport("Kernel32.dll", SetLastError = true)]
        [ResourceExposure(ResourceScope.Machine)]
        [ReliabilityContract(Consistency.WillNotCorruptState, Cer.Success)]
        [return: MarshalAs(UnmanagedType.Bool)]
        internal static extern bool CloseHandle(IntPtr handle);
    }
}
```

# code snippet FileSystemTransactions/NativeMethods.cs

The interface IKernelTransaction is used to get a transaction handle and pass it to the transacted Windows API calls. This is a COM interface and must be wrapped to .NET by using COM interop