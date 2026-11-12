

此 API 遵循流排序语义，即迁移不会在流中所有先前操作完成之前开始，且流中任何后续操作也不会在迁移完成之前开始。

### K.3.2. 数据使用提示

当多个处理器需要同时访问同一数据时，仅靠数据预取是不够的。在这种情况下，应用程序提供关于数据实际使用方式的提示很有用。以下咨询 API 可用于指定数据用途：

```
cudaError_t cudaMemAdvise(const void *devPtr,
 size_t count,
 enum cudaMemoryAdvise advice,
 int device);
```

其中，**advice** 是针对从 **devPtr** 地址开始、长度为 **count** 字节（四舍五入到最近的页面边界）的内存区域中包含的数据而指定的，可取以下值：

- **cudaMemAdviseSetReadMostly:** 这意味着数据大部分情况下是读取，只有偶尔写入。这允许驱动程序在处理器访问该数据时，在该处理器的内存中创建数据的只读副本。同样，如果对该区域调用 **cudaMemPrefetchAsync**，它会在目标处理器上创建数据的只读副本。当处理器写入此数据时，除了写入发生的那一份副本外，对应页面的所有副本都将失效。对于此建议，**device** 参数将被忽略。此建议允许多个处理器以最大带宽同时访问同一数据，如以下代码片段所示：

```
char *dataPtr;
size_t dataSize = 4096;
// Allocate memory using malloc or cudaMallocManaged
data = (char *)malloc(dataSize);
// Set advice on the memory region
cudaMemAdvise(dataPtr, dataSize, cudaMemAdviseSetReadMostly, 0);
int outerLoopIter = 0;
while (outerLoopIter < maxOuterLoopIter) {
 // The data is written to in the outer loop on the CPU
 initializeData(dataPtr, dataSize);
 // Prefetching here makes available to all GPUs by prefetching.
 // Prefetch here causes read duplication of data instead
 // of data migration
 for (int device = 0; device < maxDevices; device++) {
 cudaMemPrefetchAsync(dataPtr, dataSize, device, stream);
 }
 // The kernel only reads this data in the inner loop
 int innerLoopIter = 0;
 while (innerLoopIter < maxInnerLoopIter) {
 kernel<<<32, 32>>>((const char *)dataPtr);
 innerLoopIter++;
 }
 outerLoopIter++;
}
```

- **cudaMemAdviseSetPreferredLocation:** 此建议将数据的首选位置设置为属于 **device** 的内存。为 **device** 传入 **cudaCpuDeviceId** 值将首选位置设置为 CPU 内存。设置首选位置不会立即导致数据迁移到该位置。相反，它在该内存区域发生故障时指导迁移策略。如果数据已在其首选位置，且发生故障的处理器可以在不需要迁移数据的情况下建立映射，则将避免迁移。另一方面，如果数据不在其首选位置，或无法建立直接映射，则它将迁移到访问它的处理器。需要注意的是，设置首选位置不会阻止使用 cudaMemPrefetchAsync 进行的数据预取。

- **cudaMemAdviseSetAccessedBy:** 此建议意味着数据将由 device 访问。这不会导致数据迁移，也不会本身影响数据的位置。相反，它会导致数据始终映射在指定处理器的页表中，只要数据的位置允许建立映射。如果数据因任何原因被迁移，映射将相应更新。在数据局部性不重要但避免故障很重要的场景中，此建议很有用。例如，考虑一个包含多个 GPU 且已启用对等访问的系统，其中位于一个 GPU 上的数据偶尔由其他 GPU 访问。在这种情况下，将数据迁移到其他 GPU 不那么重要，因为访问不频繁且迁移开销可能过高。但防止故障仍可帮助提高性能，因此预先设置映射很有用。需要注意的是，在 CPU 访问此数据时，数据可能会被迁移到 CPU 内存，因为 CPU 无法直接访问 GPU 内存。任何为此数据设置了 cudaMemAdviseSetAccessedBy 标志的 GPU 现在都会将其映射更新为指向 CPU 内存中的页面。

也可以使用以下值之一取消每个建议：cudaMemAdviseUnsetReadMostly、cudaMemAdviseUnsetPreferredLocation 和 cudaMemAdviseUnsetAccessedBy。

### K.3.3. 查询使用属性

程序可以使用以下 API 查询通过 cudaMemAdvise 或 cudaMemPrefetchAsync 分配的内存范围属性：

```
cudaMemRangeGetAttribute(void *data,
 size_t dataSize,
 enum cudaMemRangeAttribute attribute,
 const void *devPtr,
 size_t count);
```

此函数查询从 devPtr 开始、大小为 count 字节的内存范围的属性。内存范围必须引用通过 cudaMallocManaged 分配或通过 __managed__ 变量声明的托管内存。可以查询以下属性：

- **cudaMemRangeAttributeReadMostly:** 如果给定内存范围中的所有页面都启用了读取复制，则返回的结果将为 1，否则为 0。

- **cudaMemRangeAttributePreferredLocation:** 如果内存范围中的所有页面都将相应处理器作为其首选位置，则返回的结果将是 GPU 设备 ID 或 cudaCpuDeviceId，否则将返回 cudaInvalidDeviceId。应用程序可以使用此查询 API 根据托管指针的首选位置属性来决定通过 CPU 或 GPU 暂存数据。需要注意的是，查询时内存范围中页面的实际位置可能与首选位置不同。

- **cudaMemRangeAttributeAccessedBy:** 将返回为该内存范围设置了该建议的设备列表。

- **cudaMemRangeAttributeLastPrefetchLocation:** 将返回使用 cudaMemPrefetchAsync 显式预取的内存范围中所有页面的最后位置。需要注意的是，这只是返回应用程序请求将内存范围预取到的最后位置。它不指示到该位置的预取操作是否已完成甚至已开始。

此外，可以使用相应的 cudaMemRangeGetAttributes 函数查询多个属性。

## 注意

所有 NVIDIA 设计规范、参考板、文件、图纸、诊断、列表和其他文档（统称及分别称为“材料”）均按“原样”提供。NVIDIA 对材料不作任何明示、暗示、法定或其他方面的保证，并明确否认所有关于非侵权、适销性和特定用途适用性的暗示保证。

提供的信息被认为是准确可靠的。然而，NVIDIA 公司对使用此类信息的后果或因其使用而可能导致的任何专利或第三方其他权利的侵权不承担责任。未明示或默示授予 NVIDIA 公司任何专利权下的许可。本出版物中提到的规格如有更改，恕不另行通知。本出版物取代并替代之前提供的所有其他信息。未经 NVIDIA 公司明确书面批准，NVIDIA 公司产品未获授权作为生命支持设备或系统中的关键组件。

## 商标

NVIDIA 和 NVIDIA 徽标是 NVIDIA 公司在美国和其他国家/地区的商标或注册商标。其他公司和产品名称可能是其各自关联公司的商标。

## 版权

© 2007-2019 NVIDIA Corporation. 保留所有权利。

