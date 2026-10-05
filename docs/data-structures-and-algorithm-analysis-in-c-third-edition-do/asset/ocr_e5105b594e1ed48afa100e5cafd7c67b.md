# Sec. 12.3 Memory Management

# 425

![](bbox=[0.225, 0.185, 0.774, 0.34])

**Figure 12.2** Blocks as seen by the memory manager. Each block includes additional information such as freelist link pointers, start and end tags, and a size field. (a) The layout for a freelist. The beginning of the block contains the tag bit, the size field, and two pointers for the freelist. The end of the block contains a second tag field and a second block size field. (b) A reserved block of bytes. The memory manager adds to these $k$ bytes an additional tag bit and block size field at the beginning of the block, and a second tag field at the end of the block.

then, if the $k-m$ words are reserved as a block on the freelist, in the current location.

When a block $F$ is free, it must be merged into the freelist. If we do not care about adjacent free blocks, then this is a simple insertion into the doubly linked list of free blocks. However, we would like to merge adjacent blocks, as this allows the memory manager to serve requests of the largest possible size. Merging is easily done with the tag and size fields stored at the ends of each block, as illustrated by Figure 12.13. Here, the memory manager checks the first unit of immediately preceding $F$ to see if the preceding block (call $P$) is free. If so, the memory manager $P$’s tag stores the size of $P$, indicating the position for the beginning of the block in memory. $P$ can then expand its size to include block $F$. If $P$ is not free, then we just add block $F$ to the freelist. Finally, we check the block following the end of block $F$. If this indicates that the following block (call $S$) is free, then $S$ is removed from the freelist and the size of $F$ is extended appropriately.

We now consider how a free block is selected to service a memory request. To illustrate the process, assume that we have a memory pool with 200 units of storage. After some series of allocation requests and releases, we have reached a point where there are four free blocks on the freelist of sizes 25, 35, 32, and 45 (in order). Assume that a request is made for 30 units of storage. For our examples, we ignore the overhead imposed for the tag, link, and size fields discussed above.