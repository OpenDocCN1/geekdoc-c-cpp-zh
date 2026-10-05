

# 表面内存 (Surface Memory)

表面内存与纹理具有相似之处，包括硬件加速功能和空间访问优化。
然而，它支持写操作，使其成为需要“读-修改-写”循环任务的多用途工具，例如原地图像编辑或涉及动态数据更新的模拟。

# 特性

与纹理内存不同，表面内存允许读和写操作，便于需要进行就地数据处理的算法。
硬件插值：它继承了纹理内存的硬件插值和灵活寻址模式，使其适用于类似的空间局部化数据访问模式，但增加了修改数据的能力。

# 应用

表面内存对于需要动态纹理更新的图形渲染流水线，或在模拟数据随时间演变的科学计算场景中特别有用。它的能力允许高效地实现对空间结构化数据进行频繁“读-修改-写”循环的算法。

# 示例

以下示例了如何使用表面内存对 2D 数据数组进行原地操作。这可以代表一个简化的图像处理算法，根据某些标准修改像素值。

```cpp
// Define surface reference
cudaSurfaceType2D surfRef; 
__global void factor(cudaSurfaceObject_t surfRef, float factor) {
    int x = blockIdx.x * blockDim.x + threadIdx.x;
    int y = blockIdx.y * blockDim.y + threadIdx.y;
    float data;
    // Read from the surface
    tex2DToArray(&data, surfRef, x, y);
    // Modify the data
    data *= factor; 
    // Write to the surface
    tex2DToArray(data, surfRef, x, y); 
}
int main() {
    // Create and bind surface
    cuArray_t cuArray;
    cudaChannelDesc channelDesc = cudaChannelDescToArray();
    int width, height; 
    cuArrayCreate(&cuArray, &channelDesc, width, height); 
    // Call kernel
    dim3 blocks(16, 16);
    dim3 grid((width + blocks.x - 1) / blocks.x, (height + blocks.y - 1) / blocks.y);
    factor<<<grid, blocks>>>(surfRef, 2.0f);
    // Clean up
}
```

在 CUDA 应用中理解并利用纹理和表面内存可以显著提高各种计算任务的性能，特别是涉及空间数据的任务。通过利用这些内存类型的独特功能，开发者可以实现优化的数据访问模式，并利用硬件加速更高效的计算。

# 4.10

# 统一内存 (Unified Memory)：简化内存管理

CUDA 演进过程中，旨在简化图形处理器（GPU）内存管理复杂性的关键进展之一是统一内存。该模型抽象了主机（CPU）和设备（GPU）之间内存的物理隔离，从而允许一个可以从 CPU 和 GPU 同时访问的统一内存视图。从本质上，统一内存允许开发者编写更少的代码来显式管理数据移动，从而提高了生产力，并使其能够更多地关注应用程序逻辑，而不是内存管理的细节。

统一内存通过利用托管内存空间实现了简单性，该空间由 NVIDIA 驱动程序根据访问模式和需求在主机和设备之间进行自动迁移。作为编程员，当使用统一内存 API 分配内存时，你就不再需要手动在主机和设备之间拷贝数据。统一内存封装的这种无缝数据迁移大幅提升了开发者的效率，特别是对于那些初接触 CUDA 编程的人来说。

# 分配统一内存

在统一内存空间中分配内存可以使用 `cudaMallocManaged` API。此调用动态分配可以从主机和 GPU 访问的内存，而不需要显式的数据传输命令。以下是操作方法：

```cpp
cudaError_t cudaMallocManaged(void **devPtr, size_t size, unsigned int flags);
```

`cudaMallocManaged` 函数接受三个参数：指向分配内存的指针、要分配的内存大小，以及一个决定内存附加行为的可选 `flags` 参数。通常使用 `cudaMemAttachGlobal` 标志，它指定分配的内存可以被支持统一内存的系统中所有 GPU 访问。

这是一个使用统一内存分配整数数组的示例：

```cpp
int *arr; size_t size = 100 * sizeof(int); cudaMallocManaged(&arr, size);
```

# 访问统一内存

从 GPU 或 CPU 访问统一内存非常简单，与访问任何动态分配的内存没有区别。CUDA 运行时会在后台处理任何必要的数据迁移。以下代码演示了如何从 CUDA 核函数访问统一内存：

```cpp
__global__ void kernel(int *arr, int value, int n) {
    int idx = threadIdx.x + blockIdx.x * blockDim.x;
    if (idx < n) { arr[idx] = value; }
}
```

需要注意的是，尽管统一内存简化了内存管理，但仍应优化访问模式。欠佳的访问模式会导致主机和设备之间频繁的数据迁移，引起性能下降。

# 同步与数据一致性

在启动访问统一内存的核函数后，必须确保主机和设备之间的数据一致性。CUDA 提供了 `cudaDeviceSynchronize` 函数，它会等待所有之前的设备活动完成，确保 GPU 进行的数据修改对主机可见，反之亦然。

尽管统一内存通过抽象数据移动极大地简化了内存管理，但开发者仍应该意识到底层内存访问模式及其对性能的影响。有效使用统一内存需要理解数据迁移何时以及如何发生，以及最小化开销的策略。尽管如此，对于许多应用程序，统一内存为 GPU 内存管理的复杂挑战提供了一个优雅且高效的解决方案，使开发者能够更多关注计算问题，而不是底层硬件的细节。

4.11

# 高效数据传输策略

主机（CPU）和设备（GPU）之间的数据传输是 CUDA 编程的一个关键方面。高效的数据传输对于实现 CUDA 应用的高性能至关重要，因为主机内存和设备内存之间的带宽通常是限制因素。在这一节中，我们将探索优化 CUDA 应用中数据传输的几种策略。

# 理解 PCIe 和内存带宽

为了优化数据传输，理解底层硬件至关重要。NVIDIA GPU 通过 PCIe（外设部件 Express）总线连接到 CPU。PCIe 总线有不同的代，每一代提供不同的数据传输速率。了解 PCIe 版本及其理论最大带宽对于估计数据传输的性能至关重要。

GPU 全局内存与其处理器之间的带宽远高于 CPU 和 GPU 之间 PCIe 的带宽。这种差异使得最小化 PCIe 上的数据传输以及确保必须传输的数据尽可能高效变得关键。

# 最小化数据传输

减少数据传输性能影响的一项基本策略是减少主机和设备之间需要传输的数据量。这涉及多种技术：

- 尽可能直接在设备上处理数据，以避免传回主机。
- 尽可能将数据传输与计算重叠。
- 构造应用程序以最大化设备上的数据重用，从而减少对数据传输的需求。

# 固定主机内存 (Pinning Host Memory)

为了实现更快速的数据传输，CUDA 允许分配固定（或页锁定）主机内存。固定内存不会被操作系统交换出，这使得主机和设备之间具有更高的传输率。

```cpp
size_t size;
cudaMallocHost(&ptr, size);
```

cudaMallocHost 是-从固定内存传输数据比可页内存更快，因为 GPU 可以通过 DMA（直接内存访问）直接访问固定内存，而跳过 CPU。

