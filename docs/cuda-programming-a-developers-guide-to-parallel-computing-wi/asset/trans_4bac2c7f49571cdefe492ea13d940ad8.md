

![](img/e0b192dbaf05f61ad420bee512a8c4e4_350_0.png)

### 图 9.13 设备间的传输速度（AMD Phenom II X4 905e，PCI-E 2.0 X8 链路）。

为进行比较，我们在测试的多个系统中，也在图 9.14、9.15 和 9.16 中显示了结果。

图 9.14 展示了一款基于英特尔低功耗 Atom 设备的小型上网本，配备了独立的 GT218 NVIDIA ION 显卡。您通常能看到的峰值 PCI-E 带宽可高达

![](img/e0b192dbaf05f61ad420bee512a8c4e4_350_1.png)

### 图 9.14 设备间的传输速度（Intel Atom D525，PCI-E 2.0 X1 链路）。

![](img/e0b192dbaf05f61ad420bee512a8c4e4_351_0.png)

### 图 9.15 设备间的传输速度（Intel i3 540，PCI-E X16 链路）。

to 5 GB/s when using a 2.0 X16 link. As this netbook uses an X1 link, we could expect a maximum of 320 MB/s and we see in the order of 200 MB/s.
However, we see a very similar pattern to the AMD system, in that we need around 2 MB plus transfer sizes before we start to achieve anything like the peak transfer rate. The only difference we see is there is a notable difference between transfers to the device and transfers from the device.

![](img/e0b192dbaf05f61ad420bee512a8c4e4_351_1.png)

### 图 9.16 设备间的传输速度（Intel i7 920，PCI-E X16 链路）。

在消费环境中相当常见的中端系统是英特尔的 i3/i5 系统。此特定系统是搭载 H55 芯片组的 i3 540。由于该设备只有一个 GPU，它以 PCI-E 2.0 的 X16 峰值速度运行（图 9.15）。

我们再次可以看到固定内存传输和非固定内存传输之间非常大的差异，超过 2 倍。不过，请注意绝对速度差异，大约比 AMD 系统提高 2 倍。这主要是因为 AMD 系统使用 X8 PCI-E 链路，而此处的 Intel 系统使用 X16 PCI-E 链路。

英特尔 i3 是典型的消费级处理器。任何编写消费类应用程序的人现在都应该非常清楚，他们需要使用固定内存传输，因为我们可以看到它带来的巨大差异。

最后，我们再看一个系统，这次来自服务器领域，使用英特尔 i7 920 Nehalem 处理器和华硕超级计算机插槽 1366 主板。这是一款常用于非常高端 GPU 的主板，因为它允许最多四个 PCI-E 插槽。此特定系统配备了 3 块 GTX290 GPU，每块均使用 PCI-E 2.0 X16 连接。

从图中看到的再次很有趣。分页内存传输和固定内存传输在传输大小超过 512 KB 之前是相等的，之后固定内存传输比基于分页内存的传输快多达 1.8 倍。与 Nehalem i3 系统不同，请注意 Nehalem i7 系统更加一致，入站和出站传输速度之间没有巨大差异。不过，还要注意峰值传输速度，尽管两台设备都在 X16 PCI-E 2.0 链路上，但仅为 5400 MB/s，而 i3 达到了 6300 MB/s 的峰值（图 9.16）。

总而言之，我们可以说，在当今计算硬件的多种选择中，固定内存传输大约比非固定内存传输快两倍。我们还看到，从和到各种设备的读写速度之间可能存在相当大的性能差异。我们还可以看到，需要使用较大而非较小的块大小，或许可以合并多次传输以提高总线的整体带宽利用率。

## 零拷贝内存

零拷贝内存是一种特殊的内存映射形式，允许您将主机内存直接映射到 GPU 的内存空间中。因此，当您在 GPU 上解引用内存时，如果它是基于 GPU 的，则可以获得高达 180 GB/s 的全局内存带宽。如果 GPU 代码读取主机映射变量，它会发出 PCI-E 读取事务，很长一段时间后主机会通过 PCI-E 总线返回数据。

在查看了上一节中的 PCI-E 总线带宽后，乍一看这似乎不太合理。大传输效率高，小传输效率低。如果我们重新使用之前示例中使用的测试程序，可以看到在我们的示例 AMD Phenom X4 平台上，中位传输时间为 0.06 ms。然而，这些是显式的单独传输，因此零拷贝实现可能更高效。

如果您考虑访问全局内存时会发生什么，在计算能力 2.x 硬件上，整个缓存行会从内存中加载。即使在计算能力 1.x 硬件上，相同的 128 字节（可能减少到 64 或 32）也会从全局内存中获取。

NVIDIA 未公布其使用的 PCI-E 传输大小，或零拷贝实际实现的详细信息。然而，用于全局内存的合并访问方法也可用于 PCI-E 传输。线程束（warp）内存延迟隐藏模型同样可应用于 PCI-E 传输，前提是有足够的算术密度来隐藏 PCI-E 传输的延迟。事实上，这是使其工作的关键。如果您对每次全局内存获取做的工作很少，且您的应用程序已经受内存限制，那么这种方法不太可能帮助您。

然而，如果您的应用程序受算术限制，零拷贝内存可以是一种非常有用的技术。它为您节省了向设备和从设备进行显式传输的时间。实际上，您无需进行显式流管理，就能将计算与数据传输重叠。当然，问题在于您需要高效地使用数据。如果您多次获取或写入同一数据点，这将创建多个 PCI-E 事务。由于每个事务在延迟方面都很昂贵，事务越少越好。

这在主机和 GPU 共享相同内存空间的系统上也非常有效，例如基于低端 NVIDIA ION 的笔记本电脑。在这里，GPU 上的全局内存 malloc 实际上会导致主机上的内存 malloc。显然，从主机的一个内存区域复制到主机的另一个内存区域没有意义。零拷贝内存可以消除此类系统中执行这些复制的需求，而无需承受 PCI-E 总线传输的影响。

零拷贝内存传输还有一个非常有用的用例。即在最初将 CPU 应用程序移植到 GPU 的阶段。在开发阶段，主机上通常会存在尚未移植到 GPU 的代码部分。通过将此类数据引用声明为零拷贝内存区域，可以分段移植代码并使其正常工作。在所有预期部分都出现在 GPU 之前，性能通常会很差。它只是允许以较小的步骤完成此操作，因此不是“全有或全无”的问题。

让我们从现有的 memcpy 程序开始，扩展内核以执行数据读取，而不是依赖显式复制。为此，我们绝对必须合并对内存的访问，读取简单的一维数组时这很容易。因此，我们的内核变为

```
__global__ void kernel_copy(u32 * const gpu_data,
                                const u32 * const host_data,
                                const u32 num_elements)
{
    const u32 idx = (blockIdx.x * blockDim.x) + threadIdx.x;
    const u32 idy = (blockIdx.y * blockDim.y) + threadIdx.y;
    const u32 tid = ((gridDim.x * blockDim.x) * idy) + idx;

    if (tid < num_elements)
        gpu_data[tid] = host_data[tid];
}
```

在内核中，我们只是将 x 和 y 网格维度转换为单个线性数组，并将源数据集中的一个元素分配给目标数据集。接下来，要使用零拷贝或主机映射内存，必须完成三个关键步骤：第一，启用它；第二，使用它分配内存；最后，将常规主机指针转换为设备内存空间。

在创建任何 CUDA 上下文之前，我们需要进行以下调用：

```
// Enable host mapping to device memory
CUDA_CALL(cudaSetDeviceFlags(cudaDeviceMapHost));
```

创建 CUDA 上下文时，驱动程序将知道它还需要支持主机映射内存。如果没有此设置，主机映射（零拷贝）内存将无法工作。如果...，这将无法工作。
