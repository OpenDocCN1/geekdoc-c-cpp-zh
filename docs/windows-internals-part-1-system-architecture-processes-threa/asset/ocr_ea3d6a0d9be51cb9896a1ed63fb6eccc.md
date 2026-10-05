# I/O priority inversion avoidance

Avoid I/O priority inversion

If an ERESOURCE is acquired by a thread with low I/O priority, and there are currently waits on the ERESOURCE with normal or higher priority, the current thread is temporarily boosted to normal I/O priority using the PsBoostThreadTo API, which increments the IoBoostCount in the ETHREAD structure. It also notifies Autoboot if the I/O priority was boosted or the thread was removed. (Refer to Chapter 4 for more on Autoboot).

It calls the IoThreadToPriority API, which enumerates all the IRPs requested the target thread (recall that each thread has a list of pending IRPs) and checks whether one has a lower priority than the target priority (normal in this case), identifying pending I/O priority invers. In turn, the device object responsible for those IRPs is identified, and the I/O manager checks whether a priority callback has been registered, which drivers can do through the IoRegisterPriorityCallback and by setting the DO_PRIORITY_CALLBACK_ENABLED flag on their device. Depending on whether the IRP is being paged I/O, this mechanism allows threaded paging boost. Finally, if no matching IRPs were found, but the thread has at least some pending IRPs, all are boosted regardless of device object or priority, which is called blanket boosting.

# I/O priority boosts and bumps

Windows uses a few modifications to normal I/O paths to avoid starvation, inversion, or otherwise unwanted scenarios when I/O priority is being used. Typically, these modifications are done by boosting I/O priority when needed. The following scenarios exhibit this behavior:

+   * When a driver is called with an IRP targeted to a particular file object, Windows makes sure that the request comes from kernel mode, the IRP uses normal priority even if the object has a lower I/O priority hint. This is called kernel bump.

+   * When reads or writes to the paging file are occurring (through IoPageRead and IoPageWrite), Windows checks whether the request comes from kernel mode and is not performed on behalf of Superfetch (which always uses idle I/O). In this case, the IRP uses normal priority even if the current thread has a lower I/O priority. This is called a paging bump.

The following experiment will show you an example of Very Low I/O priority and how you can use Process Monitor to look at I/O priorities on different requests.

EXPERIMENT: Very low versus normal I/O throughput
You can use the IO Priority sample application (included in this book's utilities) to look at the throughput difference between two threads with different I/O priorities. Follow these steps: