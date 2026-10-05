# Stage 6: Starting execution of the initial thread

At this point, the process environment has been determined, resources for its threads to have been allocated, the process has a thread, and the Windows subsystem knows about the new process. Unless the caller specified the CREATE_SUSPENDED flag, the initial thread is now resumed so that it can start running and perform the remainder of the process-initialization work that occurs in the context of the new process (stage 7).

# Stage 7: Performing process initialization in the context of the new process

The new thread begins running the kernel-mode thread routine KiStartThread. KiStartThread lowers the IRQL from deferred procedure call (DPC) to APC level and then calls the system initial thread routine, PspUserThreadStartup. The user-specified thread start address is passed as a parameter to this routine. PspUserThreadStartup performs the following actions:

+   - It installs an exception chain on x86 architecture. (Other architectures work differently in this regard, see Chapter 8 in Part 2.)
- It lowers IRQL to PASSIVE_LEVEL (which is the only IRQL user code is allowed to run).
- It disables the ability to swap the process context at runtime.
- If the thread was killed on startup (for whatever reason), it's terminated and no further action is taken.
- It sets the locale ID and the ideal processor in the TEB, based on the information present in kernel-mode data structures, and then checks whether thread creation actually failed.
- It calls DbgCreateThread, which checks whether notifications are sent for the new process. If they weren't, and notifications are enabled, an image notification is sent first to the process and then for the image load of Ntdll.dll.

> Note This is done in this stage rather than when the images are first mapped because the process ID (which is required for the kernel calls) is not yet allocated at that time.

+   - Once these checks are completed, another check is performed to see whether the process is a debugger. If it is and debugger notifications have not been sent, then a create process message is sent through the debugger object (if one present) so that the process debug event (CREATE_PROCESS_DEBUG_INFO) can be sent to the appropriate debugger process. This is followed by a thread debug event and another debugger event for the image load of Ntdll.dll. DbgCreateThread then waits for a reply from the debugger (via the ContinueDebug function).