attributes as shown. The attribute GUID must have exactly the identifier as it is used here with the interface definition, because this is the identifier used with the definition of the COM interface:

```
using System;
using System.Runtime.InteropServices;

namespace Wrox.ProCSharp.Transactions
{
    [ComImport]
    [Guid("*79427A2B-F895-40e0-BE79-B57DC82ED231*")]
    [InterfaceType(ComInterfaceType.InterfaceIsIUnknown)]
    internal interface IKernelTransaction
    {
        void GetHandle(out SafeTransactionHandle ktmHandle);
    }
}
```

code snippet FileSystemTransactions/IKernelTransaction.cs

Finally, the class TransactedFile is the class that will be used by .NET applications. This class defines the method GetTransactedFileStream() that requires a filename as parameter and returns a System.IO.FileStream. The returned stream is a normal .NET stream; it just references a transacted file.

With the implementation, TransactionInterop.GetDtcTransaction() creates an interface pointer of the IKernelTransaction to the ambient transaction that is passed as an argument to GetDtcTransaction(). Using the interface IKernelTransaction, the handle of type SafeTransactionHandle is created. This handle is then passed to the wrapped API called NativeMethods.CreateFileTransacted(). With the returned file handle, a new FileStream instance is created and returned to the caller:

```
using System;
using System.IO;
using System.Security.Permissions;
using System.Transactions;
using Microsoft.Win32.SafeHandles;

namespace Wrox.ProCSharp.Transactions
{
    public static class TransactedFile
    {
        internal const short FILE_ATTRIBUTE_NORMAL = 0x80;
        internal const short INVALID_HANDLE_VALUE = -1;
        internal const uint GENERIC_READ = 0x80000000;
        internal const uint GENERIC_WRITE = 0x40000000;
        internal const uint CREATE_NEW = 1;
        internal const uint CREATE_ALWAYS = 2;
        internal const uint OPEN_EXISTING = 3;

        [FileIOPermission(SecurityAction.Demand, Unrestricted=true)]
        public static FileStream GetTransactedFileStream(string fileName)
        {
            IKernelTransaction ktx = (IKernelTransaction)
                TransactionInterop.GetDtcTransaction(Transaction.Current);

            SafeTransactionHandle txHandle;
            ktx.GetHandle(out txHandle);

            SafeFileHandle fileHandle = NativeMethods.CreateFileTransacted(
                fileName, GENERIC_WRITE, 0,
                IntPtr.Zero, CREATE_ALWAYS, FILE_ATTRIBUTE_NORMAL,
                IntPtr.Zero,
```