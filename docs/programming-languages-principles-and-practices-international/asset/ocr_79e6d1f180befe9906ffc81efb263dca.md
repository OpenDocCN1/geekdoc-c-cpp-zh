![](bbox=[0.26, 0.13, 0.74, 0.22])

Figure 10.18 The free space represented as a linked list

When a block of a certain size needs to be allocated, the memory manager searches the list for a free block with enough space, and then adjusts the free list to remove the allocated space, as in the picture shown in Figure 10.19.

![](bbox=[0.26, 0.31, 0.74, 0.42])

Figure 10.19 Allocating storage from the free space

When memory is reclaimed, blocks are returned to the free list. For example, if the light-shaded areas are storage to be reclaimed (as shown in Figure 10.20), then the new free list after reclamation would look as shown in Figure 10.21.

![](bbox=[0.31, 0.53, 0.69, 0.61])

Figure 10.20 Returning storage to the free list

![](bbox=[0.26, 0.66, 0.74, 0.74])

Figure 10.21 The free list after the return of storage

When blocks of memory are returned to the free list, they must be joined with immediately adjacent blocks to form the largest contiguous block of free memory. This process is called coalescing. In the preceding example, the small block freed in the middle of the memory area was coalesced with the free block adjacent to it on the right. Even with coalescing, however, a free list can become fragmented—that is, it can break into a number of small-sized blocks. When this occurs, it is possible for the allocation of a large block to fail, even though there is enough total space available to allocate it. To prevent this, memory must occasionally be compacted by moving all free blocks together and coalescing them into