Even with these in place, some things are difficult to visualize, specifically memory management. Each container may use its own PFN database, or one page file, and so on. Windows 10 (64-bit versions) and Windows Server 2016 provide such possible memory control through Memory Partitions.

A memory partition consists of its own memory-related management structures, as page lists (standby, modified, zero, free, etc.), commit charge, working set, page trimmer, modified page writer, zero-page thread, and so on, until isolated from other partitions. Memory partitions are represented in the system by Partition objects, which are securable, named objects (like other executive objects). One partition always exists, called the System Partition and it represents the system as a whole and is the ultimate partition of any explicitly created partition. The system partition's address is stored in a global variable (MSystemPartition) and is in KernelObjects\MemoryPartition visible with tools as WinObj from Sysinternals as shown in Figure 5-45.

![](bbox=[0.17, 0.3, 0.72, 0.56])

FIGURE 5-45 The System Partition in WinObj
| Name | Type |
|---|---|
| MemoryPartitionObjects | Event |
| HighPagePartitionCondition | Event |
| HighMemoryCondition | Event |
| LowMemoryCondition | Event |
| LowMemoryPostCondition | Event |
| LowPageCondition | Event |
| MaximumCommit | Event |
| KernelObjects | Event |
| KnownObjects | Partition |
| KnownDll32 | Event |
| ObjectTypes | Event |
| RPCControl | Session |
| Security | Session |
| Sessions | Event |
| SuperfetchPartitionChanged | Event |
| SuperfetchGranularity | Event |
| System | Event |
| SystemErrorPortReady | Event |

All partition objects are stored in global list, where the current maximum partition count is 1024 (10 bits), because the partition index must be encoded in PTEs for quick access to partition information where applicable. One of these is the system partition and other values are used as special sentinels, leaving 1021 partitions available.

Memory partitions can be created from user mode or kernel mode using the NtCreatePartition internal (undocumented) function; user mode callers must have the SeLockMemory privilege for the call to succeed. The function can accept a parent partition, which will pages come from and eventually return to, when the partition is destroyed; the system partition is the default parent if none is specified. NtCreatePartition delegates the actual work to the memory manager MiCreatePartition function.

An existing partition can be opened by using NtOpenPartition (no special privilege required for this the object can be protected by ACLs). The actual manipulation of a partition is reserved for the NtManagePartition function. This is the function that can be used to add memory to the partition, adding a paging file, copy memory from one partition to another, and generally obtain information about a partition.

CHAPTER 5 Memory management 457