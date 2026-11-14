**Table 2.1 Memory hierarchy in the CUDA programming model detailing the location, lifetime, and privacy of the five memory spaces**

| Memory | Location | Lifetime | Privacy |
| :--- | :--- | :--- | :--- |
| Global | Device memory accessed via L2 cache | Application/deallocation | All threads |
| Constant (read-only) | Device memory accessed via constant cache | Application/deallocation | All threads |
| Texture (read-only) | Device memory accessed via texture cache | deallocation | All threads |
| Shared | Shared memory on each SM | Kernel | Private to each block of threads |
| Local | Device memory accessed via L2 cache | Thread | Private to each thread |

# ## 2.4 Programming and Optimization Concepts

GPU programming adds new concepts to the fundamentals of parallel programming. GPU programming can be broken down into two stages: porting and optimization. The first task for the programmer should be to get the GPU code running on a GPU and giving the correct results, although the effort required in later stages can be reduced if the code is not just naively ported, but, instead, the algorithm and approach are carefully tailored to match the GPU architecture. This initial porting process results in GPU portions of the program. Once the GPU code has been validated, the code needs to be optimized in order to fully utilize a GPU’s hardware and squeeze as much performance out as possible. There are three key strategies for improving code performance on GPU architectures that need to be considered during porting and optimization:

+   * Increasing parallel efficiency – achieving the maximum parallel execution in order to fully utilize the GPU architecture by ensuring a program exposes as much parallelism as possible.
+   * Improving memory throughput – making the best use of the different memory locations on a GPU in order to reduce or hide memory access latency.
+   * Improving instruction throughput – feeding the cores with a constant flow of instructions in order to reduce the amount of time cores spend idle.

In this section, GPU programming concepts are introduced, and an explanation of how they can be managed in order to influence performance, with respect to the three strategies outlined above, is given.

# ## 2.4.1 Latency: Memory Access

Memory access latency varies from one memory location to another. The highest latency memory access is data transfers between the host and the device, which is on the order of thousands of clock cycles. On the GPU global memory and local memory are the slowest memory locations, as they reside in device memory (DRAM) that has the highest latency of several hundred clock cycles (and lowest bandwidth). Constant memory and texture memory also reside in device memory but as they come armed with their own cache, accesses can be as fast as constant/texture cache latency, which can be considerably quicker than global device memory accesses. As shared memory is on-chip, it is the fastest programmer-managed memory location. There is also an on-chip L1 cache and L2 cache on devices of compute capability 2.x and higher, which offer lower latency/higher bandwidth memory accesses [1]. The latency/bandwidth of these memory locations varies from architecture to architecture, so exact numbers are not given here.