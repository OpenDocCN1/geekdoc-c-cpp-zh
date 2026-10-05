+   3. In the Process tab, click **View**, choose **Select Columns**, and add the image path.

+   4. Click the **Process** column head to sort the processes. Notice the tree view disappears. (You can either display the tree view or sort by any of the columns.) Click the Process column column head again to sort from Z to A. Click it a third time to return the tree view.

+   5. Open the **View** menu and deselect **Show Processes from All Users** to show only your processes.

+   6. Click the **Options** menu, choose **Difference Highlight Duration**, and change the value to 3 seconds. Then launch a new process (anything). Notice that the new process is highlighted in green for 3 seconds. Exit this new process, and notice that the process is highlighted in red for 3 seconds before disappearing from the display. This can be useful for seeing processes created and exiting on your system.

+   7. Double-click a process and explore the various tabs available from the process properties display. (These will be referenced in various experiments throughout the book information showing is being explained.)

# Threads

A thread is an entity within a process that Windows schedules for execution. Without it, the process's program can't run. A thread includes the following essential components:

+   The contents of a set of CPU registers representing the state of the processor

+   Two stacks—one for the thread while executing in kernel mode and one for executing in user mode

+   A private storage area called *thread-local storage (TLS)* for use by subsystems, run-time libraries, and DLLs

+   A unique identifier called a *thread ID* (part of an internal structure called a *client ID*; process IDs and threads are generated out of the same name, so never overlap)

In addition, threads sometimes have their own security context, or token, which is often used by multithreaded server applications that impersonate the security context of the clients they serve.

The volatile registers, stacks, and private storage area are called the *context*. Because this information is different for each machine architecture that Windows runs on, by structure, necessity, is architecture-specific. The *GetThreadContext* function provides access to this architecture-specific information (called the CONTEXT block).

Because switching execution from one thread to another involves the kernel scheduler, it can be an expensive operation, especially if two threads are often switching between each other. Windows implements mechanisms to reduce this cost: *fibers* and *user-mode scheduling (UMS)*.