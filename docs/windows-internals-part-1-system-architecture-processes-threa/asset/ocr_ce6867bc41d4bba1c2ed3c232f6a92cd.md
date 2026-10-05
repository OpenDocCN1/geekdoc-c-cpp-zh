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

You can configure the PagedPoolQuota, NonPagedPoolQuota, PagingFileQuota, and Working-SetPages values in the HKLM\SYSTEM\CurrentControlSet\Control\SessionManager\Memory key to specify how many handles each given process can use. This information is read at initialization, and the default system quota block is generated and then assigned to all system processes. Processes use a copy of the default system quota block unless user-specific quotas have been defined, as explained in next.