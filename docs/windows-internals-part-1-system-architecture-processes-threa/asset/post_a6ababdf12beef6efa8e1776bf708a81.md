
1kd> dd /c 1MiSystemVaCountPeak L f

Theoretically, the different virtual address ranges assigned to components can grow arbitrarily in size if enough virtual address space is available. In practice, on 32-bit systems, the kernel allocator implements limits to set on each virtual address type for the purposes of reliability and stability. (On 64-bit systems, kernel address space exhaustion is currently not a concern.) Although limits are imposed by default, system administrators can use the registry to modify these limits for the virtual address types that are currently marked as limited (see Table 5-8).

If the current request for the Mi inSystemVa exceeds the available limit, a failure is made (see the previous experiment) and a reclaim operation is requested regardless of available memory. This should help alleviate memory load and allow the virtual address allocation to work during the next attempt. Recall, however, that reclaiming affects system cache and non-paged pool.

# EXPERIMENT: Setting system virtual address limits

The MiSystemVaCountL1 contains limits for system virtual address usage that can be set for each type. Currently, the manager allows only certain virtual address types to be limited, and it provides the ability to use an undocumented system for the system dynamically during run time. (These limits can also be set by the registry, as described at http://msdn.microsoft.com/en-us/library/bb870880.aspx.) These limits can be set for those types marked as Table 5-8.

You can use the MemLimit utility (found in this book's downloadable resources) on 32-bit systems to query and set the different limits for these types and to see the current and peak virtual address space usage. Here's how you can query the current with the -q flag:

```
C:\Tools\MemLimit.exe -q
```

MemLimit v1.01 - Query and set hard limits on system VA space consumption
Copyright (C) 2008-2016 by Alex Ionescu
www.alex-ionescu.com

System VA Consumption:

| Type | Current | Peak | Limit |
| --- | --- | --- | --- |
| Non Paged Pool | 45056 KB | 55296 KB | 0 KB |
| Paged Pool | 151552 KB | 165888 KB | 0 KB |
| System Cache | 44664 KB | 47923 KB | 0 KB |
| System PTEs | 90112 KB | 135168 KB | 0 KB |
| Session Space | 63488 KB | 73728 KB | 0 KB |

As an experiment, use the following command to set a limit of 100 MB for paged pool:
memlimit.exe -p 100M

Now use Sysinternals TestLimit to create as many handles as possible. Normally, with enough paged pool, the number of handles should be around 16 million. But with the limit to 100 MB, it's:

```
C:\Sysinternals\Testlimit.exe -h
```

Testlimit v5.24 - test Windows limits
Copyright (C) 2012-2015 Mark Russinovich
Sysinternals - www.sysinternals.com

Process ID: 4780

Creating handles...
Created 10727844 handles. Lasterror: 1450

See Chapter 8 in Part 2 for more information about objects, handles, and paged-pool consumption.

# System virtual address space quotas

The system virtual address space limits described in the previous section allow for the limiting of system-wide virtual address space usage of kernel components. However, they work only on 32-bit systems when applied to the system as a whole. To address specific quota requirements that system administrators might have, the memory manager collaborates with the process manager to enforce system-wide or user-specific quotas.

You can configure the PagedPoolQuota, NonPagedPoolQuota, PagingFileQuota, and Working-SetPages values in the HKLM\System\CurrentControlSet\Control\Session Manager key. To address specific quota requirements that system administrators might have, the memory manager collaborates with the process manager to enforce system-wide or user-specific quotas.

You can configure the PagedPoolQuota, NonPagedPoolQuota, PagingFileQuota, and Working-SetPages values in the HKLM\System\CurrentControlSet\Control\Session Manager key. To address specific quota requirements that system administrators might have, the memory manager collaborates with the process manager to enforce system-wide or user-specific quotas.

You can configure the PagedPoolQuota, NonPagedPoolQuota, PagingFileQuota, and Working-SetPages values in the HKLM\System\CurrentControlSet\Control\Session Manager key. To address specific quota requirements that system administrators might have, the memory manager collaborates with the process manager to enforce system-wide or user-specific quotas.

You can configure the PagedPoolQuota, NonPagedPoolQuota, PagingFileQuota, and Working-SetPages values in the HKLM\System\CurrentControlSet\Control\Session Manager key. To address specific quota requirements that system administrators might have, the memory manager collaborates with the process manager to enforce system-wide or user-specific quotas.

You can configure the PagedPoolQuota, NonPagedPoolQuota, PagingFileQuota, and Working-SetPages values in the HKLM\System\CurrentControlSet\Control\Session Manager key. To address specific quota requirements that system administrators might have, the memory manager collaborates with the process manager to enforce system-wide or user-specific quotas.

You can configure the PagedPoolQuota, NonPagedPoolQuota, PagingFileQuota, and Working-SetPages values in the HKLM\System\CurrentControlSet\Control\Session Manager key. To address specific quota requirements that system administrators might have, the memory manager collaborates with the process manager to enforce system-wide or user-specific quotas.

You can configure the PagedPoolQuota, NonPagedPoolQuota, PagingFileQuota, and Working-SetPages values in the HKLM\System\CurrentControlSet\Control\Session Manager key. To address specific quota requirements that system administrators might have, the memory manager collaborates with the process manager to enforce system-wide or user-specific quotas.

You can configure the PagedPoolQuota, NonPagedPoolQuota, PagingFileQuota, and Working-SetPages values in the HKLM\System\CurrentControlSet\Control\Session Manager key. To address specific quota requirements that system administrators might have, the memory manager collaborates with the process manager to enforce system-wide or user-specific quotas.

You can configure the PagedPoolQuota, NonPagedPoolQuota, PagingFileQuota, and Working-SetPages values in the HKLM\System\CurrentControlSet\Control\Session Manager key. To address specific quota requirements that system administrators might have, the memory manager collaborates with the process manager to enforce system-wide or user-specific quotas.

You can configure the PagedPoolQuota, NonPagedPoolQuota, PagingFileQuota, and Working-SetPages values in the HKLM\System\CurrentControlSet\Control\Session Manager key. To address specific quota requirements that system administrators might have, the memory manager collaborates with the process manager to enforce system-wide or user-specific quotas.

You can configure the PagedPoolQuota, NonPagedPoolQuota, PagingFileQuota, and Working-SetPages values in the HKLM\System\CurrentControlSet\Control\Session Manager key. To address specific quota requirements that system administrators might have, the memory manager collaborates with the process manager to enforce system-wide or user-specific quotas.

You can configure the PagedPoolQuota, NonPagedPoolQuota, PagingFileQuota, and Working-SetPages values in the HKLM\System\CurrentControlSet\Control\Session Manager key. To address specific quota requirements that system administrators might have, the memory manager collaborates with the process manager to enforce system-wide or user-specific quotas.

You can configure the PagedPoolQuota, NonPagedPoolQuota, PagingFileQuota, and Working-SetPages values in the HKLM\System\CurrentControlSet\Control\Session Manager key. To address specific quota requirements that system administrators might have, the memory manager collaborates with the process manager to enforce system-wide or user-specific quotas.

You can configure the PagedPoolQuota, NonPagedPoolQuota, PagingFileQuota, and Working-SetPages values in the HKLM\System\CurrentControlSet\Control\Session Manager key. To address specific quota requirements that system administrators might have, the memory manager collaborates with the process manager to enforce system-wide or user-specific quotas.

As an experiment, use the following command to set a limit of 100 MB for paged pool:
memlimit.exe -p 100M

Now use Sysinternals TestLimit to create as many handles as possible. Normally, with enough paged pool, the number of handles should be around 16 million. But with the limit to 100 MB, it's:

```
C:\Sysinternals\Testlimit.exe -h
```

Testlimit v5.24 - test Windows limits
Copyright (C) 2012-2015 Mark Russinovich
Sysinternals - www.sysinternals.com

Process ID: 4780

Creating handles...
Created 10727844 handles. Lasterror: 1450

See Chapter 8 in Part 2 for more information about objects, handles, and paged-pool consumption.

# System virtual address space quotas

The system virtual address space limits described in the previous section allow for the limiting of system-wide virtual address space usage of kernel components. However, they work only on 32-bit systems when applied to the system as a whole. To address specific quota requirements that system administrators might have, the memory manager collaborates with the process manager to enforce system-wide or user-specific quotas.

You can configure the PagedPoolQuota, NonPagedPoolQuota, PagingFileQuota, and Working-SetPages values in the HKLM\System\CurrentControlSet\Control\Session Manager key. To address specific quota requirements that system administrators might have, the memory manager collaborates with the process manager to enforce system-wide or user-specific quotas.

To enable user-specific quotas, you can set the following values in the HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Session Manager key:

- PagedPoolQuota: The maximum size of the paged pool in MB.
- NonPagedPoolQuota: The maximum size of the non-paged pool in MB.
- PagingFileQuota: The maximum size of the paging file in MB.
- Working-SetPages: The maximum number of pages allowed in the working set.

The following table shows the types of quotas:

**Table 5-9 Qu types**

| Value Name | Description | Value Type | Privilege |
| --- | --- | --- | --- |
| PagedPoolQuota | This is the maximum size of the paged pool that can be allocated by this process. | Size in MB | IncreaseQuota |
| NonPagedPoolQuota | This is the maximum size of the non-paged pool that can be allocated by this process. | Size in MB | IncreaseQuota |
| PagingFileQuota | This is the maximum number of pages that a process can have backed by the page file. | Pages | IncreaseQuota |
| WorkingSetPages | This is the maximum number of pages allowed in the working set of the process. | Pages | IncreaseQuota |

## User address space layout

Just as address space in the kernel, the user address space is also built dynamically. The addresses of thread stacks, process heaps, and loaded images (such as DLLs) are dynamically computed (if the application and images support it) through the ASLR mechanism. Apart from these regions (and some system structures like the TEBs and BEB), all other memory allocations are run-time dependent and combined with DEP provides a mechanism for remote exploitation harder to achieve. Because Windows code and data are placed at dynamic locations, an attacker cannot easily hard-code a meaningful offset into either a program or a system-supplied DLL.

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_382_0.png)

FIGURE 5-14 User address space layout with ASLR enabled.

# EXPERIMENT: Analyzing user address space

The VMMap utility from Sysinternals can show you a detailed view of the virtual memory being used by any process on your machine. This information is divided into categories for each type of allocation, summarized as follows:

- Image This displays memory allocations used to map the executable and its dependencies (such as dynamic libraries) and any other memory-mapped image (portable executable files).
- Mapped File This displays memory allocations for memory mapped data files.
- Shareable This displays memory allocations marked as shareable, typically including shared memory (but not memory-mapped files, which are listed under Image or Mapped File).
- Heap This displays memory allocated for the heap(s) that this process owns.
- Managed Heap This displays memory allocated by the .NET CLR (managed objects). It would show nothing for a process that does not use .NET.
- Stack This displays memory allocated for the stack of each thread in this process.
- Private Data This displays memory allocations marked as private other than the stack and heap, such as internal data structures.
