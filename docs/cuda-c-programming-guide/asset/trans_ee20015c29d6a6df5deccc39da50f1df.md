

### 3.2.12.2.2. Direct3D 10 版本

```cpp
ID3D10Device* device;
struct CUSTOMVERTEX {
    FLOAT x, y, z;
    DWORD color;
};
ID3D10Buffer* positionsVB;
struct cudaGraphicsResource* positionsVB_CUDA;

int main() {
    int dev;
    // Get a CUDA-enabled adapter
    IDXGIFactory* factory;
    CreateDXGIFactory(__uuidof(IDXGIFactory), (void**)&factory);
    IDXGIAdapter* adapter = 0;
    for (unsigned int i = 0; ; ++i) {
        if (FAILED(factory->EnumAdapters(i, &adapter)))
            if (cudaD3D10GetDevice(&dev, adapter) == cudaSuccess)
                break;
        adapter->Release();
    }
    factory->Release();

    // Create swap chain and device
    ...
    D3D10CreateDeviceAndSwapChain(adapter,
    D3D10_DRIVER_TYPE_HARDWARE, 0,
    D3D10_CREATE_DEVICE_DEBUG,
    D3D10_SDK_VERSION,
    &swapChainDesc, &swapChain,
    &device);

    adapter->Release();

    // Use the same device
    cudaSetDevice(dev);

    // Create vertex buffer and register it with CUDA
    unsigned int size = width * height * sizeof(CUSTOMVERTEX);
    D3D10_BUFFER_DESC bufferDesc;
    bufferDesc.Usage = D3D10_USAGE_DEFAULT;
    bufferDesc.ByteWidth = size;
    bufferDesc.BindFlags = D3D10_BIND_VERTEX_BUFFER;
    bufferDesc.CPUAccessFlags = 0;
    bufferDesc.MiscFlags = 0;
    device->CreateBuffer(&bufferDesc, 0, &positionsVB);
    cudaGraphicsD3D10RegisterResource(&positionsVB_CUDA,
    positionsVB,
    cudaGraphicsRegisterFlagsNone);

    cudaGraphicsResourceSetMapFlags(positionsVB_CUDA,
    cudaGraphicsMapFlagsWriteDiscard);

    // Launch rendering loop
    while (...) {
    ...
    Render();
    ...
    }
    ...
}
```

```cpp
void Render()
{
    // Map vertex buffer for writing from CUDA
    float4* positions;
    cudaGraphicsMapResources(1, &positionsVB_CUDA, 0);
    size_t num_bytes;
    cudaGraphicsResourceGetMappedPointer((void**)&positions,
        &num_bytes,
        positionsVB_CUDA);

    // Execute kernel
    dim3 dimBlock(16, 16, 1);
    dim3 dimGrid(width / dimBlock.x, height / dimBlock.y, 1);
    createVertices<<<dimGrid, dimBlock>>>(positions, time,
        width, height);

    // Unmap vertex buffer
    cudaGraphicsUnmapResources(1, &positionsVB_CUDA, 0);

    // Draw and present
    ...
}
```

```cpp
void releaseVB()
{
    cudaGraphicsUnregisterResource(positionsVB_CUDA);
    positionsVB->Release();
}
```

```cpp
__global__ void createVertices(float4* positions, float time,
    unsigned int width, unsigned int height)
{
    unsigned int x = blockIdx.x * blockDim.x + threadIdx.x;
    unsigned int y = blockIdx.y * blockDim.y + threadIdx.y;

    // Calculate uv coordinates
    float u = x / (float)width;
    float v = y / (float)height;
    u = u * 2.0f - 1.0f;
    v = v * 2.0f - 1.0f;

    // Calculate simple sine wave pattern
    float freq = 4.0f;
    float w = sinf(u * freq + time)
        * cosf(v * freq + time) * 0.5f;

    // Write positions
    positions[y * width + x] =
        make_float4(u, w, v, __int_as_float(0xff00ff00));
}
```

### 3.2.12.2.3. Direct3D 11 版本

```cpp
ID3D11Device* device;
struct CUSTOMVERTEX {
    FLOAT x, y, z;
    DWORD color;
};
ID3D11Buffer* positionsVB;
struct cudaGraphicsResource* positionsVB_CUDA;

int main() {
    int dev;
    // Get a CUDA-enabled adapter
    IDXGIFactory* factory;
    CreateDXGIFactory(__uuidof(IDXGIFactory), (void**)&factory);
    IDXGIAdapter* adapter = 0;
    for (unsigned int i = 0; ; ++i) {
        if (FAILED(factory->EnumAdapters(i, &adapter)))
            if (cudaD3D11GetDevice(&dev, adapter) == cudaSuccess)
            {
                break;
            }
        adapter->Release();
    }
    factory->Release();

    // Create swap chain and device
    ...
    D3D11CreateDeviceAndSwapChain(adapter,
        D3D11_DRIVER_TYPE_HARDWARE,
        0,
        D3D11_CREATE_DEVICE_DEBUG,
        featureLevels, 3,
        D3D11_SDK_VERSION,
        &swapChainDesc, &swapChain,
        &device,
        &featureLevel,
        &deviceContext);

    adapter->Release();

    // Use the same device
    cudaSetDevice(dev);

    // Create vertex buffer and register it with CUDA
    unsigned int size = width * height * sizeof(CUSTOMVERTEX);
    D3D11_BUFFER_DESC bufferDesc;
    bufferDesc.Usage = D3D11_USAGE_DEFAULT;
    bufferDesc.ByteWidth = size;
    bufferDesc.BindFlags = D3D11_BIND_VERTEX_BUFFER;
    bufferDesc.CPUAccessFlags = 0;
    bufferDesc.MiscFlags = 0;
    device->CreateBuffer(&bufferDesc, 0, &positionsVB);
    cudaGraphicsD3D11RegisterResource(&positionsVB_CUDA,
        positionsVB,
        cudaGraphicsRegisterFlagsNone);

    cudaGraphicsResourceSetMapFlags(positionsVB_CUDA,
        cudaGraphicsMapFlagsWriteDiscard);

    // Launch rendering loop
    while (...) {
        ...
        Render();
        ...
    }
    ...
}
```

```cpp
void Render()
{
    // Map vertex buffer for writing from CUDA
    float4* positions;
    cudaGraphicsMapResources(1, &positionsVB_CUDA, 0);
    size_t num_bytes;
    cudaGraphicsResourceGetMappedPointer((void**)&positions,
                                         &num_bytes,
                                         positionsVB_CUDA);

    // Execute kernel
    dim3 dimBlock(16, 16, 1);
    dim3 dimGrid(width / dimBlock.x, height / dimBlock.y, 1);
    createVertices<<<dimGrid, dimBlock>>>(positions, time,
                                          width, height);

    // Unmap vertex buffer
    cudaGraphicsUnmapResources(1, &positionsVB_CUDA, 0);

    // Draw and present
    ...
}

void releaseVB()
{
    cudaGraphicsUnregisterResource(positionsVB_CUDA);
    positionsVB->Release();
}

__global__ void createVertices(float4* positions, float time,
                               unsigned int width, unsigned int height)
{
    unsigned int x = blockIdx.x * blockDim.x + threadIdx.x;
    unsigned int y = blockIdx.y * blockDim.y + threadIdx.y;

    // Calculate uv coordinates
    float u = x / (float)width;
    float v = y / (float)height;
    u = u * 2.0f - 1.0f;
    v = v * 2.0f - 1.0f;

    // Calculate simple sine wave pattern
    float freq = 4.0f;
    float w = sinf(u * freq + time)
             * cosf(v * freq + time) * 0.5f;

    // Write positions
    positions[y * width + x] =
        make_float4(u, w, v, __int_as_float(0xff00ff00));
}
```

### 3.2.12.3. SLI 互操作性

在多 GPU 系统中，所有支持 CUDA 的 GPU 均可通过 CUDA 驱动程序和运行时作为独立设备访问。但是，当系统处于 SLI 模式时，如下所述存在特殊注意事项。

首先，一个 GPU 上某个 CUDA 设备的分配会占用 Direct3D 或 OpenGL 设备的 SLI 配置中其他 GPU 的内存。因此，分配可能会比预期更早失败。

其次，应用程序应为 SLI 配置中的每个 GPU 创建多个 CUDA 上下文，每个 GPU 一个。虽然这不是严格要求，但可以避免设备之间不必要的数据传输。应用程序可以使用针对 Direct3D 的 cudaD3D[9|10|11]GetDevices() 和针对 OpenGL 的 cudaGLGetDevices() 调用集来识别当前帧和下一帧中正在执行渲染的设备的 CUDA 设备句柄。基于此信息，应用程序通常会选择适当的设备，并将 Direct3D 或 OpenGL 资源映射到 cudaD3D[9|10|11]GetDevices() 返回的 CUDA 设备上（或者当 deviceList 参数设置为 cudaD3D[9|10|11]DeviceListCurrentFrame 或 cudaGLDeviceListCurrentFrame 时，使用 cudaGLGetDevices()）。

请注意，cudaGraphicsD3D[9|10|11]RegisterResource 和 cudaGraphicsGLRegister[Buffer|Image] 返回的资源只能在发生注册的设备上使用。因此，在 SLI 配置中，当不同帧的数据在不同的 CUDA 设备上计算时，有必要为每个设备分别注册资源。

有关 CUDA 运行时如何分别与 Direct3D 和 OpenGL 互操作的详细信息，请参阅 Direct3D 互操作性和 OpenGL 互操作性。

## 3.3. 外部资源互操作性

外部资源互操作性允许 CUDA 导入由其他 API 显式导出的某些资源。这些对象通常由其他 API 使用操作系统原生句柄导出，例如 Linux 上的文件描述符或 Windows 上的 NT 句柄。它们也可以使用其他统一接口导出，例如 NVIDIA 软件通信接口。可导入的资源有两种类型：内存对象和同步对象。

内存对象可以使用 cudaImportExternalMemory() 导入到 CUDA 中。导入的内存对象可以通过 cudaExternalMemoryGetMappedBuffer() 映射到内存对象上的设备指针，或通过 cudaExternalMemoryGetMappedMipmappedArray() 映射的 CUDA mipmapped 数组，在内核中访问。取决于内存对象的类型，可能在单个内存对象上设置多个映射。映射必须与导出 API 中设置的映射匹配。任何不匹配的映射都会导致未定义行为。导入的内存对象必须使用 cudaDestroyExternalMemory() 释放。释放内存对象不会释放到该对象的任何映射。因此，映射到该对象的任何设备指针都必须使用 cudaFree() 显式释放，映射到该对象的任何 CUDA mipmapped 数组都必须使用 cudaFreeMipmappedArray() 显式释放。在对象销毁后访问其映射是非法的。

同步对象可以使用 cudaImportExternalSemaphore() 导入到 CUDA 中。导入的同步对象随后可以使用 cudaSignalExternalSemaphoresAsync() 发出信号，并使用 cudaWaitExternalSemaphoresAsync() 等待。在相应的信号发出之前发出等待是非法的。此外，取决于导入的同步对象的类型，可能会对其信号发出和等待方式施加其他约束，如后续章节所述。导入的信号量对象必须使用 cudaDestroyExternalSemaphore() 释放。在销毁信号量对象之前，所有未完成的信号和等待必须已完成。

