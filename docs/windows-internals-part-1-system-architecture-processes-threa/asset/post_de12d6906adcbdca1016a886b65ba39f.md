
Running Limit. Test a few times (closing previous instances) would easily exhaust physical memory on a 32-bit system, and this limitation resides in one of the primary limits on system-wide 32-bit thread count.

## DPC stack

Windows keeps a per-processor DPC stack available for use by the system whenever DPCs are executing. This approach isolates the DPC code from the current thread's kernel stack. (This is unrelated to the DPC's actual operation because DPCs run in arbitrary thread context. See Chapter 6 for more on DPCs.)

DPC stack is also configured as the initial stack for handling the switch (x86), svc (ARM), or syscall1 (x64) instruction during a system call. The CPU is responsible for switching the stack when these instructions are executed, based on one of the model-specific registers (MSRs on x86/x64). However, Windows does not want to reprogram the MSR for every context switch that is an expensive operation. Windows therefore configures the per-processor DPC stack pointer in the MSR.

## Virtual address descriptors

The memory manager uses a demand–paging algorithm to know when to load pages into memory, waiting until a thread references an address and incurs a page fault before retrieving the page from disk. Like copy-on-write, demand paging is a form of *lazy evaluation*—waiting to perform a task until it is required.

The memory manager uses lazy evaluation not only to bring pages into memory but also to construct page tables required to describe new pages. When a thread commits a large region of virtual memory with `VirtualAlloc`, the memory manager could immediately construct the page tables required to access the entire range. But what if some of range is never accessed? Creating page tables for the entire range would be a wasted effort. Instead, the memory manager waits to create a page table until it incurs a page fault. It creates a page table for that page. This method significantly improves performance for processes that receive and/or commit a lot of memory access it sparsely.

The virtual address space that would be occupied by as-yet-nonexistent pages is charged to the process file quota and the system commit change. This ensures that space will be available for them until they are actually created. With the lazy-evaluation algorithm, allocating every large blocks of memory is a fast operation. When a thread allocates memory, the memory manager maintains another set of data structures to keep track of which virtual addresses the thread use. To do this, the memory manager in the process’s address space and which have not. These data-structures are known as *Virtual Address Descriptors* (VADs). VADs are allocated in non-paged pool.

## Process VADs

For each process, the memory manager maintains a set of VADs that describes the status of the process’s address space. VADs are organized in a self-balancing AVL tree (named after its inventors, Adelson-Velsky and Landis, where the height of the two child subtrees of any node differs by at most 1; this makes the insertion, lookup, and deletion very fast). On average, this results in the fewest comparisons when searching for a VAD corresponding to a virtual address. There is one VAD for each contiguous range of non-virtual addresses that have all the same characteristics (reserved versus committed mapped, memory access protection, and so on). Figure 5-29 shows a diagram of a VAD tree.

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_418_0.png)

**FIGURE 5-29** VADs.

When a process addresses address space or maps a view of a section, the memory manager creates a VAD to store any information supplied by the allocation request, such as the range of addresses being reserved, whether the range will be shared or private, whether a child process can inherit the contents of the range, and the page protection applied to pages in the range.

When a thread first accesses an address, the memory manager must create a PTE for the page containing the address. To do so, it finds the VAD whose range contains the address and uses the information to fill in the PTE. If the address falls outside the range covered by the VAD or in a range of addresses that are reserved but not committed, the memory manager knows that the thread didn’t allocate the memory before attempting to use it and therefore generates an access violation.

## EXPERIMENT: Viewing VADs

You can use the kernel debugger `!vad` command to view the VADs for a given process. First find the address of the root of the VAD tree with the `!process` command. Then specify that address to the `!vad` command, as shown in the following example of the VAD tree for a process running Explorer.exe.

```
kd> !process 0 1 explorer.exe
PROCESS fffc8069382e80
SessionId: 1 Cid: 43e0 Peb: 00bc5000 ParentId: 0338
Base: 55ab700 ObjectTable: fffda86281d80 HandleCount: 823.
image: explorer.exe
VadRoot fffc80691237f0 Vads 505 Clone 0 Private 5088. Modified 2146. Locked 0.
```

```
kd> !vad fffc8069aele470 End Commit VAD Level Start
ffff809bc52b0 9 640 64f 0 Mapped READWRITE
Pagefile section, shared commit 0x10
ffff809be6900 8 650 0 Mapped READONLY
Pagefile section, shared commit 0x2
ffff809bc4290 9 660 675 0 Mapped READONLY
Pagefile section, shared commit 0x16
ffff809ae1f320 7 680 0 32 Private READWRITE
ffff809b292b0 9 700 2 701 READWRITE
ffff809d4da470 8 710 2 Private READWRITE
ffff809279570 6 720 0 23 Mapped READONLY
Pagefile section, shared commit 0x4
ffff80985670 10 730 0 31 Mapped READONLY
Pagefile section, shared commit 0x2
ffff809bd9d90 9 740 2 41 Private READWRITE
ffff809d5a7b0 8 750 0 5 Mapped READONLY
\Windows\explorer.exe
Total VADs: 574, average level: 8, maximum depth: 10
Total private commit: 0x3420 pages (53376 KB)
Total shared commit: 0x478 pages (4576 KB)
```

## Rotate VADs

A video driver must typically copy data from the user-mode memory, including the video card memory and AGP port, both of which have caching attributes. To quickly allow these different views of memory to be mapped into a process, and to support these cache attributes the memory manager implements rotate VADs, which allow video drivers to transfer data directly by GPU and to rotate unneeded memory in and out of the process pages on demand. Figure 5-30 shows an example of how the same virtual address can rotate between video RAM and virtual memory.

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_419_0.png)

FIGURE 5-30.

Each release of Windows provides enhancements to the memory manager to make better use of non-uniform memory architecture NUMA machines, such as large server systems and Intel and AMD workstations. The NUMA support in the memory manager adds intelligent knowledge of node information such as location, topology, and access costs to allow applications and drivers to take advantage of NUMA capabilities, while abstracting the underlying hardware details.

When the memory manager is initializing, it calls `MiComputeMemoryCosts` to perform various page and cache operations on different nodes. It then computes the time it took for operations to complete. Based on this information, it builds a graph of access costs (the distance between a node and another node on the system). When the system requires pages for a given operation, it consults the graph to choose the most optimal node (that is, the closest). If no memory is available on that node, it chooses the closest node, and so on.

Although the memory manager ensures that, whenever possible, memory allocations come from the processor's node (the ideal node) of the thread making the allocation, it also provides functions that allow applications to choose their own node, as `VirtualAllocEx`, `CreateFileMapping`, `MapViewOfFileEx`, and `AllocateUserPages APIs`.

The ideal node is not used when applications allocate memory but also during kernel operation and page faults. For example, a thread running on a non-ideal processor takes a page fault, the memory manager will not use the current node. Instead, it will allocate memory from the thread's ideal node. Although this might result in slower access time while the thread is still running on this CPU, overall memory access will be optimized as the thread migrates back to its ideal node. In any case, if the ideal node is out of resources, the closest node to the ideal is chosen and not a random other node. Just like user-mode applications, however, drivers can specify their own node when using APIs as `MmAllocatePagesForEx` or `MmAllocateMemoryCache`.

Various memory manager pools and data structures are also optimized to take advantage of NUMA nodes. The memory manager tries to evenly use physical memory from all nodes on the system to handle the non-pooled pool. When an allocation is made, the memory manager uses the ideal node as an index to choose a virtual memory address inside non-pooled pool that responds to physical memory belonging to that node. In addition, NUMA node free lists are created to efficiently leverage these types of memory configurations. Apart from non-pooled pool, the system cache and system PTEs are also similarly allocated across all nodes, and as the memory manager's look-aside lists.

Finally, when the system needs to zero pages, it does so in parallel across different NUMA nodes by creating threads with NUMA affinities that correspond to the nodes in which the physical memory is located. The local prefetcher and SuperFetch (described in the section "Proactive memory management[SuperFetch]") also use the ideal node of the target process during prefetching, while soft page faults cause pages to migrate to the ideal node of the faulting thread.
