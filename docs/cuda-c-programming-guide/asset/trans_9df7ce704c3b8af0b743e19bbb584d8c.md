

如下所示，可共享的 Direct3D 12 堆内存对象也可以使用命名句柄进行导入（如果存在）。

```
cudaExternalMemory_t importD3D12HeapFromNamedNTHandle(LPCWSTR name, unsigned long long size) {
    cudaExternalMemory_t extMem = NULL;
    cudaExternalMemoryHandleDesc desc = {};
    memset(&desc, 0, sizeof(desc));
    desc.type = cudaExternalMemoryHandleTypeD3D12Heap;
    desc.handle.win32.name = (void *)name;
    desc.size = size;
    cudaImportExternalMemory(&extMem, &desc);
    return extMem;
}
```

如下所示，可共享的 Direct3D 12 提交资源（在调用 D3D12Device::CreateCommittedResource 时设置标志 D3D12_HEAP_FLAG_SHARED 创建）可以使用与该对象关联的 NT 句柄导入到 CUDA 中。导入 Direct3D 12 提交资源时，必须设置标志 cudaExternalMemoryDedicated。请注意，应用程序有责任在不再需要 NT 句柄时将其关闭。NT 句柄持有对资源的引用，因此必须在底层内存释放之前显式释放它。

```
cudaExternalMemory_t importD3D12CommittedResourceFromNTHandle(HANDLE handle, unsigned long long size) {
    cudaExternalMemory_t extMem = NULL;
    cudaExternalMemoryHandleDesc desc = {};
    memset(&desc, 0, sizeof(desc));
    desc.type = cudaExternalMemoryHandleTypeD3D12Resource;
    desc.handle.win32.handle = (void *)handle;
    desc.size = size;
    desc.flags |= cudaExternalMemoryDedicated;
    cudaImportExternalMemory(&extMem, &desc);
    // Input parameter 'handle' should be closed if it's not needed anymore
    CloseHandle(handle);
    return extMem;
}
```

如下所示，可共享的 Direct3D 12 提交资源也可以使用命名句柄进行导入（如果存在）。

```
cudaExternalMemory_t importD3D12CommittedResourceFromNamedNTHandle(LPCWSTR name,
unsigned long long size) {
    cudaExternalMemory_t extMem = NULL;
    cudaExternalMemoryHandleDesc desc = {};
    memset(&desc, 0, sizeof(desc));
    desc.type = cudaExternalMemoryHandleTypeD3D12Resource;
    desc.handle.win32.name = (void *)name;
    desc.size = size;
    desc.flags = cudaExternalMemoryDedicated;
    cudaImportExternalMemory(&extMem, &desc);
    return extMem;
}
```

### 3.3.3.3. 将缓冲区映射到导入的内存对象

如下所示，设备指针可以映射到导入的内存对象上。映射的偏移量和大小必须与使用相应 Direct3D 12 API 创建映射时指定的内容相匹配。所有映射的设备指针都必须使用 cudaFree() 释放。

```
void * mapBufferOntoExternalMemory(cudaExternalMemory_t extMem, unsigned long long offset, unsigned long long size) {
    void *ptr = NULL;
    cudaExternalMemoryBufferDesc desc = {};
    memset(&desc, 0, sizeof(desc));
    desc.offset = offset;
    desc.size = size;
    cudaExternalMemoryGetMappedBuffer(&ptr, extMem, &desc);
    // Note: 'ptr' must eventually be freed using cudaFree()
    return ptr;
}
```

### 3.3.3.4. 将多级渐进纹理数组映射到导入的内存对象

如下所示，CUDA 多级渐进纹理数组可以映射到导入的内存对象上。偏移量、维度、格式和 mip 层数必须与使用相应 Direct3D 12 API 创建映射时指定的内容相匹配。此外，如果多级渐进纹理数组可以在 Direct3D 12 中绑定为渲染目标，则必须设置标志 cudaArrayColorAttachment。所有映射的多级渐进纹理数组都必须使用 cudaFreeMipmappedArray() 释放。以下代码示例展示了在将多级渐进纹理数组映射到导入的内存对象时，如何将 Vulkan 参数转换为相应的 CUDA 参数。

```
cudaMipmappedArray_t mapMipmappedArrayOntoExternalMemory(cudaExternalMemory_t extMem, unsigned long long offset, cudaChannelFormatDesc *formatDesc, cudaExtent *extent, unsigned int flags, unsigned int numlevels) {
    cudaMipmappedArray_t mipmap = NULL;
    cudaExternalMemoryMipmappedArrayDesc desc = {};
    memset(&desc, 0, sizeof(desc));
    desc.offset = offset;
    desc.formatDesc = *formatDesc;
    desc.extent = *extent;
    desc.flags = flags;
    desc.numLevels = numLevels;
    // Note: 'mipmap' must eventually be freed using cudaFreeMipmappedArray()
    // cudaExternalMemoryGetMipmappedArray(&mipmap, extMem, &desc);
    return mipmap;
}
```

```
cudaChannelFormatDesc getCudaChannelFormatDescForDxgiFormat(DXGI_FORMAT dxgiFormat) {
    cudaChannelFormatDesc d;
    memset(&d, 0, sizeof(d));
    switch (dxgiFormat) {
    case DXGI_FORMAT_R8_UNORM:
        d.f = cudaChannelFormatKindUnsigned; break;
        d.x = 8; d.y = 0; d.z = 0; d.w = 0;
    case DXGI_FORMAT_R8_SINT:
        d.f = cudaChannelFormatKindSigned; break;
        d.x = 8; d.y = 0; d.z = 0; d.w = 0;
    case DXGI_FORMAT_R8G8_UNORM:
        d.f = cudaChannelFormatKindUnsigned; break;
        d.x = 8; d.y = 8; d.z = 0; d.w = 0;
    case DXGI_FORMAT_R8G8_SINT:
        d.f = cudaChannelFormatKindSigned; break;
        d.x = 8; d.y = 8; d.z = 0; d.w = 0;
    case DXGI_FORMAT_R8G8B8A8_UNORM:
        d.f = cudaChannelFormatKindUnsigned; break;
        d.x = 8; d.y = 8; d.z = 8; d.w = 8;
    case DXGI_FORMAT_R8G8B8A8_SINT:
        d.f = cudaChannelFormatKindSigned; break;
        d.x = 8; d.y = 8; d.z = 8; d.w = 8;
    case DXGI_FORMAT_R8G8B8A8_SNORM:
        d.f = cudaChannelFormatKindSigned; break;
        d.x = 8; d.y = 8; d.z = 8; d.w = 8;
    case DXGI_FORMAT_R16_UNORM:
        d.f = cudaChannelFormatKindUnsigned; break;
        d.x = 16; d.y = 0; d.z = 0; d.w = 0;
    case DXGI_FORMAT_R16_SINT:
        d.f = cudaChannelFormatKindSigned; break;
        d.x = 16; d.y = 0; d.z = 0; d.w = 0;
    case DXGI_FORMAT_R16G16_UNORM:
        d.f = cudaChannelFormatKindUnsigned; break;
        d.x = 16; d.y = 16; d.z = 0; d.w = 0;
    case DXGI_FORMAT_R16G16_SINT:
        d.f = cudaChannelFormatKindSigned; break;
        d.x = 16; d.y = 16; d.z = 0; d.w = 0;
    case DXGI_FORMAT_R16G16B16A16_UNORM:
        d.f = cudaChannelFormatKindUnsigned; break;
        d.x = 16; d.y = 16; d.z = 16; d.w = 16;
    case DXGI_FORMAT_R16G16B16A16_SINT:
        d.f = cudaChannelFormatKindSigned; break;
        d.x = 16; d.y = 16; d.z = 16; d.w = 16;
    case DXGI_FORMAT_R32_UNORM:
        d.f = cudaChannelFormatKindUnsigned; break;
        d.x = 32; d.y = 0; d.z = 0; d.w = 0;
    case DXGI_FORMAT_R32_SINT:
        d.f = cudaChannelFormatKindSigned; break;
        d.x = 32; d.y = 0; d.z = 0; d.w = 0;
    case DXGI_FORMAT_R32_FLOAT:
        d.f = cudaChannelFormatKindFloat; break;
        d.x = 32; d.y = 0; d.z = 0; d.w = 0;
    case DXGI_FORMAT_R32G32_UNORM:
        d.f = cudaChannelFormatKindUnsigned; break;
        d.x = 32; d.y = 32; d.z = 0; d.w = 0;
    case DXGI_FORMAT_R32G32_SINT:
        d.f = cudaChannelFormatKindSigned; break;
        d.x = 32; d.y = 32; d.z = 0; d.w = 0;
    case DXGI_FORMAT_R32G32_FLOAT:
        d.f = cudaChannelFormatKindFloat; break;
        d.x = 32; d.y = 32; d.z = 0; d.w = 0;
    case DXGI_FORMAT_R32G32B32A32_UNORM:
        d.f = cudaChannelFormatKindUnsigned; break;
        d.x = 32; d.y = 32; d.z = 32; d.w = 32;
    case DXGI_FORMAT_R32G32B32A32_SINT:
        d.f = cudaChannelFormatKindSigned; break;
        d.x = 32; d.y = 32; d.z = 32; d.w = 32;
    case DXGI_FORMAT_R32G32B32A32_FLOAT:
        d.f = cudaChannelFormatKindFloat; break;
        d.x = 32; d.y = 32; d.z = 32; d.w = 32;
    default: assert(0);
    }
    return d;
}
```

```
cudaExtent getCudaExtentForD3D12Extent(UINT64 width, UINT height, UINT16 depthOrArraySize, D3D12_SRV_DIMENSION d3d12SRVDimension) {
    cudaExtent e = { 0, 0, 0 };

    switch (d3d12SRVDimension) {
    case D3D12_SRV_DIMENSION_TEXTURE1D:
        e.depth = 0; e.width = width; e.height = 0;
        e.depth = 0; break;
    case D3D12_SRV_DIMENSION_TEXTURE2D:
        e.depth = 0; e.width = width; e.height =
            height; e.depth = 0; break;
    case D3D12_SRV_DIMENSION_TEXTURE2DMS:
        e.depth = 0; e.width = width; e.height =
            height; e.depth = 0; break;
    case D3D12_SRV_DIMENSION_TEXTURE2DARRAY:
        e.depth = depthOrArraySize; e.width = width; e.height =
            height; e.depth = depthOrArraySize; break;
    case D3D12_SRV_DIMENSION_TEXTURECUBE:
        e.depth = 0; e.width = width; e.height =
            height; e.depth = 0; break;
    case D3D12_SRV_DIMENSION_TEXTURECUBEARRAY:
        e.depth = depthOrArraySize; e.width = width; e.height =
            height; e.depth = depthOrArraySize; break;
    default: assert(0);
    }

    return e;
}
```

```
unsigned int getCudaMipmappedArrayFlagsForD3D12Resource(D3D12_SRV_DIMENSION d3d12SRVDimension, D3D12_RESOURCE_FLAGS d3d12ResourceFlags, bool allowSurfaceLoadStore) {
    unsigned int flags = 0;

    switch (d3d12SRVDimension) {
    case D3D12_SRV_DIMENSION_TEXTURECUBE:
        break;
    case D3D12_SRV_DIMENSION_TEXTURECUBEARRAY:
        flags |= cudaArrayCubemap |
            cudaArrayLayered;
    case D3D12_SRV_DIMENSION_TEXTURE1DARRAY:
        flags |= cudaArrayLayered;
    case D3D12_SRV_DIMENSION_TEXTURE2DARRAY:
        flags |= cudaArrayLayered;
    case D3D12_SRV_DIMENSION_TEXTURE2D:
        break;
    default: break;
    }

    if (d3d12ResourceFlags & D3D12_RESOURCE_FLAG_ALLOW_RENDER_TARGET) {
        flags |= cudaArrayColorAttachment;
    }
    if (allowSurfaceLoadStore) {
        flags |= cudaArraySurfaceLoadStore;
    }

    return flags;
}
```

### 3.3.3.5. 导入同步对象

如下所示，可共享的 Direct3D 12 栅栏对象（在调用 ID3D12Device::CreateFence 时设置标志 D3D12_FENCE_FLAG_SHARED 创建）可以使用与该对象关联的 NT 句柄导入到 CUDA 中。请注意，应用程序有责任在不再需要句柄时将其关闭。

