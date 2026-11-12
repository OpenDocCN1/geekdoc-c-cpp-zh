
elements, requiring 128 iterations. A comparison-based sort is much quicker for such small values of N.

In this example, we used a single bit for the radix sort. Multiple bits can be used, which reduces the number of passes over the dataset at the expense of more intermediate storage. We currently use an iterative method to sort elements into sequential lists. It’s quite possible to work where the data will move to by counting the radix bits and using a prefix sum calculation to work out the index of where the data should be written. We look at prefix sum later in this chapter.

## CONSTANT MEMORY

Constant memory is a form of virtual addressing of global memory. There is no special reserved constant memory block. Constant memory has two special properties you might be interested in. First, it is cached, and second, it supports broadcasting a single value to all the elements within a warp.

Constant memory, as its name suggests, is for read-only memory. This is memory that is either declared at compile time as read only or defined at runtime as read only by the host. It is, therefore, constant only in respect of the GPU’s view onto memory. The size of constant memory is restricted to 64 K.

To declare a section of memory as constant at compile time, you simply use the `__constant__` keyword. For example:

```
__constant__ float my_array[1024] = { 0.0f, 1.0f, 1.34f, ... };
```

To change the contents of the constant memory section at runtime, you simply use the cudaMemcpyToSymbol function call prior to invoking the GPU kernel. If you do not define the constant memory at either compile time or host runtime then the contents of the memory section are undefined.

### Constant memory caching

**Compute 1.x devices** On compute 1.x devices (pre-Fermi), constant memory has the property of being cached in a small 8K L1 cache, so subsequent accesses can be very fast. This is providing that there is some potential for data reuse in the memory pattern the application is using. It is also highly optimized for broadcast access such that threads accessing the same memory address can be serviced in a single cycle.

With a 64 K segment size and an 8 K cache size, you have an 8:1 ratio of memory size to cache, which is really very good. If you can contain or localize accesses to 8 K chunks within this constant section you’ll achieve very good program performance. On certain devices you will find localizing the data to even smaller chunks will provide higher performance.

With a nonuniform access to constant memory a cache miss results in N fetches from global memory in addition to the fetch from the constant cache. Thus, a memory pattern that exhibits poor locality and/or poor data reuse should not be accessed as constant memory. Also, each divergence in the memory fetch pattern causes serialization in terms of having to wait for the constant memory. Thus, a warp with 32 separate fetches to the constant cache would take at least 32 times longer than an access to a single data item. This would grow significantly if it also included cache misses.

Single-cycle access is a huge improvement on the several hundred cycles required for a fetch from global memory. However, the several hundred-cycle access to global memory will likely be hidden by task switches to other warps, if there are enough available warps for the SM to execute. Thus, the benefit of using constant memory for its cache properties relies on the time taken to fetch data from global memory and the amount of data reuse the algorithm has. As with shared memory, the low-end devices have much less global memory bandwidth, so they benefit proportionally more from such techniques than the high-end devices.

Most algorithms can have their data broken down into “tiles” (i.e., smaller datasets) from a much larger problem. In fact, as soon as you have a problem that can’t physically fit on one machine, you have to do tiling of the data. The same tiling can be done on a multicore CPU with each one of the N cores taking 1/N of the data. You can think of each SM on the GPU as being a core on a CPU that is able to support hundreds of threads.

Imagine overlapping a grid onto the data you are processing where the total number of cells, or blocks, in the grid equals the number of cores (SMs) you wish to split the data into. Take these SM-based blocks and further divide them into at least eight additional blocks. You’ve now decomposed your data area into N SMs, each of which is allocated M blocks.

In practice, this split is usually too large and would not allow for future generations of GPUs to increase the number of SMs or the number of available blocks and see any benefit. It also does not work well where the number of SMs is unknown, for example, when writing a commercial program that will be run on consumer hardware. The largest number of SMs per device to date has been 32 (GT200 series). The Kepler and Fermi range aimed at compute has a maximum of 15 and 16 SMs respectively. The range designed primarily for gaming have up to 8 SMs.

One other important consideration is what interthread communication you need, if any. This can only reasonably be done using threads and these are limited to 1024 per block on Fermi and Kepler, less on earlier devices. You can, of course, process multiple items of data per thread, so this is not such a hard limit as it might first appear.

Finally, you need to consider load balancing. Many of the early card releases of GPU families had non power of two numbers of SMs (GTX460 = 7, GTX260 = 30, etc.). Therefore, using too few blocks leads to too little granularity and thus unoccupied SMs in the final stages of computation.

Tiling, in terms of constant memory, means splitting the data into blocks of no more than 64 K each. Ideally, the tiles should be 8 K or less. Sometimes tiling involves having to deal with halo or ghost cells that occupy the boundaries, so values have to be propagated between tiles. Where halos are required, larger block sizes work better than smaller cells because the area that needs to communicated between blocks is much smaller.

When using tiling there is actually quite a lot to think about. Often the best solution is simply to run through all combinations of number of threads, elements processed per thread, number of blocks, and tile widths, and search for the optimal solution for the given problem. We look at how to do this in Chapter 9 on optimization.

### Compute 2.x devices

On Fermi (compute 2.x) hardware and later, there is a level two (L2) cache. Fermi uses an L2 cache shared between each SM. All memory accesses are cached automatically by the L2 cache. Additionally, the L1 cache size can be increased from 16 K to 48 K by sacrificing 32 K of the shared memory per SM. Because all memory is cached on Fermi, how constant memory is used needs some consideration.

Fermi, unlike compute 1.x devices, allows any constant section of data to be treated as constant memory, even if it is not explicitly declared as such. Constant memory on 1.x devices has to be explicitly managed with special-purpose calls like cudaMemcpyToSymbol or declared at compile time. With Fermi, any nonthread-based access to an area of memory declared as constant (simply with the standard const keyword) goes through the constant cache. By nonthread-based access, this is an access that does not include threadIdx.x in the array indexing calculation.

If you need access to constant data on a per-thread-based access, then you need to use the compile time (__constant__) or runtime function (cudaMemcpyToSymbol) as with compute 1.x devices.

However, be aware that the L2 cache will still be there and is much larger than the constant cache. If you are implementing a tiling algorithm that needs halo or ghost cells between blocks, the solution will often involve copying the halo cells into constant or shared memory. Due to Fermi's L2 cache, this strategy will usually be slower than simply copying the tiled cells to shared or constant memory and then accessing the halo cells from global memory. The L2 cache will have collected the halo cells from the prior block's access of the memory. Therefore, the halo cells are quickly available from the L2 cache and come into the device much quicker than you would on compute 1.x hardware where a global memory fetch would have to go all the way out to the global memory.

### Constant memory broadcast

Constant memory has one very useful feature. It can be used for the purpose of distributing, or broadcasting, data to every thread in a warp. This broadcast takes place in just a single cycle, making this ability very useful. In comparison, a coalesced access to global memory on compute 1.x hardware would require a memory fetch taking hundreds of cycles of latency to complete. Once it has arrived from the memory subsystem, it would be distributed in the same manner to all threads, but only after a significant wait for the memory subsystem to provide the data. Unfortunately, this is an all too common problem, in that memory speeds have failed to keep pace with processor clock speeds.

Think of fetching data from global memory in the same terms as you might consider fetching data from disk. You would never write a program that fetched the data from disk multiple times, because it would be far too slow. You have to think about what data to fetch, and once you have it, how to reuse that data as much as possible, while some background process triggers the next block of data to be brought in from the disk.

By using the broadcast mechanism, which is also present on Fermi for L2 cache-based accesses, you can distribute data very quickly to multiple threads within a warp. This is particularly useful where you have some common transformation being performed by all threads. Each thread reads element N from constant memory, which triggers a broadcast to all threads in the warp. Some processing is performed on the value fetched from constant memory, perhaps in combination with a read/write to global memory. You then fetch element N + 1 from constant memory, again via a broadcast, and so on. As the constant memory area is providing almost L1 cache speeds, this type of algorithm works well.

However, be aware that if a constant is really a literal value, it is better to define it as a literal value using a #define statement, as this frees up constant memory. So don't place literals like PI into constant memory, rather define them as literal #define instead. In practice, it makes little difference in speed, only memory usage, as to which method is chosen. Let's look at an example program:
