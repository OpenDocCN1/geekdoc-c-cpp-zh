

返回值是与输入纹理坐标最接近的两个（一维纹理）、四个（二维纹理）或八个（三维纹理）纹素的线性插值。cudaFilterModeLinear 仅对浮点类型的返回值有效。

纹理对象 API 介绍纹理对象 API。

纹理引用 API 介绍纹理引用 API。

16 位浮点纹理说明如何处理 16 位浮点纹理。

纹理还可以分层，如分层纹理中所述。

立方体贴图纹理和立方体贴图分层纹理描述了一种特殊的纹理类型，即立方体贴图纹理。

纹理收集描述了一种特殊的纹理获取，即纹理收集。

### 3.2.11.1.1. 纹理对象 API

纹理对象使用 cudaCreateTextureObject() 从类型为 struct cudaResourceDesc 的资源描述中创建，该描述指定纹理，并从如下定义的纹理描述中创建：

```cpp
struct cudaTextureDesc
{
    enum cudaTextureAddressMode addressMode[3];
    enum cudaTextureFilterMode filterMode;
    enum cudaTextureReadMode readMode;
    int sRGB;
    unsigned int normalizedCoords;
    unsigned int maxAnisotropy;
    enum cudaTextureFilterMode mipmapFilterMode;
    float mipmapLevelBias;
    float minMipmapLevelClamp;
    float maxMipmapLevelClamp;
};
```

- addressMode 指定寻址模式；
- filterMode 指定过滤模式；
- readMode 指定读取模式；
- normalizedCoords 指定纹理坐标是否归一化；
- 有关 sRGB、maxAnisotropy、mipmapFilterMode、mipmapLevelBias、minMipmapLevelClamp 和 maxMipmapLevelClamp，请参阅参考手册。

以下代码示例将简单的变换内核应用于纹理。

```cpp
// Simple transformation kernel
__global__ void transformKernel(float* output,
    cudaTextureObject_t texObj,
    int width, int height,
    float theta)
{
    // Calculate normalized texture coordinates
    unsigned int x = blockIdx.x * blockDim.x + threadIdx.x;
    unsigned int y = blockIdx.y * blockDim.y + threadIdx.y;

    float u = x / (float)width;
    float v = y / (float)height;

    // Transform coordinates
    u -= 0.5f;
    v -= 0.5f;
    float tu = u * cosf(theta) - v * sinf(theta) + 0.5f;
    float tv = v * cosf(theta) + u * sinf(theta) + 0.5f;

    // Read from texture and write to global memory
    output[y * width + x] = tex2D<float>(texObj, tu, tv);
}
```

```cpp
// Host code
int main()
{
    // Allocate CUDA array in device memory
    cudaChannelFormatDesc channelDesc = cudaCreateChannelDesc(32, 0, 0, 0,
                                                              cudaChannelFormatKindFloat);
    cudaArray* cuArray;
    cudaMallocArray(&cuArray, &channelDesc, width, height);

    // Copy to device memory some data located at address h_data
    // in host memory
    cudaMemcpyToArray(cuArray, 0, 0, h_data, size,
                      cudaMemcpyHostToDevice);

    // Specify texture
    struct cudaResourceDesc resDesc;
    memset(&resDesc, 0, sizeof(resDesc));
    resDesc.resType = cudaResourceTypeArray;
    resDesc.res.array.array = cuArray;

    // Specify texture object parameters
    struct cudaTextureDesc texDesc;
    memset(&texDesc, 0, sizeof(texDesc));
    texDesc.addressMode[0] = cudaAddressModeWrap;
    texDesc.addressMode[1] = cudaAddressModeWrap;
    texDesc.filterMode = cudaFilterModeLinear;
    texDesc.readMode = cudaReadModeElementType;
    texDesc.normalizedCoords = 1;

    // Create texture object
    cudaTextureObject_t texObj = 0;
    cudaCreateTextureObject(&texObj, &resDesc, &texDesc, NULL);

    // Allocate result of transformation in device memory
    float *output;
    cudaMalloc(&output, width * height * sizeof(float));

    // Invoke kernel
    dim3 dimBlock(16, 16);
    dim3 dimGrid((width + dimBlock.x - 1) / dimBlock.x,
                 (height + dimBlock.y - 1) / dimBlock.y);
    transformKernel<<<dimGrid, dimBlock>>>(output,
                                           texObj, width, height,
                                           angle);

    // Destroy texture object
    cudaDestroyTextureObject(texObj);

    // Free device memory
    cudaFreeArray(cuArray);
    cudaFree(output);

    return 0;
}
```

### 3.2.11.1.2. 纹理引用 API

纹理引用的某些属性是不可变的，必须在编译时已知；它们在声明纹理引用时指定。纹理引用在文件作用域中声明为类型为 **纹理** 的变量：

```
Texture<DataType, Type, ReadMode> texRef;
```

其中：

- DataType 指定纹素的类型；
- Type 指定纹理引用的类型，对于一维、二维或三维纹理，分别等于 cudaTextureType1D、cudaTextureType2D 或 cudaTextureType3D，或者对于一维或二维分层纹理，分别等于 cudaTextureType1DLayered 或 cudaTextureType2DLayered；Type 是可选参数，默认值为 cudaTextureType1D；
- ReadMode 指定读取模式；它是可选参数，默认值为 cudaReadModeElementType。

纹理引用只能声明为静态全局变量，不能作为参数传递给函数。

纹理引用的其他属性是可变的，可以通过主机运行时在运行时更改。如参考手册中所述，运行时 API 具有低级 C 风格接口和高级 C++ 风格接口。纹理类型在高级 API 中定义为从低级 API 中定义的 textureReference 类型公共派生的结构，如下所示：

```cpp
struct textureReference {
    int
        normalized;
    enum cudaTextureFilterMode
        filterMode;
    enum cudaTextureAddressMode
        addressMode[3];
    struct cudaChannelFormatDesc
        channelDesc;
    int
        sRGB;
    unsigned int
        maxAnisotropy;
    enum cudaTextureFilterMode
        mipmapFilterMode;
    float
        mipmapLevelBias;
    float
        minMipmapLevelClamp;
    float
        maxMipmapLevelClamp;
};
```

- normalized 指定纹理坐标是否归一化；
- filterMode 指定过滤模式；
- addressMode 指定寻址模式；
- channelDesc 描述纹素的格式；它必须与纹理引用声明的 DataType 参数匹配；channelDesc 的类型如下：

```cpp
struct cudaChannelFormatDesc {
    int x, y, z, w;
    enum cudaChannelFormatKind f;
};
```

其中 x、y、z 和 w 等于返回值每个组件的位数，f 为：

- 如果这些组件是有符号整数类型，则为 cudaChannelFormatKindSigned；
- 如果它们是无符号整数类型，则为 cudaChannelFormatKindUnsigned；
- 如果它们是浮点类型，则为 cudaChannelFormatKindFloat。

- 有关 sRGB、maxAnisotropy、mipmapFilterMode、mipmapLevelBias、minMipmapLevelClamp 和 maxMipmapLevelClamp，请参阅参考手册。

normalized、addressMode 和 filterMode 可直接在主机代码中修改。

在内核可以使用纹理引用从纹理内存读取之前，必须使用 cudaBindTexture() 或 cudaBindTexture2D() 将纹理引用绑定到线性内存上的纹理，或使用 cudaBindTextureToArray() 将其绑定到 CUDA 数组。cudaUnbindTexture() 用于解绑纹理引用。纹理引用解绑后，可以安全地重新绑定到另一个数组，即使使用先前绑定纹理的内核尚未完成。建议使用 cudaMallocPitch() 在线性内存中分配二维纹理，并使用 cudaMallocPitch() 返回的步距作为 cudaBindTexture2D() 的输入参数。

以下代码示例将二维纹理引用绑定到 devPtr 指向的线性内存：

- 使用低级 API：

```cpp
texture<float, cudaTextureType2D,
         cudaReadModeElementType> texRef;
textureReference* texRefPtr;
cudaGetTextureReference(&texRefPtr, &texRef);
cudaChannelFormatDesc channelDesc =
    cudaCreateChannelDesc<float>();
size_t offset;
cudaBindTexture2D(&offset, texRefPtr, devPtr, &channelDesc,
                  width, height, pitch);
```

- 使用高级 API：

```cpp
texture<float, cudaTextureType2D,
         cudaReadModeElementType> texRef;
cudaChannelFormatDesc channelDesc =
    cudaCreateChannelDesc<float>();
size_t offset;
cudaBindTexture2D(&offset, texRef, devPtr, channelDesc,
                  width, height, pitch);
```

以下代码示例将二维纹理引用绑定到 CUDA 数组 cuArray：

- 使用低级 API：

```cpp
texture<float, cudaTextureType2D,
         cudaReadModeElementType> texRef;
textureReference* texRefPtr;
cudaGetTextureReference(&texRefPtr, &texRef);
cudaChannelFormatDesc channelDesc;
cudaGetChannelDesc(&channelDesc, cuArray);
cudaBindTextureToArray(texRef, cuArray, &channelDesc);
```

- 使用高级 API：

```cpp
texture<float, cudaTextureType2D,
         cudaReadModeElementType> texRef;
cudaBindTextureToArray(texRef, cuArray);
```

将纹理绑定到纹理引用时指定的格式必须与声明纹理引用时指定的参数匹配；否则，纹理获取的结果是未定义的。

可以绑定到内核的纹理数量有限制，如表 15 所示。

