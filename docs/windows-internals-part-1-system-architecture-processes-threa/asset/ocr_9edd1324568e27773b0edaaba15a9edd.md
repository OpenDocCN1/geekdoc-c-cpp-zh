14. In Process Manager, notice that the base and dynamic priorities of the thread are now 24. Recall that the kernel never applies priority boosts for threads in the Real-Time priority range.

![](bbox=[0.235, 0.143, 0.563, 0.473])

# Windows System Resource Manager

Windows Server 2012 R2 Standard Edition includes an optionally installable component called Windows Resource Manager (WSRM). It permits the administrator to configure policies that specify CPU utilization, affinity settings, and memory limits (both physical and virtual) for processes. In addition, WSRM can generate resource-utilization reports that can be used for accounting and verification of service-level agreements with users.

Policies can be applied for specific applications (by matching the name of or without specific command-line arguments), users, or groups. The policies can be scheduled to take effect at certain periods or be enabled all time.

After you set a resource-allocation policy to manage processes, the WSRM service monitors CPU consumption of managed processes and adjusts process priorities when those processes do not meet their target CPU allocations.

The physical memory limitation uses the function SetProcessWorkingSetSizeEx to set a hard-working set maximum. The virtual memory limit is implemented by the service checking the private virtual memory consumed by the processes. (See Chapter 5 for an explanation of these memory limits.) If this limit is exceeded, WSRM can be configured to kill the processes or write an entry to the event log. This behavior can be used to detect a process with a memory

CHAPTER 4 Threads