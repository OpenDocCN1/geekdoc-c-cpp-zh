

值得评论一下主机与设备之间的同步。请注意，在非托管示例中，同步 cudaMemcpy() 例程既用于同步内核（即，等待其运行完成），也用于将数据传输到主机。Unified Memory 示例不调用 cudaMemcpy()，因此在主机程序可以安全使用 GPU 输出之前，需要显式调用 cudaDeviceSynchronize()。

### K.1.3. 数据迁移与一致性

Unified Memory 尝试通过将数据迁移到正在访问它的设备来优化内存性能（即，如果 CPU 正在访问，则将数据移动到主机内存；如果 GPU 将访问，则移动到设备内存）。数据迁移是 Unified Memory 的基础，但对程序是透明的。系统会尝试将数据放置在可以最有效地访问且不违反一致性的位置。

数据的物理位置对程序不可见，并且可能随时更改，但对数据虚拟地址的访问将从任何处理器保持有效且一致，无论局部性如何。请注意，保持一致性是首要要求，性能次之；在主机操作系统的限制范围内，系统被允许失败访问或移动数据，以便在处理器之间保持全局一致性。

计算能力低于 6.x 的 GPU 架构不支持将托管数据按需以细粒度移动到 GPU。每当启动 GPU 内核时，所有托管内存通常都必须传输到 GPU 内存，以避免内存访问时发生故障。使用计算能力 6.x 时，引入了一种新的 GPU 页面故障机制，提供了更无缝的 Unified Memory 功能。结合系统范围的虚拟地址空间，页面故障提供了多种好处。首先，页面故障意味着 CUDA 系统软件不需要在每次内核启动之前将所有托管内存分配同步到 GPU。如果在 GPU 上运行的内核访问其内核中不驻留的页面，它会发生故障，从而允许页面按需自动迁移到 GPU 内存。或者，页面可以映射到 GPU 地址空间，通过 PCIe 或 NVLink 互连进行访问（按需映射有时比迁移更快）。请注意，Unified Memory 是系统范围的：GPU（和 CPU）可以从 CPU 内存或系统中其他 GPU 的内存对内存页面发生故障并迁移。

### K.1.4. GPU 内存超额订阅

计算能力低于 6.x 的设备不能分配超过 GPU 物理内存大小的托管内存。

计算能力 6.x 的设备扩展了寻址模式以支持 49 位虚拟寻址。这足以覆盖现代 CPU 的 48 位虚拟地址空间，以及 GPU 自己的内存。大虚拟地址空间和页面故障功能使应用程序可以访问整个系统虚拟内存，不受任何单个处理器物理内存大小的限制。这意味着应用程序可以超额订阅内存系统：换句话说，它们可以分配、访问和共享大于系统总物理容量的数组，从而实现对超大数据集的外核处理。只要有足够的系统内存可用于分配，cudaMallocManaged 就不会耗尽内存。

### K.1.5. 多 GPU

对于计算能力低于 6.x 的设备，托管内存分配的行为与使用 cudaMalloc() 分配的非托管内存相同：当前活动设备是物理分配的主机，所有其他 GPU 都接收到内存的对等映射。这意味着系统中的其他 GPU 将通过 PCIe 总线以降低的带宽访问内存。请注意，如果系统中 GPU 之间不支持对等映射，则托管内存页面将放置在 CPU 系统内存（“零拷贝”内存）中，所有 GPU 都将经历 PCIe 带宽限制。有关详细信息，请参阅 pre-6.x 架构上的多 GPU 程序托管内存。

在具有计算能力 6.x 设备的系统上，托管分配对所有 GPU 可见，并可以按需迁移到任何处理器。Unified Memory 性能提示（请参阅性能调优）允许开发人员探索自定义使用模式，例如跨 GPU 的数据读取复制以及在不迁移的情况下直接访问对等 GPU 内存。

### K.1.6. 系统分配器

计算能力 7.0 的设备支持通过 NVLink 进行地址转换服务（ATS）。如果由主机 CPU 和操作系统支持，ATS 允许 GPU 直接访问 CPU 的页表。GPU MMU 中的未命中将导致向 CPU 发出地址转换请求（ATR）。CPU 在其页表中查找该地址的虚拟到物理映射，并将转换结果提供回 GPU。ATS 为 GPU 提供对系统内存的完全访问权限，例如使用 malloc 分配的内存、在堆栈上分配的内存、全局变量和文件支持的内存。应用程序可以通过检查新的 pageableMemoryAccessUsesHostPageTables 属性来查询设备是否支持通过 ATS 连贯地访问可分页内存。

以下是适用于满足 Unified Memory 基本要求的任何系统的示例代码（请参阅系统要求）：

```
int *data;
cudaMallocManaged(&data, sizeof(int) * n);
kernel<<<grid, block>>>(data);
```

具有 pageableMemoryAccess 属性的系统支持这些新的访问模式：

```
int *data = (int*)malloc(sizeof(int) * n);
kernel<<<grid, block>>>(data);
```

```
int data[1024];
kernel<<<grid, block>>>(data);
```

```
extern int *data;
kernel<<<grid, block>>>(data);
```

在上面的示例中，data 可能由第三方 CPU 库初始化，然后由 GPU 内核直接访问。在具有 pageableMemoryAccess 的系统上，用户还可以使用 cudaMemPrefetchAsync 将可分页内存预取到 GPU。这可以通过优化数据局部性来带来性能优势。

通过 NVLink 的 ATS 目前仅在 IBM Power9 系统上受支持。

### K.1.7. 硬件一致性

第二代 NVLink 允许 CPU 到每个 GPU 内存的直接加载/存储/原子访问。结合新的 CPU 主控功能，NVLink 支持一致性操作，允许从 GPU 内存读取的数据存储在 CPU 的缓存层次结构中。来自 CPU 缓存的较低访问延迟对 CPU 性能至关重要。计算能力 6.x 的设备仅支持对等 GPU 原子操作。计算能力 7.x 的设备可以通过 NVLink 发送 GPU 原子操作，并在目标 CPU 上完成它们，因此第二代 NVLink 增加了对由 GPU 或 CPU 发起的原子操作的支持。

请注意，cudaMalloc 分配的内存不可从 CPU 访问。因此，为了利用硬件一致性，用户必须使用 Unified Memory 分配器，例如 cudaMallocManaged 或带有 ATS 支持的系统分配器（请参阅系统分配器）。新属性 directManagedMemAccessFromHost 指示主机是否可以在不迁移的情况下直接访问设备上的托管内存。默认情况下，对驻留在 GPU 内存中的 cudaMallocManaged 分配的任何 CPU 访问都将触发页面故障和数据迁移。应用程序可以使用 cudaMemAdviseSetAccessedBy 内存访问提示与 cudaCpuDeviceId 来在受支持的系统上启用对 GPU 内存的直接访问。

请参阅以下示例代码：

```
__global__ void write(int *ret, int a, int b) {
    ret[threadIdx.x] = a + b + threadIdx.x;
}
__global__ void append(int *ret, int a, int b) {
    ret[threadIdx.x] += a + b + threadIdx.x;
}
int main() {
    int *ret;
    cudaMallocManaged(&ret, 1000 * sizeof(int));
    cudaMemAdvise(ret, 1000 * sizeof(int), cudaMemAdviseSetAccessedBy,
    cudaCpuDeviceId); // set direct access hint
    write<<< 1, 1000 >>>(ret, 10, 100); // pages populated in GPU memory
    cudaDeviceSynchronize();
    for(int i = 0; i < 1000; i++)
    printf("%d: A=%d =%d\n", i, ret[i]); // directManagedMemAccessFromHost=1: CPU accesses GPU memory directly without migrations
    // directManagedMemAccessFromHost=0: CPU faults and triggers device-to-host migrations
    append<<< 1, 1000 >>>(ret, 10, 100); // directManagedMemAccessFromHost=1: GPU accesses GPU memory without migrations
    cudaDeviceSynchronize(); // directManagedMemAccessFromHost=0: GPU faults and triggers host-to-device migrations
    cudaFree(ret);
    return 0;
}

