

![](img/e0b192dbaf05f61ad420bee512a8c4e4_285_0.png)

图 8.1 2012年8月计算级别的消费者分布。

参数 device_num 是从零（默认设备）到系统中设备数量的一个数字。要查询设备数量，只需使用以下调用：

```
cudaError_t cudaGetDeviceCount(int * device_count);
```

```
CUDA_CALL(cudaGetDeviceCount(&num_devices));
```

请注意，在两个调用中我们都使用了在第 4 章中开发的 CUDA_CALL 宏。它只是获取返回值，检查是否有错误，打印合适的错误消息，并在失败时退出。有关其工作原理的更多信息，请参见第 4 章中关于设置 CUDA 的内容。

现在我们知道有多少设备以及如何选择一个设备，问题是选择哪一个。为此，我们需要知道特定设备的详细信息。我们可以使用以下调用来查询：

```
cudaError_t cudaGetDeviceProperties(struct cudaDeviceProp * properties, int device);
```

```
struct cudaDeviceProp device_0_prop;
```

```
CUDA_CALL(cudaGetDeviceProperties(&device_0_prop, 0));
```

结构 properties 由表 8.1 所示的结构成员组成。其中并非全部都可能感兴趣，但某些成员会很重要。其中最重要的是主计算级别修订版和次计算级别修订版。还要注意此处存在 warpSize，这意味着不同设备的 warp 大小会有所变化，尽管在实践中，迄今发布的所有设备的 warp 大小均保持为 32。

在选择设备时，没有必要逐个检查每一项以确保它是特定用户程序所需的。你可以简单地用你想要的属性填充相同的结构（0 表示不关心），并让 CUDA 运行时为你选择合适的设备。例如：

```
struct cudaDeviceProp device_prop;
int chosen_device;
```

```
memset(&device_prop, 0, sizeof(cudaDeviceProp));
device_prop.major = 2;
device_prop.minor = 0;
```

**表 8.1 设备属性详解**

| 结构成员 | 含义 | 仅限 Tesla | 单位 |
|---|---|---|---|
| char name[256]; | 设备名称，例如 GTX460。 | | 字符串 |
| size_t totalGlobalMem; | 设备上存在的全局内存最大量。 | | 字节 |
| size_t sharedMemPerBlock; | 每个块支持的共享内存最大量。 | | 字节 |
| int regsPerBlock; | 每个块允许的寄存器最大数量。 | | 寄存器 |
| int warpSize; | 设备的 warp 大小。 | | 线程 |
| size_t memPitch; | 使用分步分配内存的 memcpy 操作支持的最大步距。 | | 字节 |
| int maxThreadsPerBlock; | 每个块支持的线程最大数量。 | | 线程 |
| int maxThreadsDim[3]; | 每个维度支持的线程最大数量。 | | 线程 |
| int maxGridSize[3]; | 每个维度的块最大数量。 | | 块 |
| int clockRate; | GPU 的时钟频率，单位为 KHz。 | | KHz |
| size_t totalConstMem; | 设备上可用的常量内存最大量。 | | 字节 |
| int major; | 主计算修订版。 | | 整数 |
| int minor; | 次计算修订版。 | | 整数 |
| size_t textureAlignment; | 纹理所需的最小对齐。 | | 字节 |
| int deviceOverlap; | 如果设备支持重叠内存传输和内核，则设置为 1（已弃用）。 | | 标志 |
| int multiProcessorCount; | 设备上存在的 SM 数量。 | | 整数 |
| int kernelExecTimeoutEnabled; | 如果启用了内核超时功能（默认启用），则设置为 1。 | | 标志 |
| int integrated; | 如果设备是集成设备（即直接共享 CPU 内存的设备），则设置为 1。 | | 标志 |
| int canMapHostMemory; | 如果设备可以将 CPU 主机内存映射到 GPU 虚拟内存空间，则设置为 1。 | | 标志 |
| int computeMode; | 当前计算模式 cudaComputeModeDefault、cudaComputeModeExclusive、cudaComputeModeProhibited。允许共享设备、独占访问设备，或指定是否禁止设备访问。 | x | 枚举 |
| int maxTexture1D; | 支持的最大 1D 纹理大小。 | | 字节 |
| int maxTexture2D[2]; | 支持的最大 2D 纹理大小。 | | 字节 |
| int maxTexture3D[3]; | 支持的最大 3D 纹理大小。 | | 字节 |
| int maxTexture1DLayered[2]; | 最大 1D 分层纹理维度。 | | 字节 |
| int maxTexture2DLayered[3]; | 最大 2D 分层纹理维度。 | | 字节 |
| size_t surfaceAlignment; | 表面的对齐要求。 | | 字节 |
| int concurrentKernels; | 如果支持来自同一上下文的并发内核，则设置为 1。 | | 标志 |
| int ECCEnabled; | 如果启用了 ECC 内存，则设置为 1。 | x | 标志 |
| int pciBusID; | 设备的 PCI 总线 ID。 | | 整数 |
| int pciDeviceID; | 设备的 PCI 设备 ID。 | | 整数 |
| int pciDomainID; | 设备的 PCI 域 ID。 | | 整数 |
| int tccDriver; | 如果启用了 TCC 驱动程序模式，则设置为 1。 | x | 标志 |
| int asyncEngineCount; | 设备上存在的异步复制引擎数量。 | x* | 整数 |
| int unifiedAddressing; | 如果设备和主机共享统一地址空间，则设置为 1。 | x** | 标志 |
| int memoryClockRate; | 支持的内存时钟频率，单位为 kHz。 | | kHz |
| int memoryBusWidth; | 内存总线宽度，单位为位。 | | 位 |
| int l2CacheSize; | 二级（L2）缓存的大小（0 = 不存在）。 | | 字节 |
| int maxThreadsPerMultiProcessor; | 单个 SM 上支持的线程最大数量。 | | 线程 |

* 双复制引擎仅在 Tesla 设备上受支持。消费级设备仅限支持单个复制引擎。
† 统一寻址在 64 位平台上受支持。在 Windows 上，它需要 TCC 驱动程序，而 TCC 驱动程序又需要 Tesla 卡。在 UNIX 平台上则不是这种情况。

```
if (cudaChooseDevice(&chosen_device, device_prop) != cudaErrorInvalidValue)
{
    CUDA_CALL(cudaSetDevice(chosen_device));
}
```

在此代码中，我们创建一个设备属性结构，使用 memset 调用将其清零，然后请求计算 2.0 设备（任何 Fermi 设备）。然后我们要求 CUDA 将上下文设置为指定设备。

## 单节点系统

在 4.0 SDK 之前的 CUDA 版本中，单节点系统是唯一可用的多 GPU 模型，如图 8.2 所示。一个基于 CPU 的任务将与一个单 GPU 上下文关联。此上下文中的任务可以是进程或线程。在幕后，CUDA 运行时将 CPU 进程/线程 ID 绑定到 GPU 上下文。因此，所有后续的 CUDA 调用（例如 cudaMalloc）都将在绑定到此上下文的设备上分配内存。

这种方法有许多缺点，但也有一些优点。从编程角度来看，主机端的进程/线程模型因操作系统类型而碎片化。进程是在 CPU 上作为独立可调度单元运行并拥有自己的数据空间的程序。为了节省内存，同一进程的多个实例通常共享代码空间，操作系统为每个进程维护一组寄存器（或上下文）。

相比之下，线程是 CPU 调度中一个更轻量级的元素。它共享其父进程使用的代码和数据空间。然而，与进程一样，每个线程都需要操作系统维护一个状态（指令指针、堆栈指针、寄存器等）。

线程可以与同一进程中的其他线程通信和协作。进程可以通过进程间通信与其他进程通信和协作。进程间的此类通信可能在 CPU 核心内、CPU 插槽内、CPU 节点内、机架内、计算机系统内，甚至在计算机系统之间进行。

实际 API 取决于通信级别和操作系统。Windows 上使用的 API 与 Linux 上使用的 API 完全不同。POSIX 线程（或 pthreads）是 Linux 上常用的线程模型。Windows 上不原生支持此模型，尽管它可作为

![](img/e0b192dbaf05f61ad420bee512a8c4e4_288_0.png)

**图 8.2** 多客户端，多服务器。

