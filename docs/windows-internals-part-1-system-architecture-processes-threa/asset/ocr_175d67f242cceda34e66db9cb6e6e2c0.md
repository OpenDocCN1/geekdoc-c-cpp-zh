A final note about I/O completion: the asynchronous I/O functions ReadFileEx and WriteFileEx allow a caller to supply a callback function as a parameter. If the caller does, the I/O manager queues a user mode APC to the caller's APC queue as the last step of I/O completion. This feature allows a caller to specify a subroutine to be called when an I/O request is completed or canceled. User-mode APC completion routines execute in the context of the requesting thread and are delivered only when the thread enters an alert wait state (by calling functions such as SleepEx, WaitForSingleObjectEx, or WaitForMultipleObjects).

# User address space buffer access

As shown in Figure 6-14, there are four driver functions involved in processing an IRP. Some of these routines may need to access the buffer in user space provided by the client application. When an application or device driver invokes an IRP using the NtReadFile, NtWriteFile, or NtDeviceIoControl systems (or the Windows API functions corresponding to these services, which are ReadFile, WriteFile, and DeviceIoControl), the pointer to the user's buffer is provided in the UserBuffer member of the IRP. However, accessing this buffer directly can only be done in the requesting thread context (the client process address is visible) and in IRQL 0 (paging can be handled normally).

As discussed in the previous section, the dispatch routine meets the criteria of running in the requesting thread context and in IRQL 0. Even this is not always the case—it's possible for an upper filter to hold on the IRP and not pass it down immediately, possibly passing it later on using a different thread, or even when the CPU IRQL is 2 or higher.

The other functions (Start I/O, ISR, DCP) clearly run on an arbitrary thread (could be any thread), and with IRQL 2 (DIRQL for the ISR). Accessing the user's buffer directly from any of these routines is mostly fatal. Here's why:

+   - Because the IRQL is 2 or higher, paging is not allowed. Since the user's buffer (or part of it) may be paged out, accessing the non-resident memory would crash the system.
- Because the thread executing these functions could be any thread, and thus a random process address space would be visible, the original user's address has no meaning and would likely lead to an access violation, or worse—accessing data from some random process (the parent process of whatever was running at the time).

Clearly, there must be a safe way to access the user's buffer in any of these routines. The I/O manager provides two options, for it does the heavy lifting. These are known as Buffered I/O and Direct I/O. A third option, which is not really an option, is called Neither I/O, in which the I/O manager does nothing special and lets the driver handle the problem on its own.

A driver selects the method in the following way:

+   - For read and write operations (IRP_MJ_READ, IRP_MJ_WRITE), it sets the Flags member with an boolean operation so not to disturb other flags of the device object (DEVICE_OBJECT) to DO_BUFFERED_IO (for buffered I/O) or DO_DIRECT_IO (for direct I/O). If neither flag is set, neither I/O is implied. (DO is short for device object).