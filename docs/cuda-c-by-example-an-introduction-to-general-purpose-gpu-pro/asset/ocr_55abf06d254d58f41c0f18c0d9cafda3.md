# 10.1 Chapter Objectives

Through the course of this chapter, you will accomplish the following:

+   - You will learn about allocating page-locked host memory.
+   - You will learn what CUDA streams are.
+   - You will learn how to use CUDA streams to accelerate your applications.

# 10.2 Page-Locked Host Memory

In every example over the course of nine chapters, you have seen us allocate memory on the GPU with cudaMalloc(). On the host, we have always allocated memory with the vanilla, C library routine malloc(). However, the CUDA runtime offers its own mechanism for allocating host memory: cudaHostAlloc(). Why would you bother using this function when malloc() has served you quite well since day one of your life as a C programmer?

In fact, there is a significant difference between the memory that malloc() will allocate and the memory that cudaHostAlloc() allocates. The C library function malloc() allocates standard, pageable host memory, while cudaHostAlloc() allocates a buffer of page-locked host memory. Sometimes called pinned memory, page-locked buffers have an important property: The operating system guarantees us that it will never page this memory out to disk, which ensures its residency in physical memory. The corollary to this is that it becomes safe for the OS to allow an application access to the physical address of the memory, since the buffer will not be evicted or relocated.

Knowing the physical address of a buffer, the GPU can then use direct memory access [DMA] to copy data to or from the host. Since DMA copies proceed without intervention from the CPU, it also means that the CPU could be simultaneously paging these buffers out to disk or relocating their physical address by updating the operating system's pagetables. The possibility of the CPU moving pageable data means that using pinned memory for a DMA copy is essential. In fact, even when you attempt to perform a memory copy with pageable memory, the CUDA driver still uses DMA to transfer the buffer to the GPU. Therefore, your copy