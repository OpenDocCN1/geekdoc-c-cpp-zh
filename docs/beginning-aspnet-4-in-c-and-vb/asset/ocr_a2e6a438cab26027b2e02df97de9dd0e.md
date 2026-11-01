| DLLIMPORT PROPERTY OR FIELD | DESCRIPTION |
|---|---|
| EntryPoint | You can give the C# declaration of the function a different name than it has with the unmanaged library. The name of the method in the unmanaged library is defined in the field EntryPoint. |
| CallingConvention | Depending on the compiler or compiler settings that were used to compile the unmanaged function, different calling conventions can be used. The calling convention defines how the parameters are dealt with and where to put them on the stack. You can define the calling convention by setting an enumerable value. The Windows API usually uses the StdCall calling convention on the Windows operating system, and it uses the Cdecl calling convention on Windows CE. Setting the value to CallingConvention.Winapi works for the Windows API in both the Windows and the Windows CE environments. |
| CharSet | String parameters can be either ANSI or Unicode. With the CharSet setting, you can define how strings are managed. Possible values that are defined with the CharSet enumeration are Ansi, Unicode, and Auto. CharSet.Auto uses Unicode on the Windows NT platform, and ANSI on Windows 98 and Windows ME. |
| SetLastError | If the unmanaged function sets an error by using the Windows API SetLastError, you can set the SetLastError field to true. This way, you can read the error number afterward by using Marshal.GetLastWin32Error(). |

To make the CreateHardLink() method easier to use from a .NET environment, you should follow these guidelines:

+   - Create an internal class named NativeMethods that wraps the platform invoke method calls.
+   - Create a public class to offer the native method functionality to .NET applications.
+   - Use security attributes to mark the required security.

In the sample code, the public method CreateHardLink() in the class FileUtility is the method that can be used by .NET applications. This method has the filename arguments reversed compared to the native Windows API method CreateHardLink(). The first argument is the name of the existing file, and the second argument is the name of the new file. This is similar to other classes in the Framework; for example, File.Copy(). Because the third argument used to pass the security attributes for the new filename is not used with this implementation, the public method has just two parameters. The return type is changed as well. Instead of returning an error by returning the value false, an exception is thrown. In case of an error, the unmanaged method CreateHardLink() sets the error number with the unmanaged API SetLastError(). To read this value from .NET, the [DllImport] field SetLastError is set to true. Within the managed method CreateHardLink(), the error number is read by calling Marshal.GetLastWin32Error(). To create an error message from this number, the Win32Exception class from the namespace System.ComponentModel is used. This class accepts an error number with the constructor, and returns a localized error message. In case of an error, an exception of type IOException is thrown, which has an inner exception of type Win32Exception. The public method CreateHardLink() has the FileIOPermission attribute applied to check if the caller has the necessary permission. You can read more about .NET security in Chapter 21, “Security.”

```
using System;
using System.ComponentModel;
using System.IO;
using System.Runtime.InteropServices;
using System.Security;
using System.Security.Permissions;
```