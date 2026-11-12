

```cpp
#define KERNEL_LOOP 4096

__constant__ static const u32 const_data_gpu[KERNEL_LOOP];
__device__ static u32 gmem_data_gpu[KERNEL_LOOP];
static u32 const_data_host[KERNEL_LOOP];
```

```cpp
__global__ void gmem_test_gpu(const u32 * gmem_data, const u32 num_elements)
{
    const u32 tid = (blockIdx.x * blockDim.x) + threadIdx.x;
    if (tid < num_elements)
    {
        u32 d = gmem_data_gpu[0];

        for (int i = 0; i < KERNEL_LOOP; i++)
        {
            d ^= gmem_data_gpu[i];
            d = gmem_data_gpu[i];
            d &= gmem_data_gpu[i];
            d |= gmem_data_gpu[i];
        }

        gmem_data[tid] = d;
    }
}
```

```cpp
__global__ void const_test_gpu(const u32 * const data, const u32 num_elements)
{
    const u32 tid = (blockIdx.x * blockDim.x) + threadIdx.x;
    if (tid < num_elements)
    {
        u32 d = const_data_gpu[0];

        for (int i = 0; i < KERNEL_LOOP; i++)
        {
            d ^= const_data_gpu[i];
            d = const_data_gpu[i];
            d &= const_data_gpu[i];
            d |= const_data_gpu[i];
        }

        data[tid] = d;
    }
}
```

```cpp
__host__ void wait_exit(void)
{
    char ch;
    printf("\nPress any key to exit");
    ch = getch();
}
```

```c
__host__ void cuda_error_check(const char * prefix, const char * postfix)
{
    if (cudaPeekAtLastError() != cudaSuccess)
    {
        printf("\n%s%s%s", prefix, cudaGetErrorString(cudaGetLastError()), postfix);
        cudaDeviceReset();
        wait_exit();
        exit(1);
    }
}
```

```c
__host__ void generate_rand_data(u32 * host_data_ptr)
{
    for (u32 i = 0; i < KERNEL_LOOP; i++)
    {
        host_data_ptr[i] = (u32) rand();
    }
}
```

```c
__host__ void gpu_kernel(void)
{
    const u32 num_elements = (128*1024);
    const u32 num_threads = 256;
    const u32 num_blocks = (num_elements+(num_threads-1)) / num_threads;
    const u32 num_bytes = num_elements * sizeof(u32);
    int max_device_num;
    const int max_runs = 6;

    CUDA_CALL(cudaGetDeviceCount(&max_device_num));

    for (int device_num=0; device_num < max_device_num; device_num++)
    {
        CUDA_CALL(cudaSetDevice(device_num));
    }

    u32 * data_gpu;
    cudaEvent_t kernel_start1, kernel_stop1;
    cudaEvent_t kernel_start2, kernel_stop2;
    float delta_time1 = 0.0F, delta_time2 = 0.0F;
    struct cudaDeviceProp device_prop;
    char device_prefix[261];

    CUDA_CALL(cudaMalloc(&data_gpu, num_bytes));
    CUDA_CALL(cudaEventCreate(&kernel_start1));
    CUDA_CALL(cudaEventCreate(&kernel_start2));
    CUDA_CALL(cudaEventCreateWithFlags(&kernel_stop1, cudaEventBlockingSync));
    CUDA_CALL(cudaEventCreateWithFlags(&kernel_stop2, cudaEventBlockingSync));

    // printf("\nlaunching %u blocks, %u threads", num_blocks, num_threads);
    CUDA_CALL(cudaGetDeviceProperties(&device_prop, device_num));
    sprintf(device_prefix, "ID:%d %s:", device_num, device_prop.name);

    for (int num_test=0; num_test < max_runs; num_test++)
    {
        // Generate some random data on the host side
        // Replace with function to obtain data block from disk, network or other
        // data source
        generate_rand_data(const_data_host);

        // Copy host memory to constant memory section in GPU
        CUDA_CALL(cudaMemcpyToSymbol(const_data_gpu, const_data_host,
        KERNEL_LOOP * sizeof(u32)));
        // Warm up run
        printf("\nLaunching gmem kernel warm-up");
        gmem_test_gpu <<<num_blocks, num_threads>>>(data_gpu, num_elements);
        cuda_error_check("Error returned from gmem startup kernel");

        // Do the gmem kernel
        // printf("\nLaunching gmem kernel");
        CUDA_CALL(cudaEventRecord(kernel_start1,0));

        gmem_test_gpu <<<num_blocks, num_threads>>>(data_gpu, num_elements);

        cuda_error_check("Error returned from gmem runtime kernel");

        CUDA_CALL(cudaEventRecord(kernel_stop1,0));
        CUDA_CALL(cudaEventSynchronize(kernel_stop1));
        CUDA_CALL(cudaEventElapsedTime(&delta_time1, kernel_start1, kernel_stop1));
        printf("\nGMEM Elapsed time: %.3fms", delta_time1);

        // Copy host memory to global memory section in GPU
        CUDA_CALL(cudaMemcpyToSymbol(gmem_data_gpu, const_data_host,
        KERNEL_LOOP * sizeof(u32)));
        // Warm up run
        printf("\nLaunching constant kernel warm-up");
        const_test_gpu <<<num_blocks, num_threads>>>(data_gpu, num_elements);

        cuda_error_check("Error returned from constant startup kernel");

        // Do the constant kernel
        // printf("\nLaunching constant kernel");
        CUDA_CALL(cudaEventRecord(kernel_start2,0));

        const_test_gpu <<<num_blocks, num_threads>>>(data_gpu, num_elements);
        cuda_error_check("Error returned from constant runtime kernel");
        CUDA_CALL(cudaEventRecord(kernel_stop2,0));
        CUDA_CALL(cudaEventSynchronize(kernel_stop2));
        CUDA_CALL(cudaEventElapsedTime(&delta_time2, kernel_start2, kernel_stop2));
        //printf("Inconst Elapsed time : %3.fms", delta_time2);
        if (delta_time1 > delta_time2)
            printf("****\n%sConstant version is faster by: %.2fms (G=%.2fms, C=%.2fms)",
                   device_prefix, delta_time1-delta_time2, delta_time1, delta_time2);
        else
            printf("****\n%sGMEM version is faster by: %.2fms (G=%.2fms, C=%.2fms)",
                   device_prefix, delta_time2-delta_time1, delta_time1, delta_time2);
    }
    CUDA_CALL(cudaEventDestroy(kernel_start1));
    CUDA_CALL(cudaEventDestroy(kernel_start2));
    CUDA_CALL(cudaEventDestroy(kernel_stop1));
    CUDA_CALL(cudaEventDestroy(kernel_stop2));
    CUDA_CALL(cudaFree(data_gpu));
    CUDA_CALL(cudaDeviceReset());
    printf("\n");
    wait_exit();
}
```

## 第6章 CUDA内存处理

注意 cudaMemcpyToSymbol 调用的工作方式。您可以将数据复制到 GPU 上的任何命名全局符号，无论该符号位于全局内存还是常量内存中。因此，如果将数据分块为 64 K 块，您可以从常量缓存中访问它。如果所有线程都访问同一数据元素，这非常有用，因为您可以从常量内存部分获得广播和缓存效果。

还要注意，内存分配、事件创建、事件销毁和设备内存释放现在都在主循环之外完成。此类 CUDA API 调用在 CPU 时间方面实际上非常昂贵。通过这一简单更改，该程序的 CPU 负载会显著降低。始终尝试在开始时设置好一切，并在结束时销毁或释放它们。永远不要在循环体中执行此操作，否则会大大减慢应用程序速度。

### 常量问题

- 1. 如果您有一个大小为 16 K 的数据结构，每个块的访问模式是随机的，但每个 warp 的访问模式是统一的，那么将其放入寄存器、常量内存还是共享内存最好？为什么？

### 常量答案

- 1. 尽管将大型数组放入寄存器有点棘手，但按线程对寄存器进行分块可以实现最快的访问，无论访问模式如何。但是，每个 SM 的寄存器空间受限于 32 K（compute < 1.2）、64 K（compute 1.2、1.3）、128 K（compute 2.x）或 256 K（compute 3.x）。您必须按每个线程的基础分配其中一部分作为工作寄存器。在 Fermi 上，每个线程最多可有 64 个寄存器，因此如果分配 32 个给数据、32 个作为工作集，您将只有 128 个活动线程，即四个活动 warp。一旦程序访问片外内存（例如全局内存），延迟可能会导致 SM 停滞。因此，内核需要在寄存器块上具有较高的操作比率，这才是一个好的解决方案。

将其放入共享内存可能是最佳情况，尽管取决于实际访问模式，您可能会看到共享内存银行冲突。统一的 warp 访问将允许从共享内存向单个 warp 中的所有线程广播。只有当两个块中的 warp 访问同一银行时，才会发生共享内存冲突。但是，16 K 的共享内存将完全占用 compute 1.x 设备上一个 SM 的共享内存，并在 compute 2.x/3.x 硬件上将您限制为最多三个块。

在 compute 1.x 设备上，常量内存也是一个合理的选择。常量内存的好处是可以向线程广播。但是，16 K 的数据可能会淹没缓存内存。而且，更重要的是，常量缓存针对线性访问进行了优化，也就是说，它在单次访问时会获取缓存行。因此，原始访问附近的访问会被缓存。访问未缓存的缓存行会导致缓存未命中惩罚，其大小大于没有缓存未命中的全局内存获取。

在 compute 2.x/3.x 设备上，全局内存可能更快，因为每个 warp 的统一访问应由编译器转换为统一的 warp 级全局内存访问。这提供了常量内存在 compute 1.x 设备上本应提供的广播访问。

### 全局内存

全局内存可能是内存类型中最有趣的一种，因为它是您绝对必须理解的一种。GPU 全局内存之所以是全局的，是因为它可以从 GPU 和 CPU 两端写入。实际上，它可以从 PCI-E 总线上的任何设备访问。GPU 卡可以直接相互传输数据，而不需要 CPU。这种对等功能是在 CUDA 4.x SDK 中引入的，但尚未在所有平台上支持。目前，Windows 7/Vista 平台仅通过 TCC 驱动程序模型在 Tesla 硬件上受支持。使用 Linux 或 Windows XP 的用户可以在消费级卡和 Tesla 卡上使用此功能。

GPU 的内存可以通过以下三种方式之一供 CPU 主机处理器访问：

- 通过阻塞传输显式访问。
- 通过非阻塞传输显式访问。
- 使用零内存复制隐式访问。

GPU 设备上的内存位于 PCI-E 总线的另一侧。这是一个双向总线，理论上每个方向支持高达 8 GB/s（PCI-E 2.0）的传输。在实践中，PCI-E 带宽通常每个方向为 4–5 GB/s。具体取决于您使用的硬件，

