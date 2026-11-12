
上下文。如果程序使用 `malloc()` 或 `__nv_aligned_device_malloc()` 而未显式指定堆大小，则会分配默认的八兆字节堆。

以下 API 函数用于获取和设置堆大小：

- `cudaDeviceGetLimit(size_t* size, cudaLimitMallocHeapSize)`
- `cudaDeviceSetLimit(cudaLimitMallocHeapSize, size_t size)`

授予的堆大小至少为 `size` 字节。`cuCtxGetLimit()` 和 `cudaDeviceGetLimit()` 返回当前请求的堆大小。

堆的实际内存分配发生在模块加载到上下文时，可以通过 CUDA 驱动 API 显式加载（参见 Module），也可以通过 CUDA 运行时 API 隐式加载（参见 CUDA Runtime）。如果内存分配失败，模块加载将生成 `CUDA_ERROR_SHARED_OBJECT_INIT_FAILED` 错误。

一旦发生模块加载，堆大小即无法更改，并且不会根据需求动态调整大小。

为设备堆预留的内存是通过主机侧 CUDA API 调用（例如 `cudaMalloc()`）分配的内存之外的额外内存。

## B.21.2. 与主机内存 API 的互操作性

通过设备 `malloc()` 或 `__nv_aligned_device_malloc()` 分配的内存不能使用运行时释放（即，通过调用设备内存中的任何释放内存函数）。

同样，通过运行时分配的内存（即，通过调用设备内存中的任何内存分配函数）不能通过 `free()` 释放。

此外，在设备代码中通过调用 `malloc()` 或 `__nv_aligned_device_malloc()` 分配的内存不能用于任何运行时或驱动 API 调用（例如 cudaMemcpy、cudaMemset 等）。

## B.21.3. 示例

### B.21.3.1. 每线程分配

以下代码示例：

```
#include <stdio.h>
#include <stdlib.h>

__global__ void mallocTest()
{
    size_t size = 123;
    char* ptr = (char*)malloc(size);
    memset(ptr, 0, size);
    printf("Thread %d got pointer: %p\n", threadIdx.x, ptr);
    free(ptr);
}

int main()
{
    // Set a heap size of 128 megabytes. Note that this must
    // be done before any kernel is launched.
    cudaDeviceSetLimit(cudaLimitMallocHeapSize, 128*1024*1024);
    mallocTest<<<1, 5>>>();
    cudaDeviceSynchronize();
    return 0;
}
```

将输出：

```
Thread 0 got pointer: 00057920
Thread 1 got pointer: 0005708c
Thread 2 got pointer: 000570f8
Thread 3 got pointer: 00057164
Thread 4 got pointer: 000571d0
```

请注意，每个线程都会遇到 malloc() 和 memset() 命令，因此会接收并初始化其自己的分配。（确切的指针值会有所不同：这些仅为示例。）

### B.21.3.2. 每线程块分配

```
#include <stdlib.h>

__global__ void mallocTest()
{
    __shared__ int* data;

    // The first thread in the block does the allocation and then
    // shares the pointer with all other threads through shared memory,
    // so that access can easily be coalesced.
    // 64 bytes per thread are allocated.
    if (threadIdx.x == 0) {
        size_t size = blockDim.x * 64;
        data = (int*)malloc(size);
    }
    __syncthreads();

    // Check for failure
    if (data == NULL)
        return;

    // Thread index into the memory, ensuring coalescence
    int* ptr = data;
    for (int i = 0; i < 64; ++i)
        ptr[i * blockDim.x + threadIdx.x] = threadIdx.x;

    // Ensure all threads complete before freeing
    __syncthreads();

    // Only one thread may free the memory!
    if (threadIdx.x == 0)
        free(data);
}

int main()
{
    cudaDeviceSetLimit(cudaLimitMallocHeapSize, 128*1024*1024);
    mallocTest<<<10, 128>>>();
    cudaDeviceSynchronize();
    return 0;
}
```

### B.21.3.3. 内核启动之间持续的分配

```
#include <stdlib.h>
#include <stdio.h>

#define NUM_BLOCKS 20

__device__ int *dataptr[NUM_BLOCKS]; // Per-block pointer

__global__ void allocmem()
{
    // Only the first thread in the block does the allocation
    // since we want only one allocation per block.
    if (threadIdx.x == 0)
        dataptr[blockIdx.x] = (int*)malloc(blockDim.x * 4);
    __syncthreads();

    // Check for failure
    if (dataptr[blockIdx.x] == NULL)
        return;

    // Zero the data with all threads in parallel
    dataptr[blockIdx.x][threadIdx.x] = 0;
}

// Simple example: store thread ID into each element
__global__ void usemem()
{
    int *ptr = dataptr[blockIdx.x];
    if (ptr != NULL)
        (ptr[threadIdx.x]) += threadIdx.x;
}

// Print the content of the buffer before freeing it
__global__ void freemem()
{
    int* ptr = dataptr[blockIdx.x];
    if (ptr == NULL)
        printf("Block %d, Thread %d: final value = %d\n",
               blockIdx.x, threadIdx.x, ptr[threadIdx.x]);

    // Only free from one thread!
    if (threadIdx.x == 0)
        free(ptr);
}

int main()
{
    cudaDeviceSetLimit(cudaLimitMallocHeapSize, 128*1024*1024);

    // Allocate memory
    allocmem<<< NUM_BLOCKS, 10 >>>();

    usemem<<< NUM_BLOCKS, 10 >>>();
    usemem<<< NUM_BLOCKS, 10 >>>();
    usemem<<< NUM_BLOCKS, 10 >>>();

    // Free memory
    freemem<<< NUM_BLOCKS, 10 >>>();

    cudaDeviceSynchronize();

    return 0;
}
```

## B.22. 执行配置

对 `__global__` 函数的任何调用都必须为该调用指定 _执行配置_。执行配置定义了用于在设备上执行该函数的网格和块的维度，以及关联的流（有关流的描述，请参见 CUDA Runtime）。

执行配置通过在函数名和带括号的参数列表之间插入形式为 `<<< Dg, Db, Ns, S >>>` 的表达式来指定，其中：

- Dg 的类型为 dim3（参见 dim3），指定网格的维度和大小，使得 Dg.x * Dg.y * Dg.z 等于正在启动的块数；

- Db 的类型为 dim3（参见 dim3），指定每个块的维度和大小，使得 Db.x * Db.y * Db.z 等于每个块的线程数；

- Ns 的类型为 size_t，指定此调用每个块动态分配的共享内存字节数（在静态分配的内存之外）；此动态分配的内存由任何声明为外部数组的变量使用（如 `__shared__` 中所述）。Ns 是可选参数，默认值为 0；

- S 的类型为 cudaStream_t，指定关联的流；S 是可选参数，默认值为 0。

例如，声明为的函数

```
__global__ void Func(Float* parameter);
```

必须这样调用：

```
Func<<< Dg, Db, Ns >>>(parameter);
```

执行配置的参数在实际函数参数之前求值。

如果 Dg 或 Db 大于 Compute Capabilities 中指定的设备允许的最大尺寸，或者 Ns 大于设备上可用的共享内存最大量减去静态分配所需的共享内存量，则函数调用将失败。

## B.23. 启动边界

如在多处理器级别中详细讨论，内核使用的寄存器越少，越有可能有更多线程和线程块驻留在多处理器上，这可以提高性能。

因此，编译器使用启发式方法来最小化寄存器使用量，同时将寄存器溢出（参见设备内存访问）和指令数量降至最低。

应用程序可以选择通过在 `__global__` 函数定义中使用 `__launch_bounds__()` 限定符以启动边界的形式向编译器提供额外信息来辅助这些启发式方法：

```
__global__ void __launch_bounds__(maxThreadsPerBlock, minBlocksPerMultiprocessor)
MyKernel(...) {
    ...
}
```

- maxThreadsPerBlock 指定应用程序启动 MyKernel() 时每个块的最大线程数；它编译为 .maxntid PTX 指令；

- minBlocksPerMultiprocessor 是可选的，指定每个多处理器所需的最小驻留块数；它编译为 .minnctapersm PTX 指令。

如果指定了启动边界，编译器首先从中推导出内核应使用的寄存器数量上限 L，以确保 minBlocksPerMultiprocessor 个块（如果未指定 minBlocksPerMultiprocessor，则为单个块）的 maxThreadsPerBlock 个线程可以驻留在多处理器上（有关内核使用的寄存器数量与每个块分配的寄存器数量之间关系的信息，请参见硬件多线程）。然后，编译器以以下方式优化寄存器使用量：

- 如果初始寄存器使用量高于 L，编译器会进一步降低它，直到其小于或等于 L，通常以更多的本地内存使用和/或更多的指令数量为代价；

- 如果初始寄存器使用量低于 L

- 如果指定了 maxThreadsPerBlock 但未指定 minBlocksPerMultiprocessor，编译器使用 maxThreadsPerBlock 来确定 n 和 n+1 个驻留块之间的寄存器使用量阈值（即，当使用一个更少的寄存器为额外驻留块腾出空间时，如多处理器级别中的示例），然后应用与未指定启动边界时类似的启发式方法；

- 如果同时指定了 minBlocksPerMultiprocessor 和 maxThreadsPerBlock，编译器可能会将寄存器使用量提高到 L，以减少指令数量并更好地隐藏单线程指令延迟。

如果内核执行时每个块的线程数超过其启动边界 maxThreadsPerBlock，则内核启动将失败。
