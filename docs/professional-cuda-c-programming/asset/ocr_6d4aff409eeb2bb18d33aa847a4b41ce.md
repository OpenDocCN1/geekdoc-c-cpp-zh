![](bbox=[0.147, 0.103, 0.597, 0.355])

**FIGURE 5-1**

A fixed amount of shared memory is allocated to each thread block when it starts executing. This shared memory address space is shared by all threads in a thread block. Its contents have the same lifetime as the thread block in which it was created. Shared memory accesses are issued per warp. Ideally, each request to access shared memory is served in one transaction. In the worst case, each request to access shared memory is executed sequentially in 32 transactions. If multiple threads access the same word in shared memory, one thread fetches the word, and sends it to the other threads via multicast. Details on avoiding multicasting-transaction shared memory requests are provided in the following sections.

Shared memory is partitioned among all resident thread blocks on an SM; therefore, shared memory is a critical resource that limits device parallelism. The more shared memory used by a kernel, the fewer possible concurrently active thread blocks.

# PROGRAM-MANAGED CACHE

In C programming, loop transformations are a common cache optimization. Loop transformations improve cache locality during loop traversal by rearranging the order of iterations. At the algorithm level, you need to manually adjust loops to achieve better spatial locality while considering cache size. The cache is transparent to your program, and the compiler handles all data movement. You have no ability to control cache eviction.

Shared memory is a program-managed cache. You have full control over when data is moved into shared memory, and when data is evicted. By allowing you to manually manage shared memory, CUDA makes it easier for you to optimize your application code by providing more fine-grained control over data placement and improving on-chip data movement.