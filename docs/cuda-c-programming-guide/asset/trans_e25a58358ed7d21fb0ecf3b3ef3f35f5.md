

不再使用。NT 句柄持有对资源的引用，因此在底层信号量被释放之前，必须显式释放该句柄。

```cpp
cudaExternalSemaphore_t importD3D12FenceFromNTHandle(HANDLE handle) {
 cudaExternalSemaphore_t extSem = NULL;
 cudaExternalSemaphoreHandleDesc desc = {};
 memset(&desc, 0, sizeof(desc));
 desc.type = cudaExternalSemaphoreHandleTypeD3D12Fence;
 desc.handle.win32.handle = handle;
 cudaImportExternalSemaphore(extSem, &desc);
 // Input parameter 'handle' should be closed if it's not needed anymore
 CloseHandle(handle);
 return extSem;
}
```

如果存在命名句柄，也可以如下所示使用命名句柄导入可共享的 Direct3D 12 围栏对象。

```cpp
cudaExternalSemaphore_t importD3D12FenceFromNamedNTHandle(LPCWSTR name) {
 cudaExternalSemaphore_t extSem = NULL;
 cudaExternalSemaphoreHandleDesc desc = {};
 memset(&desc, 0, sizeof(desc));
 desc.type = cudaExternalSemaphoreHandleTypeD3D12Fence;
 desc.handle.win32.name = (void *)name;
 cudaImportExternalSemaphore(extSem, &desc);
 return extSem;
}
```

### 3.3.3.6. 对导入的同步对象进行信号/等待

如下所示，可以对导入的 Direct3D 12 围栏对象发出信号。对这样的围栏对象发出信号会将其值设置为指定的值。等待此信号的相应等待操作必须在 Direct3D 12 中发出。此外，等待此信号的等待操作必须在发出此信号之后发出。

```cpp
void signalExternalSemaphore(cudaExternalSemaphore_t extSem, unsigned long long value, cudaStream_t stream) {
 cudaExternalSemaphoreSignalParams params = {};
 memset(&params, 0, sizeof(params));
 params.params.fence.value = value;
 cudaSignalExternalSemaphoresAsync(&extSem, &params, 1, stream);
}
```

如下所示，可以等待导入的 Direct3D 12 围栏对象。等待这样的围栏对象会一直等待，直到其值大于或等于指定的值。

此等待所等待的相应信号必须在 Direct3D 12 中发出。此外，必须在发出此等待之前发出该信号。

```cpp
void waitExternalSemaphore(cudaExternalSemaphore_t extSem, unsigned long long value, cudaStream_t stream) {
    cudaExternalSemaphoreWaitParams params = {};
    memset(&params, 0, sizeof(params));
    params.params.fence.value = value;
    cudaWaitExternalSemaphoresAsync(&extSem, &params, 1, stream);
}
```

## 3.3.4. Direct3D 11 互操作性

### 3.3.4.1. 匹配设备 LUID

导入由 Direct3D 11 导出的内存和同步对象时，必须在创建它们的同一设备上导入和映射这些对象。可以通过比较 CUDA 设备的 LUID 与 Direct3D 11 设备的 LUID 来确定与创建对象的 Direct3D 11 设备对应的 CUDA 设备，如以下代码示例所示。

```cpp
int getCudaDeviceForD3D11Device(ID3D11Device *d3d11Device) {
    IDXGIDevice *dxgiDevice;
    d3d11Device->QueryInterface(__uuidof(IDXGIDevice), (void **)&dxgiDevice);
    IDXGIAdapter *dxgiAdapter;
    dxgiDevice->GetAdapter(&dxgiAdapter);
    DXGI_ADAPTER_DESC dxgiAdapterDesc;
    dxgiAdapter->GetDesc(&dxgiAdapterDesc);
    LUID d3d11Luid = dxgiAdapterDesc.AdapterLuid;
    int cudaDeviceCount;
    cudaGetDeviceCount(&cudaDeviceCount);
    for (int cudaDevice = 0; cudaDevice < cudaDeviceCount; cudaDevice++) {
        cudaDeviceProp deviceProp;
        cudaGetDeviceProperties(&deviceProp, cudaDevice);
        char *cudaLuid = deviceProp.luid;
        if (!memcmp(&d3d11Luid.LowPart, cudaLuid, sizeof(d3d11Luid.LowPart)) &&
            !memcmp(&d3d11Luid.HighPart, cudaLuid + sizeof(d3d11Luid.LowPart),
                    sizeof(d3d11Luid.HighPart))) {
            return cudaDevice;
        }
    }
    return cudaInvalidDeviceId;
}
```

### 3.3.4.2. 导入内存对象

可共享的 Direct3D 11 纹理资源（即 ID3D11Texture1D、ID3D11Texture2D 或 ID3D11Texture3D）可以通过在分别调用 ID3D11Device::CreateTexture1D、ID3D11Device::CreateTexture2D 或 ID3D11Device::CreateTexture3D 时设置 D3D11_RESOURCE_MISC_SHARED 或 D3D11_RESOURCE_MISC_SHARED_KEYEDMUTEX（在 Windows 7 上）或 D3D11_RESOURCE_MISC_SHARED_NTHANDLE（在 Windows 10 上）来创建。可共享的 Direct3D 11 缓冲区资源 ID3D11Buffer 可以通过在调用 ID3D11Device::CreateBuffer 时指定上述标志之一来创建。通过指定 D3D11_RESOURCE_MISC_SHARED_NTHANDLE 创建的可共享资源可以如下所示使用与该对象关联的 NT 句柄导入到 CUDA 中。请注意，当不再需要 NT 句柄时，关闭它是应用程序的责任。NT 句柄持有对资源的引用，因此在底层内存被释放之前，必须显式释放该句柄。导入 Direct3D 11 资源时，必须设置标志 cudaExternalMemoryDedicated。

```cpp
cudaExternalMemory_t importD3D11ResourceFromNTHandle(HANDLE handle, unsigned long long size) {
    cudaExternalMemory_t extMem = NULL;
    cudaExternalMemoryHandleDesc desc = {};
    memset(&desc, 0, sizeof(desc));
    desc.type = cudaExternalMemoryHandleTypeD3D11Resource;
    desc.handle.win32.handle = (void * )handle;
    desc.size = size;
    desc.flags = cudaExternalMemoryDedicated;
    cudaImportExternalMemory(&extMem, &desc);
    // Input parameter 'handle' should be closed if it's not needed anymore
    CloseHandle(handle);
    return extMem;
}
```

如果存在命名句柄，也可以如下所示使用命名句柄导入可共享的 Direct3D 11 资源。

```cpp
cudaExternalMemory_t importD3D11ResourceFromNamedNTHandle(LPCWSTR name, unsigned long long size) {
    cudaExternalMemory_t extMem = NULL;
    cudaExternalMemoryHandleDesc desc = {};
    memset(&desc, 0, sizeof(desc));
    desc.type = cudaExternalMemoryHandleTypeD3D11Resource;
    desc.handle.win32.name = (void * )name;
    desc.size = size;
    desc.flags = cudaExternalMemoryDedicated;
    cudaImportExternalMemory(&extMem, &desc);
    return extMem;
}
```

通过指定 D3D11_RESOURCE_MISC_SHARED 或 D3D11_RESOURCE_MISC_SHARED_KEYEDMUTEX 创建的可共享 Direct3D 11 资源，可以如下所示使用与该对象关联的全局共享 D3DKMT 句柄导入到 CUDA 中。由于全局共享 D3DKMT 句柄不持有对底层内存的引用，因此当对资源的所有其他引用都被销毁时，它会自动销毁。

```cpp
cudaExternalMemory_t importD3D11ResourceFromNtKHandle(HANDLE handle, unsigned long long size) {
    cudaExternalMemory_t extMem = NULL;
    cudaExternalMemoryHandleDesc desc = {};
    memset(&desc, 0, sizeof(desc));
    desc.type = cudaExternalMemoryHandleTypeD3D11ResourceKmt;
    desc.handle.win32.handle = (void *)handle;
    desc.size = size;
    desc.flags = cudaExternalMemoryDedicated;
    cudaImportExternalMemory(&extMem, &desc);
    return extMem;
}
```

### 3.3.4.4.3. 将缓冲区映射到导入的内存对象

如下所示，可以将设备指针映射到导入的内存对象。映射的偏移量和大小必须与使用相应的 Direct3D 11 API 创建映射时指定的偏移量和大小匹配。所有映射的设备指针都必须使用 cudaFree() 释放。

```cpp
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

### 3.3.4.4.4. 将多级渐进纹理数组映射到导入的内存对象

如下所示，可以将 CUDA 多级渐进纹理数组映射到导入的内存对象。偏移量、维度、格式和 mip 级数必须与使用相应的 Direct3D 11 API 创建映射时指定的内容匹配。此外，如果多级渐进纹理数组可以在 Direct3D 12 中绑定为渲染目标，则必须设置标志 cudaArrayColorAttachment。所有映射的多级渐进纹理数组都必须使用 cudaFreeMipmappedArray() 释放。以下代码示例显示

