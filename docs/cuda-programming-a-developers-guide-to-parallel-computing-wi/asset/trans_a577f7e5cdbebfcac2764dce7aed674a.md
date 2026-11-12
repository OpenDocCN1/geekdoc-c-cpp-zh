
和

```
cudaMemcpyPeerAsync( dest_device_ptr, dst_device_num, src_device_ptr, src_device_num,
num_bytes, stream );
```

最后，完成后，我们需要通过调用来禁用 P2P 访问的资源配置：

```
cudaDeviceDisablePeerAccess(device_num);
```

就性能而言，SimpleP2P 应用程序报告的速度为 2.4 GB/s，这与该特定测试系统（PCI-E 2.0 x8）上可用的峰值 3 GB/s 非常接近。

SDK 中的 SimpleP2P 示例程序提供了一些简单的模板代码，说明如何在实践中执行此操作。它在两个 GPU 之间进行一系列 GPU 传输，然后计算传输速度。有了这里介绍的背景知识，你应该能够阅读并遵循示例代码。

## asyncAPI 和 cudaOpenMP

asyncAPI SDK 示例提供了使用异步 API 的示例，但对于初次接触 CUDA 的人来说，其实并不十分容易理解。我们在文本中已经介绍过流和异步操作。这些对于让多 GPU 设置与 CPU 使用协同工作非常重要。因此，我们将查看此示例，看看它究竟做了什么。

asyncAPI 示例的基本前提是，它创建一个异步流，向其中放入一个到设备的内存拷贝、一个内核，最后是一个返回主机的内存拷贝。在此期间，它在 CPU 上运行一些代码，仅仅是计数递增，而 GPU 正在运行异步内核。

cudaOpenMP 示例展示了如何将 OpenMP 与 CUDA 一起使用。它识别 CPU 线程的数量，以及每个连接的 CUDA 设备的数量和名称。然后，它尝试为每个 GPU 设备生成一个线程，并共享不同设备的工作。

我们将在此提供一个类似的示例，融合了两个 SDK 示例，但对其进行了一些简化，并可能作为你自己的工作的模板代码更有用。

```
#include <stdio.h>
#include <omp.h>

#include "cuda_helper.h"
#include "cuda.h"

__global__ void increment_kernel(int * __restrict__ const data,
                                 const int inc_value,
                                 const int num_elem)
{
    const int idx = blockIdx.x * blockDim.x + threadIdx.x;

    // Check array index does not overflow the array
    if (idx < num_elem)
}
// Repeat N times - just to make the kernel take some time
const int repeat = 512;
for (int i=0; i < repeat; i++)
{
    data[idx] += inc_value;
}

// Max number of devices on any single node is, usually at most, eight
#define MAX_NUM_DEVICES 8

__host__ int main(int argc, char *argv[])
{
    const int num_elem = 1024 * 1024 * 16;
    const int size_in_bytes = num_elem * sizeof(int);
    const int increment_value = 1;
    const int loop_iteration_check = 1000000;
    const int shared_mem = 0;

    // Define the number of threads/blocks needed
    const int num_threads = 512;
    const int num_blocks = ((num_elem + (num_threads-1)) / num_threads);

    // One array element per CPU thread
    int host_counter[MAX_NUM_DEVICES];
    float delta_device_time[MAX_NUM_DEVICES];
    cudaDeviceProp device_prop[MAX_NUM_DEVICES];

    int num_devices;
    CUDA_CALL(cudaGetDeviceCount(&num_devices));
    printf("\nidentified %d devices. Spawning %d threads to calculate %d MB using (%dx%d)",
        num_devices, num_devices, ((size_in_bytes/1024)/1024), num_blocks, num_threads );

    // Declare thread private, per thread variables
    int * device_ptr[MAX_NUM_DEVICES];
    int * host_ptr[MAX_NUM_DEVICES];
    cudaEvent_t start_event[MAX_NUM_DEVICES], stop_event[MAX_NUM_DEVICES];
    cudaStream_t async_stream[MAX_NUM_DEVICES];

    // Create all allocations outside of OpenMP in series
    for (int device_num=0; device_num < num_devices; device_num++)
    {
        // Set the device to a unique device per CPU thread
        CUDA_CALL(cudaSetDevice(device_num));

        // Get the current device properties
        CUDA_CALL(cudaGetDeviceProperties(&device_prop[device_num], device_num));

        // Allocate the resources necessary
        CUDA_CALL(cudaMalloc((void **) &device_ptr[device_num], size_in_bytes));
        CUDA_CALL(cudaMallocHost((void **) &host_ptr[device_num], size_in_bytes));
        CUDA_CALL(cudaEventCreate(&start_event[device_num]));
        CUDA_CALL(cudaEventCreate(&stop_event[device_num]));
        CUDA_CALL(cudaStreamCreate(&async_stream[device_num]));
    }

    // Spawn one CPU thread for each device
    #pragma omp parallel num_threads(num_devices)
    {
        // Variables declared within the OpenMP block are thread private and per thread
        // Variables outside OpenMP block exist once in memory and are shared between
        // threads.

        // Get our current thread number and use this as the device number
        const int device_num = omp_get_thread_num();

        // Set the device to a unique device per CPU thread
        CUDA_CALL(cudaSetDevice(device_num));

        // Push start timer, memset, kernel, copy back and stop timer into device queue
        CUDA_CALL(cudaEventRecord(start_event[device_num], async_stream[device_num]));

        // Copy the data to the device
        CUDA_CALL(cudaMemsetAsync(device_ptr[device_num], 0, size_in_bytes,
            async_stream[device_num]));

        // Invoke the kernel
        increment_kernel<<<num_blocks, num_threads, shared_mem, async_stream[device_num]
            >>>(device_ptr[device_num], increment_value, num_elem);

        // Copy data back from the device
        CUDA_CALL(cudaMemcpyAsync(host_ptr[device_num], device_ptr[device_num],
            size_in_bytes, cudaMemcpyDeviceToHost,
            async_stream[device_num]));

        // Record the end of the GPU work
        CUDA_CALL(cudaEventRecord(stop_event[device_num], async_stream[device_num]));

        // Device work has now been sent to the GPU, so do some CPU work
        // whilst we're waiting for the device to complete its work queue

        // Reset host counter
        int host_counter_local = 0;
        int complete = 0;

        // Do some work on the CPU until all the device kernels complete
        do
        {
            // Insert useful CPU work here
            host_counter_local++;

            // Check device completion status every loop_iteration_check iterations
            if ( (host_counter_local % loop_iteration_check) == 0 )
            {
                // Assume everything is now complete
                complete = 1;

                // Check if all GPU streams have completed. Continue to do more CPU
                // work if one of more devices have pending work.
                for ( int device_check_num=0; device_check_num < num_devices;
                    device_check_num++)
                {
                    if ( cudaEventQuery(stop_event[device_check_num]) == cudaErrorNotReady )
                        complete = 0;
                }
            } while( complete == 0 );

            // Write out final result
            host_counter[device_num] = host_counter_local;

            // Calculate elapsed GPU time
            CUDA_CALL(cudaEventElapsedTime(&delta_device_time[device_num],
                start_event[device_num],
                stop_event[device_num]));
    } // End parallel region

    // Now running as a single CPU thread again

    // Free allocated resources
    // Create all the allocations outside of OpenMP in series
    for (int device_num=0; device_num < num_devices; device_num++)
    {
        // Set the device to a unique device per CPU thread
        CUDA_CALL(cudaSetDevice(device_num));

        CUDA_CALL(cudaStreamDestroy(async_stream[device_num]));
        CUDA_CALL(cudaEventDestroy(start_event[device_num]));
        CUDA_CALL(cudaEventDestroy(stop_event[device_num]));
        CUDA_CALL(cudaFreeHost(host_ptr[device_num]));
        CUDA_CALL(cudaFree(device_ptr[device_num]));
        // Reset the device for later use
        CUDA_CALL(cudaDeviceReset());
    }

    // Print a summary of the results
    for (int device=0; device < num_devices; device++)
    {
        printf("\nKernel Time for device %s:%d: %.2fms",
            device_prop[device].name, device, delta_device_time[device]);
        printf("\nCPU count for thread id: %d", device, host_counter[device]);
    }
}
```

SDK 示例中有几个点需要进一步讨论。首先，在 asyncAPI 示例中，使用的是流 0，即默认流。不幸的是，在许多情况下，默认流会导致流之间的隐式同步。你几乎肯定最终会使用双缓冲或三缓冲方法，而这种隐式同步会让你措手不及。使用异步操作时，请始终创建自己的流。

```
cudaStream_t async_stream[MAX_NUM_DEVICES];
CUDA_CALL(cudaSetDevice(device_num));
CUDA_CALL(cudaStreamCreate(&async_stream[device_num]));
```

你可能没有注意到的 asyncAPI 流示例中的第二点是，它获取元素数量 N，并直接将其除以线程数量以获取网格的块数量。碰巧 N 是线程数量的倍数，但如果不是呢？会发生什么情况呢？数组中的最后几个元素不会被 GPU 内核处理。对于刚开始学习 CUDA 的人来说，这可能根本不明显。如果你计划允许 N 不是线程数量的倍数，请始终使用以下公式生成块数量：

```
const int num_elem = 1024 * 1024 * 16;
const int num_threads = 512;
const int num_blocks = ((num_elem + (num_threads-1)) / num_threads);
```

在内核中，添加对数组越界的检查：

```
// Check array index does not overflow the array
if (idx < num_elem)
```

现在，这会产生将 num_elem 传递给内核并在内核内检查它的开销。如果你能保证始终使用线程数量的倍数，那么你可以避免需要此代码，并坚持使用更简单的 num_blocks = num_elem / num_threads 方法。大多数时候，作为程序员，我们可以说这是成立的，因为我们通常控制数据块大小。

现在，如果我们查看 cudaOpenMP 示例，如何启动多个 CPU 线程？它使用对 omp_set_num_threads 的调用：
