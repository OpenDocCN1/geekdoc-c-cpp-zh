often used in referencing asynchronous I/O. Many Win32 calls accept an overlapped structure in order to perform asynchronous I/O. Overlapped structures have the following format:

```
typedef struct _OVERLAPPED
{
    DWORD Internal;
    DWORD InternalHigh;
    DWORD Offset;
    DWORD OffsetHigh;
    HANDLE hEvent;
} OVERLAPPED;
```

Notice that the overlapped structure maintains a handle to an event object used to signal I/O completion. The offset fields represent a 64-bit offset into the file object on which the I/O is performed. As we are working with messages in queues and not data streams, these fields are irrelevant. The internal fields are, well, internal. We're not supposed to use them, but from time to time, you will find the first 32 bits useful because they contain error codes during overlapped I/O failure.

So using events is as easy as creating an event, saving its handle in the overlapped structure, passing the structure to the Receive call, and then waiting for the I/O to complete. Events are created with the Win32 CreateEvent() call. For our purposes, a default event is fine. Therefore, we can supply the CreateEvent() call with all zero or NULL arguments.

Several routines can be used to wait for objects in Win32. Win32 synchronization objects have two states, signaled and nonsignaled. Waiting for a nonsignaled object will cause a thread to block. Signaled objects release waiting threads from their wait.

The following routines are the two most popular wait functions, enabling you to wait for one or many objects respectively:

+   - `WaitForSingleObject()`
+   - `WaitForMultipleObjects()`

Application code can cause events to become signaled and nonsignaled by calling the following two event API routines:

+   - `SetEvent()`
+   - `ResetEvent()`

Listing 25.12 demonstrates a simple application that uses events to synchronize MSMQ Receive operations. You'll note that I have created a Quit event to allow the main application thread to signal the worker thread to exit.