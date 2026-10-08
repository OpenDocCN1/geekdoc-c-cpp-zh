
thread. Using fewer registers in your kernels may allow more thread blocks to reside on an SM. More concurrent thread per-SM can increase occupancy and improve performance.

You can check the hardware resources used by a kernel with the nvcc compiler option below. For example, this will print the number of registers, bytes of shared memory, and bytes of constant memory used by each thread.

```
-Xptxas -v, -abi=no
```

If a kernel uses more registers than the hardware, the excess registers will spill over to local memory. This register spinning can have adverse consequences. The nvcc compiler uses heuristics to minimize register usage and avoid register spinning. You can optionally adjust these heuristics by providing additional information for each kernel to the compiler in the launch of bounds:

```
global void
lunch_bounds(maxThreadsPerBlock, minBlocksPerMultiprocessor)
kernel() {
// your kernel body
}
```

maxThreadsPerBlock specifies the maximum number of threads per block that a kernel will launch, minBlocksPerMultiprocessor is optional, and specifies the desired number of resident blocks per SM. Optimal bounds for a kernel will usually differ across architectural revisions.

You can also control the maximum number of registers used by all kernels in a compilation unit using the maxregcount option. In this example:

```
-maxregcount=32
```

the value specified (32) is ignored for kernels that have launch bounds specified.

# Local Memory

Variables in a kernel that are eligible for registers but cannot fit into the register space allocated for that kernel will spill into local memory. Variables that are likely to be in local memory are:

- Local arrays referenced with indices whose values cannot be determined at compile-time.
- Large local structures or arrays that would consume too register space.
- Any variable that does not fit within the kernel register limit.

The name "local memory" is misleading: Values spilled to local memory reside in the same physical location as global memory, so local memory accesses are characterized by high latency and low bandwidth and are subject to the requirements for efficient access which are described in the section "Memory Access Patterns" found later in this chapter. For GPUs with compute capability 2.0 and higher, local memory data is also cached in a per-SM L1 and per-device L2 cache.

# Shared Memory

Variables decorated with the following attribute in a kernel are stored in shared memory:

```
__shared__
```

Because shared memory is on-chip, it has a much higher bandwidth and much lower latency than local or global memory. It is used similarly to CPU L1 cache, but is also programmable.

Each SM has a limited amount of shared memory that is partitioned among thread blocks. Therefore, you must be careful not to over-utilize shared memory or you will inadvertently limit the number of active warps.

Shared memory is declared in the scope of a kernel function but has its lifetime with a thread block. When a thread block is finishing execution, its allocation of shared memory will be released and assigned to other thread blocks.

Shared memory serves as a basic for inter-thread communication. Threads within a block can cooperate by sharing data stored in shared memory. Access to shared memory must be synchronized using the following CUDA runtime introduced in early chapters:

```
void __syncthreads();
```

This function creates a barrier for all threads in the same thread block must reach before any other thread is allowed to proceed. By creating a barrier within a thread block, you can prevent a potential data hazard. Data hazards were covered in more depth in Chapter 3. They occur when there is an undefined ordering of multiple accesses to the same memory location from different threads, where at least one of accesses is a write. __syncthreads may also affect performance by forcing the SM to idle frequently.

The L1 cache and shared memory for an SM use the same 64 KB of on-chip, which is partially partitioned but can be dynamically configured at runtime:

```
cudaError cudaFuncSetCacheConfig(const void *func, enum cudaFuncCache cacheConfig);
```

This function configures the partitioning of on-chip memory on a per-kernel basis, setting the configuration for the kernel function by func. The supported cache configurations are:

- cudaFuncCachePrefNone: no preference (default)
- cudaFuncCachePrefShared: prefer 48 KB shared memory and 16 KB L1 cache
- cudaFuncCachePrefL1: prefer 48 KB L1 cache and 16 KB shared memory
- cudaFuncCachePrefEqual: equal split of L1 cache and shared memory, both 32KB

Fermi devices support the first three configurations, and Kepler devices support all of them.

# Constant Memory

Constant memory resides in device memory and is cached in a dedicated, per-SM constant cache. A constant variable is decorated with the following attribute:

```
__constant__
```

Constant variables must be declared with global scope, outside of any kernels. A limited amount of constant memory can be declared — 64 KB for all compute capabilities. Constant memory is statically declared and visible to all kernels in the same compilation unit.

Kernels can only read from constant memory. Constant memory must therefore be initialized by the host using:

```
cudaError_t cudaMemcpyToSymbol(const void* symbol, const void* src,
               size_t count);
```

This function count bytes from the memory pointed by src to the memory pointed by symbol, which is a variable that resides on the device in global or constant memory. This function is synchronous in most cases.

Constant memory performs best when all threads in a warp read the same memory address. For example, a coefficient for a mathematical formula is a good use for constant memory because all threads in a warp will use the same coefficient to conduct the same calculation on different data. If each thread in a warp reads from a different address, and only once, then constant memory is not the best choice because a single read from constant memory broadcasts to all threads in a warp.

# Texture Memory

Texture memory resides in device memory and is cached in a Per-SM, read-only cache. Texture memory is a type of global memory that is accessed through a dedicated read-only cache. The read-only cache includes support for hardware filtering, performing floating-point interpolation as part of the process. Texture memory is optimized for 2D spatial locality, so threads in a warp use texture memory to access 2D data will achieve the best performance. For applications, this is ideal and provides a performance advantage over the cache and the filtering hardware. However, for other applications texture memory can be slower than global memory.

# Global Memory

Global memory is the largest, highest-latency, and most commonly used memory on a GPU. The global name refers to its state and lifetime. Its state can be accessed from the device from any SM throughout the lifetime of the application.

A variable in global memory can either be declared statically or dynamically. You can declare a global variable statically in device code using the following qualifier:

```
__device__
```

In the “CUDA Programming Model” of Chapter 2, you learned how to dynamically allocate global memory. Global memory is allocated by the host using cudaMalloc and freed by the host using cudaFree. Pointers to global memory are passed to kernel functions as parameters. Global memory allocations exist for the lifetime of an application and are accessible to all of kernels. You must take care when accessing global memory from multiple threads. Because thread execution cannot be synchronized across thread blocks, there is a potential hazard of multiple threads in thread blocks concurrently modifying the same location in global memory, which will lead to an undefined program behavior.

Global memory resides in device memory and is accessible via naturally 32-byte, 64-byte, or 128-byte memory transactions. These memory transactions must be aligned; for the first address
