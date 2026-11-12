

映射的资源可以通过内核使用 cudaGraphicsResourceGetMappedPointer() 为缓冲区返回的设备内存地址，以及使用 cudaGraphicsSubResourceGetMappedArray() 为 CUDA 数组返回的地址进行读取或写入。

在资源被映射期间，通过 OpenGL、Direct3D 或另一个 CUDA 上下文访问该资源会产生未定义的结果。OpenGL 互操作性和 Direct3D 互操作性分别针对每个图形 API 提供了具体说明和一些代码示例。SLI 互操作性针对系统处于 SLI 模式时的情况提供了具体说明。

## 3.2.12.1. OpenGL 互操作性

可以映射到 CUDA 地址空间的 OpenGL 资源包括 OpenGL 缓冲区、纹理和呈现缓冲区对象。

缓冲区对象使用 cudaGraphicsGLRegisterBuffer() 进行注册。在 CUDA 中，它表现为一个设备指针，因此可以由内核读取和写入，或通过 cudaMemcpy() 调用进行读写。

纹理或呈现缓冲区对象使用 cudaGraphicsGLRegisterImage() 进行注册。在 CUDA 中，它表现为一个 CUDA 数组。内核可以通过将其绑定到纹理或表面引用来从数组中读取。如果资源已使用 cudaGraphicsRegisterFlagsSurfaceLoadStore 标志注册，它们也可以通过表面写入函数向其中写入。该数组还可以通过 cudaMemcpy2D() 调用进行读取和写入。cudaGraphicsGLRegisterImage() 支持具有 1、2 或 4 个分量且内部类型为 float（例如 GL_RGBA_FLOAT32）、归一化整数（例如 GL_RGBA8、GL_INTENSITY16）和非归一化整数（例如 GL_RGBA8UI）的所有纹理格式（请注意，由于非归一化整数格式需要 OpenGL 3.0，它们只能由着色器写入，而不能由固定功能管道写入）。

正在共享其资源的 OpenGL 上下文必须是发出任何 OpenGL 互操作性 API 调用的主机线程的当前上下文。

请注意：当 OpenGL 纹理设置为无绑定（例如，通过使用 glGetTextureHandle*/glGetImageHandle* API 请求图像或纹理句柄）时，它无法与 CUDA 注册。应用程序需要在请求图像或纹理句柄之前先将纹理注册为互操作。

```
GLuint positionsVBO;
struct cudaGraphicsResource* positionsVBO_CUDA;
int main()
{
    // Initialize OpenGL and GLUT for device 0
    // and make the OpenGL context current
    ...
    glutDisplayFunc(display);
    ...
    // Explicitly set device 0
    cudaSetDevice(0);
    ...
    // Create buffer object and register it with CUDA
    glGenBuffers(1, &positionsVBO);
    glBindBuffer(GL_ARRAY_BUFFER, positionsVBO);
    glBufferData(GL_ARRAY_BUFFER, width * height * sizeof(float),
                 0, GL_DYNAMIC_DRAW);
    glBindBuffer(GL_ARRAY_BUFFER, 0);
    cudaGraphicsGLRegisterBuffer(&positionsVBO_CUDA,
                                 positionsVBO,
                                 cudaGraphicsMapFlagsWriteDiscard);
    ...
    // Launch rendering loop
    glutMainLoop();
    ...
}
void display()
{
    // Map buffer object for writing from CUDA
    float* positions;
    cudaGraphicsMapResources(1, &positionsVBO_CUDA, 0);
    size_t num_bytes;
    cudaGraphicsResourceGetMappedPointer((void**)&positions,
                                         &num_bytes,
                                         positionsVBO_CUDA);
    ...
    // Execute kernel
    dim3 dimBlock(16, 16, 1);
    dim3 dimGrid(width / dimBlock.x, height / dimBlock.y, 1);
    createVertices<<<dimGrid, dimBlock>>>(positions, time,
                                          width, height);
    ...
    // Unmap buffer object
    cudaGraphicsUnmapResources(1, &positionsVBO_CUDA, 0);
    ...
    // Render from buffer object
    glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);
    glBindBuffer(GL_ARRAY_BUFFER, positionsVBO);
    glVertexPointer(4, GL_FLOAT, 0, 0);
    glEnableClientState(GL_VERTEX_ARRAY);
    glDrawArrays(GL_POINTS, 0, width * height);
    glDisableClientState(GL_VERTEX_ARRAY);
    ...
    // Swap buffers
    glutSwapBuffers();
    glutPostRedisplay();
}

void deleteVBO()
{
    cudaGraphicsUnregisterResource(positionsVBO_CUDA);
    glDeleteBuffers(1, &positionsVBO);
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

    // calculate simple sine wave pattern
    float freq = 4.0f;
    float w = sinf(u * freq + time)
             * cosf(v * freq + time) * 0.5f;

    // Write positions
    positions[y * width + x] = make_float4(u, w, v, 1.0f);
}
```

在 Windows 和 Quadro GPU 上，可以使用 `cudaWGLGetDevice()` 检索与 `wglEnumGpusNV()` 返回的句柄关联的 CUDA 设备。在多 GPU 配置中，如果 OpenGL 渲染在 Quadro GPU 上执行，而 CUDA 计算在系统中的其他 GPU 上执行，则 Quadro GPU 提供的 OpenGL 互操作性性能高于 GeForce 和 Tesla GPU。

## 3.2.12.2. Direct3D 互操作性

支持 Direct3D 9Ex、Direct3D 10 和 Direct3D 11 的 Direct3D 互操作性。

CUDA 上下文只能与满足以下条件的 Direct3D 设备进行互操作：Direct3D 9Ex 设备必须使用 `DeviceType` 设置为 `D3DDEVTYPE_HAL` 且 `BehaviorFlags` 具有 `D3DCREATE_HARDWARE_VERTEXPROCESSING` 标志来创建；Direct3D 10 和 Direct3D 11 设备必须使用 `DriverType` 设置为 `D3D_DRIVER_TYPE_HARDWARE` 来创建。

可以映射到 CUDA 地址空间的 Direct3D 资源包括 Direct3D 缓冲区、纹理和表面。这些资源使用 `cudaGraphicsD3D9RegisterResource()`、`cudaGraphicsD3D10RegisterResource()` 和 `cudaGraphicsD3D11RegisterResource()` 进行注册。

以下代码示例使用内核动态修改存储在顶点缓冲区对象中的 2D `width` × `height` 顶点网格。

### 3.2.12.2.1. Direct3D 9 版本

```
IDirect3D9* D3D;
IDirect3DDevice9* device;
struct CUSTOMVERTEX {
    FLOAT x, y, z;
    DWORD color;
};
IDirect3DVertexBuffer9* positionsVB;
struct cudaGraphicsResource* positionsVB_CUDA;

int main()
{
    // Init dev;
    // Initialize Direct3D
    D3D = Direct3DCreate9Ex(D3D_SDK_VERSION);

    // Get a CUDA-enabled adapter
    unsigned int adapter = 0;
    for (int adapter = 0; adapter < g_pD3D->GetAdapterCount(); adapter++) {
        D3DADAPTER_IDENTIFIER9 adapterId;
        g_pD3D->GetAdapterIdentifier(adapter, 0, &adapterId);
        if (cudaD3D9GetDevice(&dev, adapterId.DeviceName)
            == cudaSuccess)
            break;
    }

    // Create device
    D3D->CreateDeviceEx(adapter, D3DDEVTYPE_HAL, hWnd,
        D3DCREATE_HARDWARE_VERTEXPROCESSING,
        sparams, NULL, &device);

    // Use the same device
    cudaSetDevice(dev);

    // Create vertex buffer and register it with CUDA
    unsigned int size = width * height * sizeof(CUSTOMVERTEX);
    device->CreateVertexBuffer(size, 0, D3DFVF_CUSTOMVERTEX,
        D3DPOOL_DEFAULT, &positionsVB, 0);
    cudaGraphicsD3D9RegisterResource(&positionsVB_CUDA,
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

void Render()
{
    // Map vertex buffer for writing from CUDA
    float4 * positions;
    cudaGraphicsMapResources(1, &positionsVB_CUDA, 0);
    size_t num_bytes;
    cudaGraphicsResourceGetMappedPointer((void **)&positions,
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

__global__ void createVertices(float4 * positions, float time,
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

