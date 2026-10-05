# I/O cancellation for thread termination

The other scenario in which I/Os be cancelled when a thread exits, either directly or as a result of its process terminating (which causes the threads of the process to terminate). Because every thread has a list of IRPs associated with it Io, the I/O manager can walk this list, look for cancelable IRPs, and cancel them. Unlike C, which does not wait for an IRP to be cancelled before returning, the process manager will not allow thread termination to proceed until all I/Os have been cancelled. As a result, if a driver fails to cancel an IRP, the process and thread object will remain active until the system shuts down.

Note Only IRPs for which a driver sets a cancel routine are cancelable. The process manager waits until all I/Os associated with a thread are either cancelled or completed before deleting the thread.

# EXPERIMENT: Debugging an unkillable process

In this experiment, we use Myfault from Sysinternals to force an unkillable process by causing the Myfault.sys driver, which Myfault.exe, to indefinitely hold an IRP without having registered a cancel routine for it. (Notfault is covered in detail in the "Crash dump analysis" section of Chapter 15, "Crash dump analysis," in Part 2) Follow these steps:

+   1. Run Notfault.exe.
2. The Not My Fault dialog box appears. Click the Hang and choose Hang with IRP, as shown in the following screenshot. Click the Hang button.
3. You shouldn't see anything happening, and you should be able to click the Cancel button to quit the application. However, you should still see Myfault in Task Manager or Process Explorer. Attempts to terminate the process will fail because Windows will wait for the IRP to complete given that the Myfault driver doesn't register a cancel routine.

![](bbox=[0.239, 0.555, 0.483, 0.803])