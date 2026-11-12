
## how to convert Direct3D 11 parameters into the corresponding CUDA parameters when mapping mipmapped arrays onto imported memory objects.

```cpp
cudaMipmappedArray_t mapMipmappedArrayOntoExternalMemory(cudaExternalMemory_t extMem, unsigned long long offset, cudaChannelFormatDesc *formatDesc, cudaExtent *extent, unsigned int flags, unsigned int numlevels) {
    cudaMipmappedArray_t mipmap = NULL;
    cudaExternalMemoryMipmappedArrayDesc desc = {};

    memset(&desc, 0, sizeof(desc));

    desc.offset = offset;
    desc.formatDesc = *formatDesc;
    desc.extent = *extent;
    desc.flags = flags;
    desc.numLevels = numlevels;

    // Note: 'mipmap' must eventually be freed using cudaFreeMipmappedArray()
    // cudaExternalMemoryGetMipmappedArray(&mipmap, extMem, &desc);

    return mipmap;
}
```

```cpp
cudaChannelFormatDesc getCudaChannelFormatDescForDxgiFormat(DXGI_FORMAT dxgiFormat) {
    cudaChannelFormatDesc d;
    memset(&d, 0, sizeof(d));
    switch (dxgiFormat) {
    case DXGI_FORMAT_R8_UNORM:
        d.x = 8; d.y = 0; d.z = 0; d.w = 0;
        d.f = cudaChannelFormatKindUnsigned; break;
    case DXGI_FORMAT_R8_SINT:
        d.x = 8; d.y = 0; d.z = 0; d.w = 0;
        d.f = cudaChannelFormatKindSigned; break;
    case DXGI_FORMAT_R8G8_UNORM:
        d.x = 8; d.y = 8; d.z = 0; d.w = 0;
        d.f = cudaChannelFormatKindUnsigned; break;
    case DXGI_FORMAT_R8G8_SINT:
        d.x = 8; d.y = 8; d.z = 0; d.w = 0;
        d.f = cudaChannelFormatKindSigned; break;
    case DXGI_FORMAT_R8G8B8A8_UNORM:
        d.x = 8; d.y = 8; d.z = 8; d.w = 8;
        d.f = cudaChannelFormatKindUnsigned; break;
    case DXGI_FORMAT_R8G8B8A8_SINT:
        d.x = 8; d.y = 8; d.z = 8; d.w = 8;
        d.f = cudaChannelFormatKindSigned; break;
    case DXGI_FORMAT_R16_UNORM:
        d.x = 16; d.y = 0; d.z = 0; d.w = 0;
        d.f = cudaChannelFormatKindUnsigned; break;
    case DXGI_FORMAT_R16_SINT:
        d.x = 16; d.y = 0; d.z = 0; d.w = 0;
        d.f = cudaChannelFormatKindSigned; break;
    case DXGI_FORMAT_R16G16_UNORM:
        d.x = 16; d.y = 16; d.z = 0; d.w = 0;
        d.f = cudaChannelFormatKindUnsigned; break;
    case DXGI_FORMAT_R16G16_SINT:
        d.x = 16; d.y = 16; d.z = 0; d.w = 0;
        d.f = cudaChannelFormatKindSigned; break;
    case DXGI_FORMAT_R16G16B16A16_UNORM:
        d.x = 16; d.y = 16; d.z = 16; d.w = 16;
        d.f = cudaChannelFormatKindUnsigned; break;
    case DXGI_FORMAT_R16G16B16A16_SINT:
        d.x = 16; d.y = 16; d.z = 16; d.w = 16;
        d.f = cudaChannelFormatKindSigned; break;
    case DXGI_FORMAT_R32_UNORM:
        d.x = 32; d.y = 0; d.z = 0; d.w = 0;
        d.f = cudaChannelFormatKindUnsigned; break;
    case DXGI_FORMAT_R32_SINT:
        d.x = 32; d.y = 0; d.z = 0; d.w = 0;
        d.f = cudaChannelFormatKindSigned; break;
    case DXGI_FORMAT_R32_FLOAT:
        d.x = 32; d.y = 0; d.z = 0; d.w = 0;
        d.f = cudaChannelFormatKindFloat; break;
    case DXGI_FORMAT_R32G32_UNORM:
        d.x = 32; d.y = 32; d.z = 0; d.w = 0;
        d.f = cudaChannelFormatKindUnsigned; break;
    case DXGI_FORMAT_R32G32_SINT:
        d.x = 32; d.y = 32; d.z = 0; d.w = 0;
        d.f = cudaChannelFormatKindSigned; break;
    case DXGI_FORMAT_R32G32_FLOAT:
        d.x = 32; d.y = 32; d.z = 0; d.w = 0;
        d.f = cudaChannelFormatKindFloat; break;
    case DXGI_FORMAT_R32G32B32A32_UNORM:
        d.x = 32; d.y = 32; d.z = 32; d.w = 32;
        d.f = cudaChannelFormatKindUnsigned; break;
    case DXGI_FORMAT_R32G32B32A32_SINT:
        d.x = 32; d.y = 32; d.z = 32; d.w = 32;
        d.f = cudaChannelFormatKindSigned; break;
    case DXGI_FORMAT_R32G32B32A32_FLOAT:
        d.x = 32; d.y = 32; d.z = 32; d.w = 32;
        d.f = cudaChannelFormatKindFloat; break;
    default: assert(0);
    }
    return d;
}
```

```cpp
cudaExtent getCudaExtentForD3D11Extent(UINT64 width, UINT height, UINT16 depthOrArraySize, D3D11_SRV_DIMENSION d3d11SRVDimension) {
    cudaExtent e = { 0, 0, 0 };

    switch (d3d11SRVDimension) {
    case D3D11_SRV_DIMENSION_TEXTURE1D:
        e.width = width; e.height = 0;
        e.depth = 0; break;
    case D3D11_SRV_DIMENSION_TEXTURE2D:
        e.width = width; e.height = height; e.depth = 0; break;
    case D3D11_SRV_DIMENSION_TEXTURE3D:
        e.width = width; e.height = height; e.depth = depthOrArraySize; break;
    case D3D11_SRV_DIMENSION_TEXTURECUBE:
        e.width = width; e.height = height; e.depth = 0; break;
    case D3D11_SRV_DIMENSION_TEXTURECUBEARRAY:
        e.width = width; e.height = height; e.depth = depthOrArraySize; break;
    case D3D11_SRV_DIMENSION_TEXTURE1DARRAY:
        e.width = width; e.height = 0;
        e.depth = depthOrArraySize; break;
    case D3D11_SRV_DIMENSION_TEXTURE2DARRAY:
        e.width = width; e.height = height; e.depth = depthOrArraySize; break;
    case D3D11_SRV_DIMENSION_TEXTURECUBEARRAY:
        e.width = width; e.height = height; e.depth = depthOrArraySize; break;
    default: assert(0);
    }
    return e;
}
```

```cpp
unsigned int getCudaMipmappedArrayFlagsForD3D12Resource(D3D11_SRV_DIMENSION d3d11SRVDimension, D3D11_BIND_FLAG d3d11BindFlags, bool allowSurfaceLoadStore) {
    unsigned int flags = 0;

    switch (d3d11SRVDimension) {
    case D3D11_SRV_DIMENSION_TEXTURECUBE:    flags |= cudaArrayCubemap;
        break;
    case D3D11_SRV_DIMENSION_TEXTURECUBEARRAY: flags |= cudaArrayCubemap | cudaArrayLayered; break;
    case D3D11_SRV_DIMENSION_TEXTURE1DARRAY:   flags |= cudaArrayLayered; break;
    case D3D11_SRV_DIMENSION_TEXTURE2DARRAY:   flags |= cudaArrayLayered; break;
    default: break;
    }

    if (d3d11BindFlags & D3D11_BIND_RENDER_TARGET) {
        flags |= cudaArrayColorAttachment;
    }

    if (allowSurfaceLoadStore) {
        flags |= cudaArraySurfaceLoadStore;
    }

    return flags;
}
```

### 3.3.4.5. Importing synchronization objects

A shareable Direct3D 11 fence object, created by setting the flag **D3D11_FENCE_FLAG_SHARED** in the call to **ID3D11Device5::CreateFence**, can be imported into CUDA using the NT handle associated with that object as shown below. Note that it is the application's responsibility to close the handle when it is not required anymore. The NT handle holds a reference to the resource, so it must be explicitly freed before the underlying semaphore can be freed.

```cpp
cudaExternalSemaphore_t importD3D11FenceFromNTHandle(HANDLE handle) {
    cudaExternalSemaphore_t extSem = NULL;
    cudaExternalSemaphoreHandleDesc desc = {};
    memset(&desc, 0, sizeof(desc));
    desc.type = cudaExternalSemaphoreHandleTypeD3D11Fence;
    desc.handle.win32.handle = handle;
    cudaImportExternalSemaphore(extSem, &desc);
    // Input parameter 'handle' should be closed if it's not needed anymore
    CloseHandle(handle);
    return extSem;
}
```

A shareable Direct3D 11 fence object can also be imported using a named handle if one exists as shown below.

```cpp
cudaExternalSemaphore_t importD3D11FenceFromNamedNTHandle(LPCWSTR name) {
    cudaExternalSemaphore_t extSem = NULL;
    cudaExternalSemaphoreHandleDesc desc = {};
    memset(&desc, 0, sizeof(desc));
    desc.type = cudaExternalSemaphoreHandleTypeD3D11Fence;
    desc.handle.win32.name = (void *)name;
    cudaImportExternalSemaphore(extSem, &desc);
    return extSem;
}
```

A shareable Direct3D 11 keyed mutex object associated with a shareable Direct3D 11 resource, viz, IDXGIKeyedMutex, created by setting the flag D3D11_RESOURCE_MISC_SHARED_KEYEDMUTEX, can be imported into CUDA using the NT handle associated with that object as shown below. Note that it is the application's responsibility to close the handle when it is not required anymore. The NT handle holds a reference to the resource, so it must be explicitly freed before the underlying semaphore can be freed.

```cpp
cudaExternalSemaphore_t importD3D11KeyedMutexFromNTHandle(HANDLE handle) {
    cudaExternalSemaphore_t extSem = NULL;
    cudaExternalSemaphoreHandleDesc desc = {};
    memset(&desc, 0, sizeof(desc));
    desc.type = cudaExternalSemaphoreHandleTypeKeyedMutex;
    desc.handle.win32.handle = handle;
    cudaImportExternalSemaphore(extSem, &desc);
    // Input parameter 'handle' should be closed if it's not needed anymore
    CloseHandle(handle);
    return extSem;
}
```
