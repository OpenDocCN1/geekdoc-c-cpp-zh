

例如，如果组 g 按如上方式初始化，则

```
g.sync();
```

将同步块中所有线程（即等效于 __syncthreads()）。

请注意，组中所有线程都必须参与集体操作，否则行为未定义。

### C.2.2. 分块分区

tiled_partition() 函数可用于将线程块分解为多个较小的协作线程组。例如，如果我们先创建一个包含块中所有线程的组：

```
thread_block wholeBlock = this_thread_block();
```

然后我们可以将其分割为较小的组，每组大小为 32 个线程：

```
thread_group tile32 = tiled_partition(wholeBlock, 32);
```

而且，我们还可以将这些组中的每一个进一步分割为更小的组，每组大小为 4 个线程：

```
thread_group tile4 = tiled_partition(tile32, 4);
```

例如，如果我们随后包含以下代码行：

```
if (tile4.thread_rank()==0) printf("Hello from tile4 rank 0\n");
```

则该语句将由块中每第四个线程打印：即每个 tile4 组中 rank 为 0 的线程，这些线程对应 wholeBlock 组中 rank 为 0、4、8、12... 的线程。

请注意，目前仅支持大小为 2 的幂且不大于 32 的分块大小。

### C.2.3. 线程块分块

tiled_partition 函数还有一个替代的模板版本，其中模板参数用于指定分块大小：在编译时已知此大小，有可能实现更优的执行。与前一节类似，以下代码将分别创建大小为 32 和 4 的两组分块组：

```
thread_block_tile<32> tile32 = tiled_partition<32>(this_thread_block());
thread_block_tile<4> tile4 = tiled_partition<4>(this_thread_block());
```

请注意，此处使用的是 thread_block_tile 模板数据结构，并且组大小是作为模板参数而非参数传递给 tiled_partition 调用的。

线程块分块还公开了以下附加功能：

- .shfl()
- .shfl_down()
- .shfl_up()
- .shfl_xor()
- .any()
- .all()
- .ballot()
- .match_any()
- .match_all()

这些协作同步操作类似于 Warp Shuffle Functions 和 Warp Vote Functions 中描述的操作。但是，在用户定义的协作组上下文中使用它们，提供了增强的灵活性和生产力。此功能将在本附录后面部分进行演示。

如上所述，仅支持大小为 2 的幂且不大于 32 的分块大小。

### C.2.2.4. 合并组

在 CUDA 的 SIMT 架构中，硬件级别的多处理器以称为 warp 的 32 线程组执行线程。如果应用程序代码中存在数据相关的条件分支，导致 warp 内的线程发生分歧，则 warp 将串行执行每个分支，禁用不在该路径上的线程。路径上保持活跃的线程称为合并线程。协作组具有发现并创建包含所有合并线程的组的功能，如下所示：

```
coalesced_group active = coalesced_threads();
```

例如，考虑一种情况：代码中存在一个分支，其中每个 warp 中只有第 2、4 和 8 个线程是活跃的。将上述调用放置在该分支中，将为每个 warp 创建一个名为 **活跃** 的组，该组包含三个线程（rank 为 0-2，包含两端）。

### C.2.2.5. 块内协作组的用法

本节通过一些用法示例说明协作组功能。

### C.2.5.1. 发现模式

通常，开发者需要处理当前活跃的线程集。不对存在的线程做任何假设，而是开发者处理碰巧存在的线程。这体现在以下示例中：“跨 warp 线程的聚合原子递增”（使用正确的 CUDA 9.0 内置函数集编写）：

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

可以使用协作组重写如下：

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

### C.2.5.2. Warp 同步代码模式

开发者可能之前编写过 warp 同步代码，他们对 warp 大小做了隐含假设，并围绕该数字编写代码。现在需要显式指定此大小。

// If the size is known statically
auto g = tiled_partition<16>(this_thread_block());
// Can use g.shfl and all other warp-synchronous builtins

但是，用户可能希望更好地划分其算法，但又不需要 warp 同步内置函数的优势。

```
auto g = tiled_partition(this_thread_block(), 8);
```

在这种情况下，组 g 仍然可以同步，并且你仍然可以在其之上构建各种并行算法，但 shfl() 等不可访问。

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

### C.2.5.3. 组合

以前，编写某些代码时实现中存在隐藏约束。请看此示例：

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

线程块中的所有线程必须到达 __syncthreads() 屏障，但是，对可能想要使用 sum(..) 的开发者来说，此约束是隐藏的。使用协作组，更好的写法如下：

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

## C.3. 网格同步

在引入协作组之前，CUDA 编程模型仅允许在内核完成边界处同步线程块。内核边界伴随着状态的隐式失效，以及潜在的性能影响。

例如，在某些用例中，应用程序有大量小内核，每个内核代表处理流水线中的一个阶段。当前 CUDA 编程模型要求存在这些内核，以确保在处理一个流水线阶段的线程块生产数据之前，处理下一个流水线阶段的线程块已准备好消费。在这种情况下，提供全局线程块间同步的能力将允许将应用程序重构为具有持久线程块，这些线程块可以在给定阶段完成时在设备上同步。

要在内核内部同步整个网格，只需使用以下组：

```
grid_group grid = this_grid();
```

并调用：

```
grid.sync();
```

要启用网格同步，启动内核时需要使用 cudaLaunchCooperativeKernel CUDA 运行时启动 API，而不是 <<<...>>> 执行配置语法：

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

（或 CUDA 驱动程序等效项）。

为了保证线程块在 GPU 上驻留，需要仔细考虑启动的块数量。例如，可以启动与 SM 数量相同的块，如下所示：

```
cudaDeviceProp deviceProp;
cudaGetDeviceProperties(&deviceProp, dev);
// initialize, then launch
cudaLaunchCooperativeKernel((void*)my_kernel, deviceProp.multiProcessorCount,
numThreads, args);
```

或者，可以通过使用占用率计算器计算每个 SM 可同时容纳多少块，以最大化暴露的并行性，如下所示：

```
cudaOccupancyMaxActiveBlocksPerMultiprocessor(&numBlocksPerSm, my_kernel,
numThreads, 0);
// initialize, then launch
cudaLaunchCooperativeKernel((void*)my_kernel,
deviceProp.multiProcessorCount*numBlocksPerSm, numThreads, args);
```

另请注意，要使用网格同步，设备代码必须进行单独编译（请参阅 CUDA 中的“在 CUDA 中使用单独编译”部分，CUDA

