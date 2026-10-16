name of the existing file, and the second argument is the new file. This is similar to other classes in the framework, such as File.Copy. Because the third argument used to pass the security attributes for the new filename is not used with this implementation, the public method has just two parameters. The return type is changed as well. Instead of returning an error by returning the value false, an exception is thrown. In case of an error, the unmanaged method CreateHardLink sets the error number with the unmanaged API SetLastError. To read this value from .NET, the [DllImport] field SetLastError is set to true. Within the managed method CreateHardLink, the error number is read by calling Marshal.GetLastWin32Error. To create an error message from this number, the Win32Exception class from the namespace System.ComponentModel is used. This class accepts an error number with the constructor, and returns a localized error message. In case of an error, an exception of type IOException is thrown, which has an inner exception of type Win32Exception. The public method CreateHardLink has the FileIOPermission attribute applied to check whether the caller has the necessary permission. You can read more about .NET security in Chapter 24 (code file PInvokeSample/NativeMethods.cs).

```
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
            EntryPoint ="CreateHardLinkW", CharSet = CharSet.Unicode)]
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
                var ex = new
                Win32Exception(Marshal.GetLastWin32Error());
                throw new IOException(ex.Message, ex);
            }
        }
    }

    public static class FileUtility
    {
        [FileIOPermission(SecurityAction.LinkDemand, Unrestricted =
```