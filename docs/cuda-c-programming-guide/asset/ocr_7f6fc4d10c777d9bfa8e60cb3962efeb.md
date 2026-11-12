# 3.2.12.2.2. Direct3D 10 Version

```
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
    IDXGIAdapter *__uidof(IDXGIFactory)), (void**)&factory);
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