# 4.4. Page tables and virtual memory

the data region. As indicated in figure 4.8, the global data map to higher addresses than code.

The dynamically allocated memory is() in between. The principle way to allocate memory dynamically is using malloc() in C. In C++, we may also use new[]. In some of our earlier examples, we used _mm_malloc() to force alignment of memory at 16-byte boundaries, cache line boundaries, or page boundaries.

The sketch in 4.8 has omitted a few things, namely, shared libraries and variables to threads. Like dynamically allocated memory, these are also mapped to virtual addresses higher than code and data regions and lower than the stack region.

Kernel code and data are mapped to addresses beyond PAGE_OFFSET. We will look at that mapping shortly.

# 4.4.2 Physical address space and page tables

Program speed is influenced by the paging system in several ways. Typically, 40% of the instructions are loads and stores, and each memory access involves the paging system. The TLB (translation look-aside buffer) is a shortcut past the huge overheads of the paging system. If a memory word is found in L1 cache and its virtual address is found in TLB, the latency of the memory access will be 4 cycles. However, if there is a TLB miss, the latency can go up to several hundred cycles. If there is a page fault, the latency of a single memory access can go up to millions, ever billions, of cycles. It is also true that the first access of a page in virtual memory always leads to a page fault, and the page fault handler is responsible for allocating a page frame in physical memory.

The paging system is responsible for protecting a program's memory from other programs and preventing programs from making illegal memory accesses. During a context switch, when the kernel executes one process and schedules another, the kernel may need to flush the TLB (using a privileged instruction) to protect the address space of the processes. The TLB flush can be expensive. We will look at how the kernel and hardware work together to implement the paging system to get a sense of the overheads of the paging system.