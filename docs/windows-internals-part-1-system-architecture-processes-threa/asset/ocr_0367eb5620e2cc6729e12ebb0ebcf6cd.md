didn't have to worry about it because the system would crash away. However, because low-memory conditions can occur temporarily, and today's mobile devices are not as powerful as larger machines, it is important that device drivers properly handle allocation failures that indicate kernel memory is exhausted.

The driver calls that will be invoked with random failures include the functions ExAllocatePool*, MmProbeAndLockPagesSpec, MmMapIoCache, MmAllocateContiguous-Memory, MmAllocatePagesForId, IoAllocateInt, IoAllocateMd, IoAllocateWorkItem, IoAllocateErrorLogEntry, IoSetCompleteRoutineEx, and other R APIs that allocate from the pool. Driver Verifier also fails allocations managed by kernel GDI functions (see the WDK documentation for a complete list). Additionally, you can specify the following:

+   ** The probability that allocation will fail** This is 6 percent by default.

+   ** Which applications should be subject to the simulation** All are by default.

+   ** Which pool tags should be affected** All are by default.

+   ** What delay should be used before fault injection starts** The default is 7 minutes after the system boots, which is enough to get past the critical initialization period in which a low-memory condition might prevent a device driver from loading.

You can change these customizations with command line options to verifier.exe.

After the period, Driver Verifier starts randomly failing allocation calls for device drivers it verifies. If a driver doesn't correctly handle allocation failures, this will likely show up as a system crash.

# Systematic Low Resources Simulation

Similar to the Low Resources Simulation, this option fails certain calls to the kernel and Ndis.Sys (for network drivers), but does so in a systematic way, by examining the call stack at the point of failure injection. If the driver handles the failures correctly, that call stack will not be injected again. This allows the driver to see issues in a systematic way, fix a reported issue, and move on to the next. Examining all call stacks is a relatively expensive operation, verifying more than a single driver at a time with this is not recommended.

# Miscellaneous checks

Some of the checks that Driver Verifier calls miscellaneous allow it to detect the freeing of system structures in the pool that are all active. For example, Driver Verifier will check for:

+   ** Active work items in free memory** A driver calls ExFreePool to free a pool block in one or more work items queued with IoQueueWorkItem are present.

+   ** Active resources in free memory** A driver calls ExFreePool before calling ExDelete-Resource to destroy an ERESOURCE object.

+   ** Active look-aside list in free memory** A driver calls ExFreePool before calling ExDelete-PagedLookasideList or ExDeletePagedLookasideList to delete the look-aside list.