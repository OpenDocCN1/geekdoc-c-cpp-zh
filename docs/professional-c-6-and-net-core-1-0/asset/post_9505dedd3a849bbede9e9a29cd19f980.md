
```
Element 0 = 0
Element 1 = 1
Element 2 = 4
Element 3 = 9
Element 4 = 16
Element 5 = 25
Element 6 = 36
Element 7 = 49
Element 8 = 64
Element 9 = 81
Element 10 = 100
Element 11 = 121
Element 12 = 144
Element 13 = 169
Element 14 = 196
```

## Platform Invoke

Not all the features of Windows API calls are available from the .NET Framework. This is true not only for old Windows API calls but also for very new features from Windows 10 or Windows Server 2016. Maybe you’ve written some DLLs that export unmanaged methods and you would like to use them from C# as well.

To reuse an unmanaged library that doesn’t contain COM objects—it contains only exported functions—you can use Platform Invoke (P/Invoke). With P/Invoke, the CLR loads the DLL that includes the function that should be called and marshals the parameters.

To use the unmanaged function, first you have to determine the name of the function as it is exported. You can do this by using the `dumpbin` tool with the `/exports` option.

For example, the command

```
dumpbin /exports c:\windows\system32\kernel32.dll | more
```

lists all exported functions from the DLL `kernel32.dll`. In the example, you use the `CreateHardLink` Windows API function to create a hard link to an existing file. With this API call, you can have several filenames that reference the same file as long as the filenames are on one hard disk only. This API call is not available from .NET Framework 4.5.1, so you must use platform invoke.

To call a native function, you have to define a C# external method with the same number of arguments, and the argument types that are defined with the unmanaged method must have matching types in managed code.

The Windows API call `CreateHardLink` has this definition in C++:

```
BOOL CreateHardLink(
    LPCTSTR lpFileName,
    LPCTSTR lpExistingFileName,
    LPSECURITY_ATTRIBUTES lpSecurityAttributes);
```

This definition must be mapped to .NET data types. The return type is a BOOL in unmanaged code; this simply maps to the bool data type. LPCTSTR defines a long pointer to a const string. The Windows API uses the Hungarian naming convention for the data type. LP is a long pointer, C is a const, and STR is a null-terminated string. The T marks the type as a generic type, and the type is resolved to either LPCSTR (an ANSI string) or LPWSTR (a wide Unicode string), depending on the compiler’s settings to 32 or 64 bit. C strings map to the .NET type String. LPSECURITY_ATTRIBUTES, which is a long pointer to a struct of type SECURITY_ATTRIBUTES. Because you can pass NULL to this argument, mapping this type to IntPtr is okay. The C# declaration of this method must be marked with the extern modifier because there’s no implementation of this method within the C# code. Instead, the method implementation is in the DLL kernel32.dll, which is referenced with the attribute [DllImport]. The return type of the .NET declaration CreateHardLink is of type bool, and the native method CreateHardLink returns a BOOL, so some additional clarification is useful. Because there are different Boolean data types with C++ (for example, the native bool and the Windows-defined BOOL, which have different values), the attribute [MarshalAs] specifies to what native type the .NET type bool should map:

```
[DllImport("kernel32.dll", SetLastError = true, EntryPoint = "CreateHardLinkW", CharSet = CharSet.Unicode)]
[return: MarshalAs(UnmanagedType.Bool)]
public static extern bool CreateHardLink(string newFileName, string existingFileName, IntPtr securityAttributes);
```

> NOTE The website http://www.pinvoke.net is very helpful with the conversion from native to managed code.

The settings that you can specify with the attribute [DllImport] are listed in the following table.

| DllImport Property or Field | Description |
| --- | --- |
| EntryPoint | You can give the C# declaration of the function a different name than the one it has with the unmanaged library. The name of the method in the unmanaged library is defined in the field EntryPoint. |
| CallingConvention | Depending on the compiler or compiler settings that were used to compile the unmanaged function, you can use different calling conventions. The calling convention defines how the parameters are handled and where to put them on the stack. You can define the calling convention by setting an enumerated value. The Windows API usually uses the StdCall calling convention on the Windows operating system, and it uses the Cdecl calling convention on Windows CE. Setting the value to CallingConvention.Winapi works for the Windows API in both the Windows and the Windows CE environments. |
| CharSet | String parameters can be either ANSI or Unicode. With the CharSet setting, you can define how strings are managed. Possible values that are defined with the CharSet enumeration are Ansi, Unicode, and Auto. CharSet.Auto uses Unicode on the Windows NT platform, and ANSI on Microsoft's older operating systems. |
| SetLastError | If the unmanaged function sets an error by using the Windows API SetLastError, you can set the SetLastError field to true. This way, you can read the error number afterward by using Marshal.GetLastWin32Error. |

To make the CreateHardLink method easier to use from a .NET environment, you should follow these guidelines:

- Create an internal class named NativeMethods that wraps the platform invoke method calls.
- Create a public class to offer the native method functionality to .NET applications.
- Use security attributes to mark the required security.

In the following example, the public method CreateHardLink in the class FileUtility is the method that can be used by .NET applications. This method has the filename arguments reversed compared to the native Windows API method CreateHardLink. The first argument is the name of the existing file, and the second argument is the new file. This is similar to other classes in the framework, such as File.Copy. Because the third argument used to pass the security attributes for the new filename is not used with this implementation, the public method has just two parameters. The return type is changed as well. Instead of returning an error by returning the value false, an exception is thrown. In case of an error, the unmanaged method CreateHardLink sets the error number with the unmanaged API SetLastError. To read this value from .NET, the [DllImport] field SetLastError is set to true. Within the managed method CreateHardLink, the error number is read by calling Marshal.GetLastWin32Error. To create an error message from this number, the Win32Exception class from the namespace System.ComponentModel is used. This class accepts an error number with the constructor, and returns a localized error message. In case of an error, an exception of type IOException is thrown, which has an inner exception of type Win32Exception. The public method CreateHardLink has the FileIOPermission attribute applied to check whether the caller has the necessary permission. You can read more about .NET security in Chapter 24 (code file PInvokeSample/NativeMethods.cs).

```csharp
using System;
using System.ComponentModel;
using System.IO;
using System.Runtime.InteropServices;
using System.Security;
using System.Security.Permissions;

namespace Wrox.ProCSharp.Interop
{
    [SecurityCritical]
    internal static class NativeMethods
    {
        [DllImport("kernel32.dll", SetLastError = true,
            EntryPoint = "CreateHardLinkW", CharSet = CharSet.Unicode)]
        [return: MarshalAs(UnmanagedType.Bool)]
        private static extern bool CreateHardLink(
            [In, MarshalAs(UnmanagedType.LPWStr)] string newFileName,
            [In, MarshalAs(UnmanagedType.LPWStr)] string existingFileName,
            IntPtr securityAttributes);

        internal static void CreateHardLink(string oldFileName,
            string newFileName)
        {
            if (!CreateHardLink(newFileName, oldFileName,
            IntPtr.Zero))
            {
                var ex = new Win32Exception(Marshal.GetLastWin32Error());
                throw new IOException(ex.Message, ex);
            }
        }
    }

    public static class FileUtility
    {
        [FileIOPermission(SecurityAction.LinkDemand, Unrestricted =
```
