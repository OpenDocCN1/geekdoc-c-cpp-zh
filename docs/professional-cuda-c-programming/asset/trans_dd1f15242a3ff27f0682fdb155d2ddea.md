

# 内存分配与释放

CUDA 编程模型假设系统是异构的，由主机（host）和设备（device）组成，它们拥有各自独立的内存空间。内核函数（Kernel functions）在设备内存空间中运行，而 CUDA 运行时提供了用于分配和释放设备内存的函数。你可以使用以下函数在主机上分配全局内存：

```
cudaError_t cudaMalloc(void **devPtr, size_t count);
```

该函数在设备上分配指定字节数的全局内存，并将该内存的地址通过 `devPtr` 返回。所分配的内存对于任何变量类型（包括整数、浮点值、布尔值等）都经过适当对齐。`cudaMalloc` 函数在失败时返回 `cudaError`。分配的全局内存中所包含的值不会被清空。你有责任用从主机传输的数据填充分配的全局内存，或者使用以下函数对其进行初始化：

```
cudaError_t cudaMemset(void *devPtr, int value, size_t count);
```

该函数将从设备内存地址 `devPtr` 开始的 `count` 个字节中的每个字节填充为变量 `value` 中存储的值。

一旦应用程序不再使用某块分配的全局内存，可以使用以下函数将其释放：

```
cudaError_t cudaFree(void *devPtr);
```

该函数释放由 `devPtr` 指向的全局内存，该内存必须之前已使用设备分配函数（如 `cudaMalloc`）分配过。否则，它将返回错误 `cudaErrorInvalidDevicePointer`。如果该地址已经被释放，`cudaFree` 也会返回错误。

设备内存的分配和释放是非常开销较大的操作，因此应尽可能重用设备内存，以减少对整体性能的影响。

# 内存传输

一旦分配了全局内存，你可以使用以下函数从主机将数据传输到设备：

```
cudaError_t cudaMempy(void *dst, const void *src, size_t count,
enum cudaMemcpyKind kind);
```

该函数将字节从内存位置 `src` 拷贝到内存位置 `dst`。变量 `kind` 指定了拷贝的方向，并可以取以下值：

```
cudaMemcpyHostToHost
cudaMemcpyHostToDevice
cudaMempyDeviceToHost
cudaMemcpyDeviceToDevice
```

如果指针 `dst` 和 `src` 的方向与 `kind` 指定的方向不符，则 `cudaMempy` 的行为未定义。该函数在大多数情况下表现为同步行为。

列表 4-2 显示了使用 `cudaMempy` 的示例。该示例在主机和设备之间传输数据。全局内存使用 `cudaMalloc` 分配，数据使用指定为 `cudaMemcpyHostToDevice` 的方向传输到设备。使用 `cudaMempy` 和 `cudaMemcpyDeviceToHost` 方向将数据传回主机。

# 列表 4-2: 简单的内存传输 (memTransfer.cu)

```
#include <cuda_runtime.h>
#include <stdio.h>

int main(int argc, char **argv) {
    // 设置设备
    int dev = 0;
    cudaSetDevice(dev);

    // 内存大小
    unsigned int size = 1<<22;
    unsigned int nbytes = size * sizeof(float);

    // 获取设备信息
    cudaDeviceProp deviceProp;
    cudaGetDeviceProperties(&deviceProp, dev);
    printf("%d starting at %s\n", argv[0]);
    printf("%d: %d size %d bytes %.2fMB\n", dev, deviceProp.name, nbytes/(1024.0*1024.0));

    // 分配主机内存
    float *h_a = (float*)malloc(nbytes);

    // 分配设备内存
    float *d_a;
    cudaMalloc((float **)&d_a, nbytes);

    // 初始化主机内存
    for(unsigned i=0;i<size;i++) h_a[i] = 0.5f;

    // 将数据传输到设备
    cudaMemcpy(d_a, h_a, nbytes, cudaMemcpyHostToDevice);

    // 将数据从设备传输到主机
    cudaMemcpy(h_a, d_a, nbytes, cudaMemcpyDeviceToHost);

    // 释放内存
    cudaFree(d_a);
    free(h_a);

    // 重置设备
    cudaDeviceReset();
    return EXIT_SUCCESS;
}
```

使用 `nvcc` 编译代码并使用 `nvprof` 运行如下：

```
$ nvcc -O3 memTransfer.cu -o memTransfer
$ nvprof ./memTransfer
```

在 Fermi M2090 上运行的输出所示：

```
=3369= NVPROF is profiling process 3369, command: .memTransfer
 /memTransfer starting at device 0: Tesla M2090 memory size 4194304 nbyte 16.00MB
=3369= Profiling application: .memTransfer
=3369= Profiling result:
Time (%) Time Calls Avg Max Name
53.50% 3.7102ms 1 3.7102ms 3.7102ms [CUDA memcpy DToH]
46.50% 3.2249ms 1 3.2249ms 3.2249ms [CUDA memcpy HToD]
```

从主机到设备的的数据传输被标记为 HToD，从设备到主机的标记为 DToH。图 4-3 显示了 CPU 和 GPU 的连接性。从图中可以看到 CPU 和 GPU 的关系。从主机到设备的数据传输被标记为 HToD，从设备到主机的标记为 DToH。

