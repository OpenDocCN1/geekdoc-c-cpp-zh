

以下代码示例将一些简单的变换内核应用于纹理。

```cpp
// Simple copy kernel
__global__ void copyKernel(cudaSurfaceObject_t inputSurfObj,
                           cudaSurfaceObject_t outputSurfObj,
                           int width, int height)
{
    // Calculate surface coordinates
    unsigned int x = blockIdx.x * blockDim.x + threadIdx.x;
    unsigned int y = blockIdx.y * blockDim.y + threadIdx.y;
    if ((x < width) && (y < height)) {
        // Read from input surface
        uchar4 data;
        surf2DRead(&data, inputSurfObj, x * 4, y);
        // Write to output surface
        surf2DWrite(data, outputSurfObj, x * 4, y);
    }
}

// Host code
int main()
{
    // Allocate CUDA arrays in device memory
    cudaChannelFormatDesc channelDesc =
        cudaCreateChannelDesc(8, 8, 8, 8,
                              cudaChannelFormatKindUnsigned);
    cudaArray* cuInputArray;
    cudaMallocArray(&cuInputArray, &channelDesc, width, height,
                    cudaArraySurfaceLoadStore);
    cudaArray* cuOutputArray;
    cudaMallocArray(&cuOutputArray, &channelDesc, width, height,
                    cudaArraySurfaceLoadStore);

    // Copy to device memory some data located at address h_data
    cudaMemcpyToArray(cuInputArray, 0, 0, h_data, size,
                      cudaMemcpyHostToDevice);

    // Specify surface
    struct cudaResourceDesc resDesc;
    memset(&resDesc, 0, sizeof(resDesc));
    resDesc.resType = cudaResourceTypeArray;
    resDesc.res.array.array = cuInputArray;

    // Create the surface objects
    resDesc.res.array.array = cuInputArray;
    cudaSurfaceObject_t inputSurfObj = 0;
    cudaCreateSurfaceObject(&inputSurfObj, &resDesc);
    resDesc.res.array.array = cuOutputArray;
    cudaSurfaceObject_t outputSurfObj = 0;
    cudaCreateSurfaceObject(&outputSurfObj, &resDesc);

    // Invoke kernel
    dim3 dimBlock(16, 16);
    dim3 dimGrid((width + dimBlock.x - 1) / dimBlock.x,
                 (height + dimBlock.y - 1) / dimBlock.y);
    copyKernel<<<dimGrid, dimBlock>>>(inputSurfObj,
                                      outputSurfObj,
                                      width, height);

    // Destroy surface objects
    cudaDestroySurfaceObject(inputSurfObj);
    cudaDestroySurfaceObject(outputSurfObj);

    // Free device memory
    cudaFreeArray(cuInputArray);
    cudaFreeArray(cuOutputArray);

    return 0;
}
```

### 3.2.11.2.2. 表面引用 API

表面引用在文件作用域中声明为 surface 类型的变量：

```cpp
surface<void, Type> surfRef;
```

其中 `Type` 指定表面引用的类型，等于 `cudaSurfaceType1D`、`cudaSurfaceType2D`、`cudaSurfaceType3D`、`cudaSurfaceTypeCubemap`、`cudaSurfaceType1DLayered`、`cudaSurfaceType2DLayered` 或 `cudaSurfaceTypeCubemapLayered`；`Type` 是可选参数，默认值为 `cudaSurfaceType1D`。表面引用只能声明为静态全局变量，不能作为参数传递给函数。

在内核使用表面引用访问 CUDA 数组之前，必须使用 `cudaBindSurfaceToArray()` 将表面引用绑定到 CUDA 数组。

以下代码示例将表面引用绑定到 CUDA 数组 `cuArray`：

- 使用低级 API：

```cpp
surface<void, cudaSurfaceType2D> surfRef;
surfaceReference* surfRefPtr;
cudaGetSurfaceReference(&surfRefPtr, "surfRef");
cudaChannelFormatDesc channelDesc;
cudaGetChannelDesc(&channelDesc, cuArray);
cudaBindSurfaceToArray(surfRef, cuArray, channelDesc);
```

- 使用高级 API：

```cpp
surface<void, cudaSurfaceType2D> surfRef;
cudaBindSurfaceToArray(surfRef, cuArray);
```

CUDA 数组必须使用与维度和类型匹配的表面函数，并通过与维度匹配的表面引用进行读写；否则，读写 CUDA 数组的结果是未定义的。

与纹理内存不同，表面内存使用字节寻址。这意味着，通过纹理函数访问纹理元素时使用的 x 坐标需要乘以元素的字节大小，才能通过表面函数访问同一元素。例如，对于绑定到纹理引用 `texRef` 和表面引用 `surfRef` 的一维浮点 CUDA 数组，纹理坐标 x 处的元素通过 `texRef` 使用 `tex1D(texRef, x)` 读取，但通过 `surfRef` 使用 `surf1Dread(surfRef, 4*x)` 读取。同样，对于绑定到纹理引用 `texRef` 和表面引用 `surfRef` 的二维浮点 CUDA 数组，纹理坐标 x 和 y 处的元素通过 `texRef` 使用 `tex2D(texRef, x, y)` 访问，但通过 `surfRef` 使用 `surf2Dread(surfRef, 4*x, y)` 访问（y 坐标的字节偏移量在内部从 CUDA 数组的底层行步距计算得出）。

以下代码示例将一些简单的变换内核应用于纹理。

```cpp
// 2D surfaces
surface<void, 2> inputSurfRef;
surface<void, 2> outputSurfRef;

// Simple copy kernel
__global__ void copyKernel(int width, int height)
{
    // Calculate surface coordinates
    unsigned int x = blockIdx.x * blockDim.x + threadIdx.x;
    unsigned int y = blockIdx.y * blockDim.y + threadIdx.y;
    if (x < width && y < height) {
        uchar4 data;
        // Read from input surface
        surf2Dread(&data, inputSurfRef, x * 4, y);
        // Write to output surface
        surf2Dwrite(data, outputSurfRef, x * 4, y);
    }
}

// Host code
int main()
{
    // Allocate CUDA arrays in device memory
    cudaChannelFormatDesc channelDesc =
        cudaCreateChannelDesc(8, 8, 8, 8,
                              cudaChannelFormatKindUnsigned);
    cudaArray* cuInputArray;
    cudaMallocArray(&cuInputArray, &channelDesc, width, height,
                    cudaArraySurfaceLoadStore);
    cudaArray* cuOutputArray;
    cudaMallocArray(&cuOutputArray, &channelDesc, width, height,
                    cudaArraySurfaceLoadStore);

    // Copy to device memory some data located at address h_data
    // In host memory
    cudaMemcpyToArray(cuInputArray, 0, 0, h_data, size,
                      cudaMemcpyHostToDevice);

    // Bind the arrays to the surface references
    cudaBindSurfaceToArray(inputSurfRef, cuInputArray);
    cudaBindSurfaceToArray(outputSurfRef, cuOutputArray);

    // Invoke kernel
    dim3 dimBlock(16, 16);
    dim3 dimGrid((width + dimBlock.x - 1) / dimBlock.x,
                 (height + dimBlock.y - 1) / dimBlock.y);
    copyKernel<<<dimGrid, dimBlock>>>(width, height);

    // Free device memory
    cudaFreeArray(cuInputArray);
    cudaFreeArray(cuOutputArray);

    return 0;
}
```

### 3.2.11.2.3. 立方体贴图表面

立方体贴图表面使用 surfCubemapread() 和 surfCubemapwrite() 作为二维分层表面进行访问，即使用表示面的整数索引和两个浮点纹理坐标来寻址该面对应层中的纹理元素。面的顺序如表 2 所示。

### 3.2.11.2.4. 立方体贴图分层表面

立方体贴图分层表面使用 `surfCubemapLayeredread()` 和 `surfCubemapLayeredwrite()` 作为二维分层表面进行访问，即使用表示某个立方体贴图面的整数索引和两个浮点纹理坐标来寻址该面对应层中的纹理元素。面的顺序如表 2 所示，例如，索引 ((2 * 6) + 3) 访问第三个立方体贴图的第四个面。

### 3.2.11.13. CUDA 数组

CUDA 数组是针对纹理获取优化的不透明内存布局。它们是一维、二维或三维的，由元素组成，每个元素具有 1、2 或 4 个分量，这些分量可以是有符号或无符号的 8 位、16 位或 32 位整数，16 位浮点数，或 32 位浮点数。CUDA 数组仅可通过内核按照纹理内存中描述的纹理获取或按照表面内存中描述的表面读写来访问。

### 3.2.11.14. 读写一致性

纹理和表面内存是缓存的（参见设备内存访问），在同一内核调用中，缓存不与全局内存写入和表面内存写入保持一致，因此对同一内核调用中通过全局写入或表面写入已写入的地址进行的任何纹理获取或表面读取都将返回未定义的数据。换句话说，只有当某个纹理或表面内存位置是由之前的内核调用或内存复制更新的，而非由同一内核调用中的同一线程或另一线程之前更新时，线程才能安全地读取该位置。

### 3.2.12. 图形互操作性

OpenGL 和 Direct3D 的某些资源可以映射到 CUDA 的地址空间中，以便让 CUDA 能够读取 OpenGL 或 Direct3D 写入的数据，或者让 CUDA 能够写入供 OpenGL 或 Direct3D 使用的数据。

资源必须先注册到 CUDA，然后才能使用 OpenGL 互操作性和 Direct3D 互操作性中提到的函数进行映射。这些函数返回类型为 `struct cudaGraphicsResource` 的 CUDA 图形资源指针。注册资源可能开销较高，因此通常每个资源只调用一次。CUDA 图形资源使用 `cudaGraphicsUnregisterResource()` 注销。每个打算使用该资源的 CUDA 上下文都需要单独注册它。

资源注册到 CUDA 后，可以使用 `cudaGraphicsMapResources()` 和 `cudaGraphicsUnmapResources()` 按需要多次映射和取消映射。可以调用 `cudaGraphicsResourceSetMapFlags()` 来指定使用提示（仅写入、仅读取），CUDA 驱动程序可使用这些提示来优化资源管理。

