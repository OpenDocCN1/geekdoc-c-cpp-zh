# Affinity

Each thread has an affinity mask that specifies the processors on which the thread is allowed to run. The thread affinity mask is inherited from the process affinity mask. By default, all processes (and therefore all threads) begin with an affinity mask that is equal to the set of all active processors on their assigned group. In others, the system is free to schedule all threads on any available processor within the group associated with the process. However, to optimize throughput, partition workloads to a specific set of processors, or both, applications can choose to change the affinity mask for a thread. This can be done at several levels:

+   - By calling the SetThreadAffinityMask function to set the affinity for an individual thread.

+   - By calling the SetProcessAffinityMask function to set the affinity for all the threads in a process.

+   - Task Manager and Process Explorer provide a GUI to this function. To access it, right-click a process and choose Set Affinity. In addition, the PsExec tool (from Sysinternals) provides a command-line interface to this function (see the -a switch in its output).

+   - By making a process a member of a job that has a job-wide affinity mask set using the SetInformationJobObject function (described in Chapter 3).

+   - By specifying an affinity mask in the image header when compiling the application.

> Tip For a detailed specification of the Windows image format, search for Portable Executable and Common Object Format Specification at http://msdn.microsoft.com.

An image can also have the uniprocessor flag set at link time. If this flag is set, the system chooses a single processor at process-creation time (MmNumberOfProcessors) and assigns that as the process affinity mask, starting with the first processor and then going round-robin across all the processors within the group. For example, on a dual-processor system, the first time an image marked with the uniprocessor flag is launched, it is assigned to CPU 0; the second time, CPU 1; the third time, CPU 0; the fourth time, CPU 1, and so on. This flag can be used as a temporary workaround for programs that have multithreaded synchronization bugs on multiprocessor systems due to race conditions but not on uniprocessor systems. If an image exhibits such symptoms and is unsigned, you can add the flag manually editing the image header with a Portable Executable (PE) image-editing tool. A better solution, compatible with signed executables, is to use the Microsoft Application Compatibility Toolkit and add a shim to force the compatibility database to mark the image as uniprocessor-

# EXPERIMENT: Viewing and changing process affinity

In this experiment, you will modify the affinity settings for a process and see that process affinity is inherited by new processes: