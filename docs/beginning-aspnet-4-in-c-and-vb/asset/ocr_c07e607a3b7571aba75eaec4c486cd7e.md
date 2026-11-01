```
```csharp
namespace Wrox.ProcSharp.Interop
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
            if (!CreateHardLink(newFileName, oldFileName, IntPtr.Zero))
            {
                var ex = new Win32Exception(Marshal.GetLastWin32Error());
                throw new IOException(ex.Message, ex);
            }
        }

        public static class FileUtility
        {
            [FileIOPermission(SecurityAction.LinkDemand, Unrestricted = true)]
            public static void CreateHardLink(string oldFileName,
                string newFileName)
            {
                NativeMethods.CreateHardLink(oldFileName, newFileName);
            }
        }
    }
}
```
```

code snippet PInvokeSample/NativeMethods.cs

This class can now be used to create hard links very easily. If the file passed with the first argument of the program does not exist, you will get an exception with the message "The system cannot find the file specified." If the file exists, you get a new filename referencing the original file. You can easily verify this by changing text in one file; it will show up in the other file as well.

```
```csharp
using System;
using System.IO;

namespace Wrox.ProcSharp.Interop
{
    class Program
    {
        static void Main(string[] args)
        {
            if (args.Length != 2)
            {
                Console.WriteLine("usage: PInvokeSample " +
                    "existingfilename newfilename");
                return;
            }
            try
            {
                FileUtility.CreateHardLink(args[0], args[1]);
            }
            catch (IOException ex)
            {
```
```