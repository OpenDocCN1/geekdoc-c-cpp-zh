
# Chapter 4. Memory

| | Number of Sets | Associativity | Size |
|---|---|---|---|
| Instruction TLB | 32/16/32 | 4/8/4 way | 128 entries |
| Data TLB | 16 | 4 way | 64 entries |
| Level 2 TLB (Shared) | 128/128/-_ | 4/8/-_ | 512/1024/- entries |

Table 4.2: TLB parameters for three x86 processors: 2.6 GHz SSE2, 2.2 GHz AVX, and 3.6 GHz AVX2 (see table A.1 for the full names of the machines). The 3.6 GHz AVX2 machine does not have level 2 TLB.

forms a virtual address. To map the virtual address to the physical address, it looks up the TLB; if there is a TLB miss, it must look up the page tables. Looking up the page tables may trigger additional DRAM accesses if the page tables are not in cache.

The page table lookup may trigger a page fault if the virtual address is yet to be mapped to a page frame. If so, the page fault handler, which is an important component of the operating system kernel, is invoked. It allocates an actual page frame so that a physical address may be formed. Once the processor can look with the caches and trigger a DRAM access if necessary.

We think of a simple instruction such as movq (%rax, %rsi, 2), %rbx as taking a few cycles. If there is a page fault, the actual cost can be in the millions of cycles. In fact, there can be two page faults from this single instruction if the quad word crosses page boundaries. Even if there is no page fault, there can be a TLB miss, which can consume the order of 100 cycles.

# Virtual memory and program speed

Given that the virtual memory setup is exceedingly complex and is invoked every other instruction, it follows that the mechanisms to implement virtual memory may influence program speed in many ways.

When memory is dynamically allocated by a program using malloc(), new(), or _mm_malloc(), the last of which is preferred if memory needs to be aligned, the allocation function returns an address in virtual memory, and pages may be allocated only in virtual memory. There is always a page fault the first time a page is accessed. The pages are mapped to page frames by the page fault handler. If there is enough

# 4.1. DRAM and cache memory

DRAM memory, page faults do not occur except when pages are accessed for the first time.

On most computers, the memory controllers predict memory accesses and prefetch words to cache. The prefetching normally does not cross page boundaries to prevent page faults from being triggered.

Another scenario where the paging system is in play is when large amounts of data are transferred from DRAM to the network card or to graphics processor memory. During the transfer, some of the pages may get moved out of DRAM memory into hard disk by the memory management unit of the operating system kernel, complicating the transfer. One way is to copy the data to be transferred to kernel buffers and incur a substantial overhead. Another way is to request the operating system to keep the pages “pinned” to DRAM memory.

There are many more ways in which virtual memory impacts program speed. The role of cache and TLB misses is explained later in this chapter. Other aspects related to multithreaded programming are found in the next chapter.

# 4.1.4 Latency to DRAM memory: First attempts

In this section, we make our first attempts at measuring the access time to DRAM memory. All our attempts fail, but we are led into certain aspects of the memory system that have a bearing on program performance.

The organization of memory is such that if we attempt to investigate one part of it, we need to be aware of the other parts as well. All the parts of the memory system are interrelated. Thus, to measure the access time to DRAM memory, we need to know about the size of the cache. We begin by giving a basic picture of the memory system as a whole. The measurement of latency brings to light some other parts of the memory system, and as we progress, we fill in some of the details in the picture.

A significant point is that all the traffic between DRAM and the processor packages are in multiples of the cache line size. The cache line is 64 bytes or 512 bits. If we attempt to read a single byte or a single word (2 bytes or 16 bits) or a double word or a quad word from memory, the memory system will bring the entire cache line into cache, anticipating that we will access locations in the same cache line soon.

Latency to DRAM memory is defined as the time to issuing a load/store instruction that triggers a DRAM access and its completion. The latency of writing to memory can differ from the latency of reading for certain types of DRAM. We limit ourselves to read latency for simplicity.

Measuring the latency to DRAM memory is a more complicated matter than one may realize at first sight. Many techniques are used to hide the latency to DRAM memory. Among these, the two most important are instruction-level parallelism and caching. Instruction-level parallelism enables the processor to issue a sequence of load or instructions to set up a pipeline of memory. If the pipeline can hold 10 memory accesses in various stages, the effective latency of a long stream of DRAM accesses is cut to a tenth. For example, the latency to DRAM is 200 cycles, the nth memory access may be initiated during cycle number 20n and completed during cycle number 20n+199. This sort of overlapping is possible only if the memory accesses are independent and there is sufficient parallelism in the instruction stream. Caching greatly reduces the effective latency of DRAM memory access as well. These techniques for hiding latency to memory are so effective that many programs do not realize how large the latency to DRAM memory can be.

Here is a first and not very careful attempt at measuring:

```
int unitstride(int *a){
    int sum=0;
    for(int i=0; i < 1000*1000*1000; i++)
        sum += a[i];
    return sum;
}
```

The function unitstride() loads 10^9 entries of a[] and computes their sum. The compiler unfolds the loop and introduces parallelism in the loop body. As a result, the running time of this function is determined by instructions that load entries of a[] and not by arithmetic.

The function unitstride() is timed as follows:

```
void time_unitstride(){
    int a[1000*1000*1000];
    a[0] = 0;
    for(int i=0; i < 1000*1000*1000; i++)
        Timestamp clk;
        clk.tick();
    unitstride(a);
```

# 4.1.5 DRAM cache memory

The function time_unitstride() defines a[] statically, initializes every entry of a[] to 0, and makes a single call to unitstride(). The function call is timed, and the number of cycles is divided by 10^9 to derive the cycles per access. Each array dereferencing a[i] in unitstride() is counted as a memory access.

The two functions unitstride() and time_unitstride() are defined in separate files and compiled separately. As usual, we use the -ipo option for procedural optimization during compilation, and we use -fno-inline-functions to eliminate inlining. If the two functions are in the same file or if procedural optimization is turned on, the compiler will figure out that the call to unitstride() is doing nothing meaningful and simply eliminate the call.

Initializing the array to zero on line 4 ensures that page frames in physical memory have been allocated to the entire array before the function unitstride() is called. The program reports 0.92 cycles per access. This is a woful underestimate of the latency to DRAM memory.

Any program that accesses data sequentially with unit stride will benefit from the size of the cache line. To avoid cache hits, the program below accesses only one of 16 locations.

```
int stride16(int *a){
    sum=0;
```
