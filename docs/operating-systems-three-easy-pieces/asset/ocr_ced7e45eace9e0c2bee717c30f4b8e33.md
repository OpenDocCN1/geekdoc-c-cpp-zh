# SEGMENTATION

> TIP: IF 1000 SOLUTIONS EXIST, NO GREAT DOES The fact that so many different algorithms exist to try to minimize external fragmentation is indicative of a stronger underlying truth: there is no "best" to solve the problem. Thus, we settle for something reasonable and hope it is good enough. The only solution (as we will see in forthcoming chapters) is to avoid the problem altogether, by never allocating memory in variable-sized chunks

malloc() will find free space for the object and return a pointer to it the caller. In others, however the heap segment itself may need to grow. In this case, the memory-allocation library will provide a system call to grow the heap (e.g., the traditional UNIX sbrk() system call). The OS will then (usually) provide more space, updating the segment size to the new (bigger) size, and informing the library of success; the library can then allocate space for the new object and return successfully to the calling program. Note that the OS can reject the request, if no physical memory is available, or if it decides that the process has too much

There and perhaps most important, is managing free space in physical memory. When a new address space is created, the OS has to find in physical memory for its segments. Previously, we assumed that each address space was the same size, and physical memory could be thought of as a bank of slots where processes would fit in. Now, we have a number of segments, and each segment might be a different.

The general problem that arises is physical memory quickly full of free space, making it difficult to allocate new segments, or to grow existing ones. We call this problem fragmentation [R69]; see Figure 16.6 (left).

In the example, a process comes along and wishes to allocate a 20KB segment. In that example, there is 24KB free, but not in contiguous segment (rather, in non-contiguous chunks). Then, the OS cannot satisfy the 20KB request. Similar problems could occur when a request to grow a segment arrives; if the next so many bytes of physical space are not available, the OS will have to reject the request, even though there may be free bytes anywhere in physical memory

One solution to this problem would be to compact physical memory by rearranging the existing segments. For example, the OS could whichever processes are running, copy their data to one contiguous region of memory, and then their segment register values point to the new physical locations, and thus have a large free extent of memory with which to work. By doing so, the OS enables the new allocation request to succeed. However, compaction is expensive, as copying segments is memory-intensive and generally uses a fair amount of processor time; see

© 2008–19, ARPACI-USSEAU

THREE EASY PIECES