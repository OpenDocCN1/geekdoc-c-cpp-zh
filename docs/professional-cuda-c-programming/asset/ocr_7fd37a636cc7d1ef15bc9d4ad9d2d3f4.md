Because shared memory is on-chip, it has a much higher bandwidth and much lower latency than local or global memory. It is used similarly to CPU L1 cache, but is also programmable.

Each SM has a limited amount of shared memory that is partitioned among thread blocks. Therefore, you must be careful not to over-utilize shared memory or you will inadvertently limit the number of active warps.

Shared memory is declared in the scope of a kernel function but has its lifetime with a thread block. When a thread block is finishing execution, its allocation of shared memory will be released and assigned to other thread blocks.

Shared memory serves as a basic for inter-thread communication. Threads within a block can cooperate by sharing data stored in shared memory. Access to shared memory must be synchronized using the following CUDA runtime introduced in early chapters:

```
void __syncthreads();
```

This function creates a barrier for all threads in the same thread block must reach before any other thread is allowed to proceed. By creating a barrier within a thread block, you can prevent a potential data hazard. Data hazards were covered in more depth in Chapter 3. They occur when there is an undefined ordering of multiple accesses to the same memory location from different threads, where at least one of accesses is a write.__syncthreads may also affect performance by forcing the SM to idle frequently.

The L1 cache and shared memory for an SM use the same 64 KB of on-chip, which is partially partitioned but can be dynamically configured at runtime:

```
cudaError cudaFuncSetCacheConfig(const void *func, enum cudaFuncCache cacheConfig);
```

This function configures the partitioning of on-chip memory on a per-kernel basis, setting the configuration for the kernel function by func. The supported cache configurations are:

+   - cudaFuncCachePrefNone: no preference (default)
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