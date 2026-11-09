```
```csharp
using System;
using System.Runtime.InteropServices;
using Microsoft.Win32.SafeHandles;

internal static class SomeType {
    [DllImport("Kernel32", CharSet=CharSet.Unicode, EntryPoint="CreateEvent")]
    // This prototype is not robust
    private static extern IntPtr CreateEventBad(
        IntPtr pSecurityAttributes, Boolean manualReset, Boolean initialState, String name);

    // This prototype is robust
    [DllImport("Kernel32", CharSet=CharSet.Unicode, EntryPoint="CreateEvent")]
    private static extern SafeWaitHandle CreateEventGood(
        IntPtr pSecurityAttributes, Boolean manualReset, Boolean initialState, String name);

    public static void SomeMethod() {
        IntPtr handle = CreateEventBad(IntPtr.Zero, false, false, null);
        SafeWaitHandle swh = CreateEventGood(IntPtr.Zero, false, false, null);
    }
}
```
```

You’ll notice that the CreateEventBad method is prototyped as returning an IntPtr, which will return the handle back to managed code; however, interoperating with native code this way is not robust. You see, after CreateEventBad is called (which creates the native event resource), it is possible that a ThreadAbortException could be thrown prior to the handle being assigned to the handle variable. In the rare cases when this could happen, the managed code would leak the native resource. The only way to get the event closed is to terminate the whole process.

The SafeHandle class fixes this potential resource leak. Notice that the CreateEventGood method is prototyped as returning a SafeWaitHandle (instead of an IntPtr). When CreateEventGood is called, the CLR calls the Win32 CreateEvent function. As the CreateEvent function returns to managed code, the CLR knows that SafeWaitHandle is derived from SafeHandle, causing the CLR to automatically construct an instance of the SafeWaitHandle class on the managed heap, passing in the handle value returned from CreateEvent. The constructing of the SafeWaitHandle object and the assignment of the handle happen in native code now, which cannot be interrupted by a ThreadAbortException. Now, it is impossible for managed code to leak this native resource. Eventually, the SafeWaitHandle object will be garbage collected and its Finalize method will be called, ensuring that the resource is released.

One last feature of SafeHandle-derived classes is that they prevent someone from trying to exploit a potential security hole. The problem is that one thread could be trying to use a native resource while another thread tries to free the resource. This could manifest itself as a handle-recycling exploit. The SafeHandle class prevents this security vulnerability by using reference counting. Internally, the SafeHandle class defines a private field that maintains a count. When a SafeHandle-derived object is set to a valid handle, the count is set to 1. Whenever a SafeHandle-derived object is passed as an argument to a native method, the CLR knows to automatically increment the counter. Likewise, when the native method returns to managed code, the CLR knows to decrement the counter. For example, you would prototype the Win32 SetEvent function as follows: