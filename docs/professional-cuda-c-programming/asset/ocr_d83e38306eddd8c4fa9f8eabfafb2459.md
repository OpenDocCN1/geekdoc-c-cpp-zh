You can download the file reduceIntegerShfl.cu from Wrox.com. The result on Tesla K40 with CUDA 6.0 follows. You gain 1.42 speedup using the shuffle instruction to implement warp-level parallel reduction.

| Time (%) | Time | Calls | Avg | Min | Max | Name |
|---|---|---|---|---|---||
| 24.95% | 4.0000us | 1 | 4.0000us | 4.0000us | 4.0000us | reduceSmem() |
| 17.76% | 2.8480us | 1 | 2.8480us | 2.8480us | 2.8480us | reduceShfl() |

# SUMMARY

To obtain maximum performance, you need a memory hierarchy that can be explicitly managed. In C programming, there are no means to directly control data movement. In this chapter you learned about CUDA memory hierarchy types, such as shared memory, constant memory, and read-only cache. You learned how to control when data is brought in or evicted from shared memory to significantly improve performance. You also learned about the behavior of constant memory and the read-only cache and how to use them effectively.

Shared memory can be declared as a 1D or 2D array, shared memory is one-dimensional, and is accessed through 32 banks. Avoiding bank conflicts is an important factor during application optimization of shared memory. Shared memory is partitioned among all resident thread blocks; therefore, it is a critical resource and limit cache occupancy.

There are two main reasons to use shared memory in a kernel. One is to cache data on-chip and reduce the amount of global memory traffic. The other is to transform how data is arranged in shared memory to avoid non-coalesced global memory accesses.

Constant memory is optimized for read-only data that is broadcast to many threads at a time. Constant memory also uses its own SM cache, preventing reads from constant memory from interfering with global memory accesses passing through the L1 cache. As a result, using constant memory for appropriate data will not only optimize the accesses to that particular item but also improve overall global throughput.

The read-only texture cache offers an alternative to constant memory that is more optimized for scattered reads of data. This read-only cache uses a separate access pipeline and cache to make that data accessible to the SM. As a result, the read-only cache shares many of its benefits with constant memory, but is optimized for a different access pattern.

The shuffle instruction is a warp-level intrinsic function that enables threads in a warp to share data with each other quickly and directly. The shuffle instruction has lower latency than shared memory and does not require allocating additional resources. Using the shuffle instruction can reduce the number of warp-synchronous optimizations for a kernel. However, in many cases the shuffle instruction is not a replacement for shared memory as shared memory is visible to an entire block.

This chapter went into depth on a number of special-purpose types of memory. Although the use of each of these memory types is less general than global memory, using them appropriately