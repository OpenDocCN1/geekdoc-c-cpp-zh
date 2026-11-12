
For example, if the group g is initialized as above, then

```
g.sync();
```

will synchronize all threads in the block (i.e. equivalent to __syncthreads()).

Note that all threads in the group must participate in collective operations, or the behavior is undefined.

### C.2.2. Tiled Partitions

The tiled_partition() function can be used to decompose the thread block into multiple smaller groups of cooperative threads. For example, if we first create a group containing all the threads in the block:

```
thread_block wholeBlock = this_thread_block();
```

then we can partition this into smaller groups, each of size 32 threads:

```
thread_group tile32 = tiled_partition(wholeBlock, 32);
```

and, furthermore, we can partition each of these groups into even smaller groups, each of size 4 threads:

```
thread_group tile4 = tiled_partition(tile32, 4);
```

If, for instance, we were to then include the following line of code:

```
if (tile4.thread_rank()==0) printf("Hello from tile4 rank 0\n");
```

then the statement would be printed by every fourth thread in the block: the threads of rank 0 in each tile4 group, which correspond to those threads with ranks 0,4,8,12... in the wholeBlock group.

Note that, currently, only supported are tile sizes which are a power of 2 and no larger than 32.

### C.2.3. Thread Block Tiles

An alternative templated version of the tiled_partition function is available, where a template parameter is used to specify the size of the tile: with this known at compile time there is the potential for more optimal execution. Analogous to that in the previous section, the following code will create two sets of tiled groups, of size 32 and 4 respectively:

```
thread_block_tile<32> tile32 = tiled_partition<32>(this_thread_block());
thread_block_tile<4> tile4 = tiled_partition<4>(this_thread_block());
```

Note that the thread_block_tile templated data structure is being used here, and that the size of the group is passed to the tiled_partition call as a template parameter rather than an argument.

Thread Block Tiles also expose additional functionality as follows:

- .shfl()
- .shfl_down()
- .shfl_up()
- .shfl_xor()
- .any()
- .all()
- .ballot()
- .match_any()
- .match_all()

where these cooperative synchronous operations are analogous to those described in Warp Shuffle Functions and Warp Vote Functions. However their use here, in the context of these user-defined Cooperative Groups, offers enhanced flexibility and productivity. This functionality will be demonstrated later in this appendix.

As mentioned above, only supported are tile sizes which are a power of 2 and no larger than 32.

### C.2.2.4. Coalesced Groups

In CUDA's SIMT architecture, at the hardware level the multiprocessor executes threads in groups of 32 called warps. If there exists a data-dependent conditional branch in the application code such that threads within a warp diverge, then the warp serially executes each branch disabling threads not on that path. The threads that remain active on the path are referred to as coalesced. Cooperative Groups has functionality to discover, and create, a group containing all coalesced threads as follows:

```
coalesced_group active = coalesced_threads();
```

For example, consider a situation whereby there is a branch in the code in which only the 2nd, 4th and 8th threads in each warp are active. The above call, placed in that branch, will create (for each warp) a group, **active**, that has three threads (with ranks 0-2 inclusive).

### C.2.2.5. Uses of Intra-block Cooperative Groups

In this section, Cooperative Group functionality is illustrated through some usage examples.

### C.2.5.1. Discovery Pattern

Commonly developers need to work with the current active set of threads. No assumption is made about the threads that are present, and instead developers work with the threads that happen to be there. This is seen in the following “aggregating atomic increment across threads in a warp” example (written using the correct CUDA 9.0 set of intrinsics):

```
{
    unsigned int writemask = __activemask();
    unsigned int total = __popc(writemask);
    unsigned int prefix = __popc(writemask & __lanemask_lt());
    // Find the lowest-numbered active lane
    int elected_lane = __ffs(writemask) - 1;
    int base_offset = 0;
    if (prefix == 0) {
        base_offset = atomicAdd(p, total);
    }
    base_offset = __shfl_sync(writemask, base_offset, elected_lane);
    int thread_offset = prefix + base_offset;
    return thread_offset;
}
```

This can be re-written with Cooperative Groups as follows:

```
{
    cg::coalesced_group g = cg::coalesced_threads();
    int prev;
    if (g.thread_rank() == 0) {
        prev = atomicAdd(p, g.size());
    }
    prev = g.thread_rank() + g.shfl(prev, 0);
    return prev;
}
```

### C.2.5.2. Warp-Synchronous Code Pattern

Developers might have had warp-synchronous codes that they previously made implicit assumptions about the warp size and would code around that number. Now this needs to be specified explicitly.

// If the size is known statically
auto g = tiled_partition<16>(this_thread_block());
// Can use g.shfl and all other warp-synchronous builtins

However, the user might want to better partition his algorithm, but without needing the advantage of warp-synchronous builtins.

```
auto g = tiled_partition(this_thread_block(), 8);
```

In this case, the group g can still synchronize and you can still build varied parallel algorithms on top, but shfl() etc. are not accessible.

```
__global__ void cooperative_kernel(...) {
    // obtain default "current thread block" group
    thread_group my_block = this_thread_block();
    // subdivide into 32-thread, tiled subgroups
    // Tiled subgroups evenly partition a parent group into
    // adjacent sets of threads - In this case each one warp in size
    thread_group my_tile = tiled_partition(my_block, 32);
    // This operation will be performed by only the
    // first 32-thread tile of each block
    if (my_block.thread_rank() < 32) {
        // ...
        my_tile.sync();
    }
}
```

### C.2.5.3. Composition

Previously, there were hidden constraints on the implementation when writing certain code. Take this example:

```
__device__ int sum(int *x, int n) {
    // ...
    __syncthreads();
    return total;
}
```

```
__global__ void parallel_kernel(float *x) {
    // ...
    // Entire thread block must call sum
    sum(x, n);
}
```

All threads in the thread block must arrive at the __syncthreads() barrier, however, this constraint is hidden from the developer who might want to use sum(..). With Cooperative Groups, a better way of writing this would be:

```
__device__ int sum(const thread_group& g, int *x, int n)
{
    // ...
    g.sync();
    return total;
}
```

```
__global__ void parallel_kernel(...)
{
    // ...
    // Entire thread block must call sum
    sum(this_thread_block(), x, n);
    // ...
}
```

## C.3. Grid Synchronization

Prior to the introduction of Cooperative Groups, the CUDA programming model only allowed synchronization between thread blocks at a kernel completion boundary. The kernel boundary carries with it an implicit invalidation of state, and with it, potential performance implications.

For example, in certain use cases, applications have a large number of small kernels, with each kernel representing a stage in a processing pipeline. The presence of these kernels is required by the current CUDA programming model to ensure that the thread blocks operating on one pipeline stage have produced data before the thread block operating on the next pipeline stage is ready to consume. In such cases, the ability to provide global inter thread block synchronization would allow the application to be restructured to have persistent thread blocks, which are able to synchronize on the device when a given stage is complete.

To synchronize across the grid, from within a kernel, you would simply use the group:

```
grid_group grid = this_grid();
```

and call:

```
grid.sync();
```

To enable grid synchronization, when launching the kernel it is necessary to use, instead of the <<<...>>> execution configuration syntax, the cudaLaunchCooperativeKernel CUDA runtime launch API:

```
cudaLaunchCooperativeKernel {
const T *Func,
dim3 gridDim,
dim3 blockDim,
void **args,
size_t sharedMem = 0,
cudaStream_t stream = 0
}
```

(or the CUDA driver equivalent).

To guarantee co-residency of the thread blocks on the GPU, the number of blocks launched needs to be carefully considered. For example, as many blocks as there are SMs can be launched as follows:

```
cudaDeviceProp deviceProp;
cudaGetDeviceProperties(&deviceProp, dev);
// initialize, then launch
cudaLaunchCooperativeKernel((void*)my_kernel, deviceProp.multiProcessorCount,
numThreads, args);
```

Alternatively, you can maximize the exposed parallelism by calculating how many blocks can fit simultaneously per-SM using the occupancy calculator as follows:

```
cudaOccupancyMaxActiveBlocksPerMultiprocessor(&numBlocksPerSm, my_kernel,
numThreads, 0);
// initialize, then launch
cudaLaunchCooperativeKernel((void*)my_kernel,
deviceProp.multiProcessorCount*numBlocksPerSm, numThreads, args);
```

Note also that to use grid synchronization, the device code must be compiled in separate compilation (see the "Using Separate Compilation in CUDA" section in the CUDA
