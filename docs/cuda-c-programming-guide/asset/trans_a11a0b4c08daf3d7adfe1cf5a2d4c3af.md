

return d;
}

cudaExtent getCudaExtentForVulkanExtent(VkExtent3D vkExt, uint32_t arrayLayers,
                                         VkImageViewType vkImageViewType) {
    cudaExtent e = { 0, 0, 0 };

    switch (vkImageViewType) {
    case VK_IMAGE_VIEW_TYPE_1D:
        e.width = vkExt.width; e.height = 0;
    case VK_IMAGE_VIEW_TYPE_2D:
        e.width = vkExt.width; e.height =
            vkExt.height; e.depth = 0; break;
    case VK_IMAGE_VIEW_TYPE_3D:
        e.width = vkExt.width; e.height =
            vkExt.height; e.depth = vkExt.depth; break;
    case VK_IMAGE_VIEW_TYPE_CUBE:
        e.width = vkExt.width; e.height =
            vkExt.height; e.depth = arrayLayers; break;
    case VK_IMAGE_VIEW_TYPE_1D_ARRAY:
        e.width = vkExt.width; e.height = 0;
    case VK_IMAGE_VIEW_TYPE_2D_ARRAY:
        e.width = vkExt.width; e.height =
            vkExt.height; e.depth = arrayLayers; break;
    case VK_IMAGE_VIEW_TYPE_CUBE_ARRAY:
        e.width = vkExt.width; e.height =
            vkExt.height; e.depth = arrayLayers; break;
    default: assert(0);
    }

    return e;
}

unsigned int getCudaMipmappedArrayFlagsForVulkanImage(VkImageViewType
                                                      vkImageViewType,
                                                      VkImageUsageFlags vkImageUsageFlags,
                                                      bool
                                                      allowSurfaceLoadStore) {
    unsigned int flags = 0;

    switch (vkImageViewType) {
    case VK_IMAGE_VIEW_TYPE_CUBE:    flags |= cudaArrayCubemap;
        break;
    case VK_IMAGE_VIEW_TYPE_CUBE_ARRAY: flags |= cudaArrayCubemap |
        cudaArrayLayered;
    case VK_IMAGE_VIEW_TYPE_1D_ARRAY:
        flags |= cudaArrayLayered;
    case VK_IMAGE_VIEW_TYPE_2D_ARRAY:
        flags |= cudaArrayLayered;
        break;
    default: break;
    }

    if (vkImageUsageFlags & VK_IMAGE_USAGE_COLOR_ATTACHMENT_BIT) {
        flags |= cudaArrayColorAttachment;
    }

    if (allowSurfaceLoadStore) {
        flags |= cudaArraySurfaceLoadStore;
    }

    return flags;
}

## 3.3.1.5. 导入同步对象

使用 **VK_EXTERNAL_SEMAPHORE_HANDLE_TYPE_OPAQUE_FD_BIT** 导出的 Vulkan 信号量对象可以使用与该对象关联的文件描述符导入到 CUDA 中，如下所示。请注意，一旦导入，CUDA 即拥有该文件描述符的所有权。在成功导入后使用该文件描述符会导致未定义行为。

```cpp
cudaExternalSemaphore_t importVulkanSemaphoreObjectFromFileDescriptor(int fd) {
    cudaExternalSemaphore_t extSem = NULL;
    cudaExternalSemaphoreHandleDesc desc = {};
    memset(&desc, 0, sizeof(desc));
    desc.type = cudaExternalSemaphoreHandleTypeOpaqueFd;
    desc.handle.fd = fd;
    cudaImportExternalSemaphore(&extSem, &desc);
    // Input parameter 'fd' should not be used beyond this point as CUDA has
    // assumed ownership of it
    return extSem;
}
```

使用 VK_EXTERNAL_SEMAPHORE_HANDLE_TYPE_OPAQUE_WIN32_BIT 导出的 Vulkan 信号量对象可以使用与该对象关联的 NT 句柄导入到 CUDA 中，如下所示。请注意，CUDA 不会假设 NT 句柄的所有权，应用程序有责任在不再需要该句柄时将其关闭。NT 句柄持有对资源的引用，因此必须在底层信号量释放之前显式释放它。

```cpp
cudaExternalSemaphore_t importVulkanSemaphoreObjectFromNTHandle(HANDLE handle) {
    cudaExternalSemaphore_t extSem = NULL;
    cudaExternalSemaphoreHandleDesc desc = {};
    memset(&desc, 0, sizeof(desc));
    desc.type = cudaExternalSemaphoreHandleTypeOpaqueWin32;
    desc.handle.win32.handle = handle;
    cudaImportExternalSemaphore(&extSem, &desc);
    // Input parameter 'handle' should be closed if it's not needed anymore
    CloseHandle(handle);
    return extSem;
}
```

使用 **VK_EXTERNAL_SEMAPHORE_HANDLE_TYPE_OPAQUE_WIN32_BIT** 导出的 Vulkan 信号量对象还可以使用命名句柄（如果存在）进行导入，如下所示。

```cpp
cudaExternalSemaphore_t importVulkanSemaphoreObjectFromNamedNTHandle(LPCWSTR name) {
    cudaExternalSemaphore_t extSem = NULL;
    cudaExternalSemaphoreHandleDesc desc = {};
    memset(&desc, 0, sizeof(desc));
    desc.type = cudaExternalSemaphoreHandleTypeOpaqueWin32;
    desc.handle.win32.name = (void *)name;
    cudaImportExternalSemaphore(&extSem, &desc);
    return extSem;
}
```

使用 **VK_EXTERNAL_SEMAPHORE_HANDLE_TYPE_OPAQUE_WIN32_KMT_BIT** 导出的 Vulkan 信号量对象可以使用与该对象关联的全局共享 D3DKMT 句柄导入到 CUDA 中，如下所示。由于全局共享 D3DKMT 句柄不持有对底层信号量的引用，因此当对资源的所有其他引用都被销毁时，它会自动销毁。

```cpp
cudaExternalSemaphore_t importVulkanSemaphoreObjectFromKMTHandle(HANDLE handle) {
    cudaExternalSemaphore_t extSem = NULL;
    cudaExternalSemaphoreHandleDesc desc = {};
    memset(&desc, 0, sizeof(desc));
    desc.type = cudaExternalSemaphoreHandleTypeOpaqueWin32Kmt;
    desc.handle.win32.handle = (void *)handle;
    cudaImportExternalSemaphore(&extSem, &desc);
    return extSem;
}
```

## 3.3.1.6. 对导入的同步对象进行信号/等待

如下所示，可以对导入的 Vulkan 信号量对象发送信号。对这样的信号量对象发送信号会将其设置为信号状态。等待此信号的相应等待操作必须在 Vulkan 中发出。此外，等待此信号的等待操作必须在发出此信号之后发出。

```cpp
void signalExternalSemaphore(cudaExternalSemaphore_t extSem, cudaStream_t stream) {
    cudaExternalSemaphoreSignalParams params = {};
    memset(&params, 0, sizeof(params));
    cudaSignalExternalSemaphoresAsync(&extSem, &params, 1, stream);
}
```

如下所示，可以对导入的 Vulkan 信号量对象进行等待。对这样的信号量对象进行等待会一直等待直到它达到信号状态，然后将其重置回非信号状态。此等待操作所等待的相应信号必须在 Vulkan 中发出。此外，必须在发出此等待操作之前发出该信号。

```cpp
void waitExternalSemaphore(cudaExternalSemaphore_t extSem, cudaStream_t stream)
{
    cudaExternalSemaphoreWaitParams params = {};
    memset(&params, 0, sizeof(params));
    cudaWaitExternalSemaphoresAsync(&extSem, &params, 1, stream);
}
```

## 3.3.2. OpenGL 互操作性

传统的 OpenGL-CUDA 互操作（如第 3.2.12.1 节所述）通过 CUDA 直接使用在 OpenGL 中创建的句柄来工作。但是，由于 OpenGL 也可以使用在 Vulkan 中创建的内存和同步对象，因此存在一种替代方法来进行 OpenGL-CUDA 互操作。本质上，Vulkan 导出的内存和同步对象可以同时导入到 OpenGL 和 CUDA 中，然后用于协调 OpenGL 和 CUDA 之间的内存访问。有关如何导入由 Vulkan 导出的内存和同步对象的更多详细信息，请参阅以下 OpenGL 扩展：

- GL_EXT_memory_object
- GL_EXT_memory_object_fd
- GL_EXT_memory_object_win32
- GL_EXT_semaphore
- GL_EXT_semaphore_fd
- GL_EXT_semaphore_win32

## 3.3.3. Direct3D 12 互操作性

### 3.3.3.1. 匹配设备 LUID

导入由 Direct3D 12 导出的内存和同步对象时，必须在创建它们的同一设备上对其进行导入和映射。可以通过比较 CUDA 设备的 LUID 与 Direct3D 12 设备的 LUID 来确定与创建这些对象的 Direct3D 12 设备对应的 CUDA 设备，如以下代码示例所示。请注意，Direct3D 12 设备不得在链接节点适配器上创建。即，ID3D12Device::GetNodeCount 返回的节点数必须为 1。

```cpp
int getCudaDeviceForD3D12Device(ID3D12Device *d3d12Device) {
    LUID d3d12Luid = d3d12Device->GetAdapterLuid();

    int cudaDeviceCount;
    cudaGetDeviceCount(&cudaDeviceCount);

    for (int cudaDevice = 0; cudaDevice < cudaDeviceCount; cudaDevice++) {
        cudaDeviceProp deviceProp;
        cudaGetDeviceProperties(&deviceProp, cudaDevice);

        char *cudaLuid = deviceProp.luid;

        if ((!memcmp(&d3d12Luid.LowPart, cudaLuid, sizeof(d3d12Luid.LowPart))) &&
            !memcmp(&d3d12Luid.HighPart, cudaLuid + sizeof(d3d12Luid.LowPart),
            sizeof(d3d12Luid.HighPart))) {
            return cudaDevice;
        }
    }
    return cudaInvalidDeviceId;
}
```

### 3.3.3.2. 导入内存对象

可共享的 Direct3D 12 堆内存对象（通过在调用 ID3D12Device::CreateHeap 时设置标志 D3D12_HEAP_FLAG_SHARED 创建）可以使用与该对象关联的 NT 句柄导入到 CUDA 中，如下所示。请注意，应用程序有责任在不再需要 NT 句柄时将其关闭。NT 句柄持有对资源的引用，因此必须在底层内存释放之前显式释放它。

```cpp
cudaExternalMemory_t importD3D12HeapFromNTHandle(HANDLE handle, unsigned long long size) {
    cudaExternalMemory_t extMem = NULL;
    cudaExternalMemoryHandleDesc desc = {};

    memset(&desc, 0, sizeof(desc));
    desc.type = cudaExternalMemoryHandleTypeD3D12Heap;
    desc.handle.win32.handle = (void *)handle;
    desc.size = size;

    cudaImportExternalMemory(&extMem, &desc);

    // Input parameter 'handle' should be closed if it's not needed anymore
    CloseHandle(handle);

    return extMem;
}
```

