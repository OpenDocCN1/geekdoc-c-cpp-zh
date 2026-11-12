

一个端口。C++ Boost 库支持一个通用的线程包 thread，它为 Linux 和 Windows 都提供支持。

CPU 线程与我们在执行内核时使用的 GPU 线程类似，只不过它们不像 GPU 线程那样以组或 warp 的方式执行。GPU 线程通过共享内存进行通信，并显式同步以确保每个线程都读取/写入了该内存。共享内存局限于某个 SM，这意味着线程理论上只能与同一 SM 内的其他线程通信。由于 block 是调度到 SM 的单位，线程通信实际上被限制在每个 block 的范围内。

CPU 上的进程可以类比为 GPU 上的 block。进程被调度到 N 个 CPU 核心中的一个上运行。block 被调度到 GPU 上的 N 个 SM 中的一个上运行。从这个意义上说，SM 就像 CPU 核心。

CPU 进程可以通过同一插槽上的主机内存相互通信。然而，由于进程使用独立的内存空间，这种通信只有在第三方进程间通信库的协助下才能实现，因为任一进程都无法物理上查看另一进程的地址空间。然而，GPU block 的情况并非如此，因为它们访问 GPU 全局内存上的共同地址空间。

使用共享主机内存的多 CPU 系统也可以通过此共享主机内存相互通信，但同样需要第三方进程间通信库的帮助。多个 GPU 可以在同一主机上相互通信，使用主机内存，或者自 CUDA SDK 4.0 起，直接通过 PCI-E 总线的点对点通信模型进行通信。不过请注意，点对点通信仅支持使用 Fermi 或更高版本显卡的 64 位操作系统。对于 Windows，这仅通过 TCC（Tesla 计算集群）驱动程序支持，这实际上意味着它仅支持 Tesla 显卡。

然而，一旦 CPU 核心/插槽之间无法再使用共享主机内存，你就被迫使用其他网络传输机制（如 TCP/IP、InfiniBand 等）。此类通信的标准已成为 MPI（消息传递接口）。还有诸如 ZeroMQ（0MQ）之类的替代方案，虽然不那么广为人知，但同样有效。

请注意，这两者在单个主机节点内部通信时都使用共享主机内存传输。然而，支持线程的模型（例如 pthreads、ZeroMQ）进行线程间通信的速度远快于基于进程模型（如 MPI）的模型。

我们在此将重点放在只有一个 CPU 插槽、运行单线程 CPU 程序且存在多个 GPU 的情况。这是消费级硬件中最常见的用例，因此也是最值得涵盖的用例。有关多个 GPU 之间点对点传输等更高级主题，请参见第 10 章。

## 流

流是 GPU 上的虚拟工作队列。它们用于异步操作，即当你希望 GPU 独立于 CPU 运行时。某些操作会隐式导致同步点，例如，默认的主机与设备之间的内存拷贝。在大多数情况下，这就是程序想要的，即在将结果从 GPU 拷贝回后，他们会立即在 CPU 上对这些结果进行某些操作。如果结果是部分出现，那么应用程序在调试或单步执行时会工作，但在全速运行时会失败——这是一个调试噩梦。

通过创建流，你可以将工作和事件推入流中，流会按推入的顺序执行工作。流和事件与创建它们的 GPU 上下文相关联。因此，为了展示如何在多个 GPU 上创建几个流和事件，我们将设置一个小程序来演示这一点。

```
void fill_array(u32 * data, const u32 num_elements)
{
    for (u32 i=0; i < num_elements; i++)
    {
        data[i] = i;
    }
}
```

在第一个函数中，我们只是用 0 到 num_elements 的值填充数组。第二个函数只是检查 GPU 结果是否符合我们的预期。显然，在实际中，这两个函数都会被替换为执行更有用操作的真实代码。

```
void check_array(char * device_prefix,
                 u32 * data,
                 const u32 num_elements)
{
    bool error_found = false;

    for (u32 i=0; i < num_elements; i++)
    {
        if (data[i] != (i*2))
        {
            printf("%sError: %u %u\n",
                   device_prefix,
                   i,
                   data[i]);
            error_found = true;
        }
    }

    if (error_found == false)
        printf("%sArray check passed\n", device_prefix);
}
```

```
__global__ void gpu_test_kernel(u32 * data)
{
    const int tid = (blockIdx.x * blockDim.x)
                    + threadIdx.x;
    data[tid] *= 2;
}
```

接下来我们声明内核函数本身。它只不过是将每个数据元素乘以 2。这并不十分有用，但只是我们可以轻松检查的东西，以确保数组的每个元素都已被正确处理。

```
// Define maximum number of supported devices
#define MAX_NUM_DEVICES (4)

// Define the number of elements to use in the array
#define NUM_ELEM (1024*1024*8)

// Define one stream per GPU
cudaStream_t stream[MAX_NUM_DEVICES];

// Define a string to prefix output messages with so
// we know which GPU generated it
char device_prefix[MAX_NUM_DEVICES][300];

// Define one working array per device, on the device
u32 * gpu_data[MAX_NUM_DEVICES];

// Define CPU source and destination arrays, one per GPU
u32 * cpu_src_data[MAX_NUM_DEVICES];
u32 * cpu_dest_data[MAX_NUM_DEVICES];
```

最后，我们来到程序的主体部分。这个函数声明了一系列值，每个值都由 device_num 索引。这使我们能够对每个设备使用相同的代码，只需递增索引即可。

```
// Host program to be called from main
__host__ void gpu_kernel(void)
{
// No dynamic allocation of shared memory required
// const int shared_memory_usage = 0;

// Define the size in bytes of a single GPU's worth
// of data
const size_t single_gpu_chunk_size = (sizeof(u32) *
NUM_ELEM);

// Define the number of threads and blocks to launch
const int num_threads = 256;
const int num_blocks = ((NUM_ELEM + (num_threads-1))
/ num_threads);

// Identify how many devices and clip to the maximum
// defined
int num_devices;
CUDA_CALL(cudaGetDeviceCount(&num_devices));

if (num_devices > MAX_NUM_DEVICES)
    num_devices = MAX_NUM_DEVICES;
}
```

第一项任务是通过 cudaGetDeviceCount 调用识别我们可用的 GPU 数量。为确保数量不超过计划，该数字会被截断到最大支持值，即一个简单的 #define。考虑到四张双 GPU 卡，八会比这里选取的四更好的最大值。

```
// Run one memcpy and kernel on each device
for (int device_num=0;
     device_num < num_devices;
     device_num++)
{
    // Select the correct device
    CUDA_CALL(cudaSetDevice(device_num));
```

每个循环的第一部分将当前设备上下文设置为 device_num 参数，以确保所有后续调用都与该设备一起工作。

```
// Generate a prefix for all screen messages
struct cudaDeviceProp device_prop;
CUDA_CALL(cudaGetDeviceProperties(&device_prop,
                                  device_num));

sprintf(device_prefix[device_num], "\nID:%d %s", device_num, device_prop.name);

// Create a new stream on that device
CUDA_CALL(cudaStreamCreate(&stream[device_num]));

// Allocate memory on the GPU
CUDA_CALL(cudaMalloc((void**)&gpu_data[device_num],
                     single_gpu_chunk_size));

// Allocate page locked memory on the CPU
CUDA_CALL(cudaMallocHost((void **)
                        &cpu_src_data[device_num],
                         single_gpu_chunk_size));

CUDA_CALL(cudaMallocHost((void **)
                        &cpu_dst_data[device_num],
                         single_gpu_chunk_size));

// Fill it with a known pattern
fill_array(cpu_src_data[device_num], NUM_ELEM);

// Copy a chunk of data from the CPU to the GPU
// asynchronous
```

