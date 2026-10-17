
为了允许内核从零拷贝内存读取，你需要将数组 `A` 和 `B` 分配为映射锁页内存。然后你可以直接在设备上初始化数组 `A` 和 `B`，而无需将它们传输到设备内存。接下来，获取映射锁页内存的设备指针供内核使用。内存分配并初始化后，调用内核。

### 列表 4-3：使用零拷贝内存求和 (`sumArrayZerocopy.cu`)

（列出的 `main` 函数）

```
int main(int argc, char **argv) {
    // part 0: set up device and array
    // set up device
    int dev = 0;
    cudaSetDevice(dev);

    // get device properties
    cudaDeviceProp deviceProp;
    cudaGetDeviceProperties(&deviceProp, dev);

    // check if supported memory
    if (!deviceProp.canMapHostMemory()) {
        printf("Device %d does not support mapping CPU host memory!\n", dev);
        cudaDeviceReset(0);
        exit(EXIT_SUCCESS);
    }

    // set up size of vectors
    int ipower = 10;
    if (argc > 1) ipower = atoi(argv[1]);
    int nElem = 1<<ipower;
    size_t nbytes = nElem * sizeof(float);
    if (ipower < 18) {
        printf("Vector size %d power %d nbytes %.3f KB\n", nElem, ipower, (float)nbytes/(1024.0));
    } else {
        printf("Vector size %d power %d nbytes %.3f MB\n", nElem, ipower, (float)nbytes/(1024.0*1024.0));
    }

    // part 1: using device memory
    // malloc host memory
    float *h_A, *h_B, *hostRef, *gpuRef;
    h_A = (float *)malloc(nbytes);
    h_B = (float *)malloc(nbytes);
    hostRef = (float *)malloc(nbytes);
    gpuRef = (float *)malloc(nbytes);

    // initialize data at host side
    initialData(h_A, nElem);
    initialData(h_B, nElem);
    memset(hostRef, 0, nbytes);
    memset(gpuRef, 0, nbytes);

    // add vector at host side for result checks
    sumArraysOnHost(h_A, h_B, hostRef, nElem);

    // malloc device global memory
    float *d_A, *d_B, *d_C;
    cudaMalloc((float**)&d_A, nbytes);
    cudaMalloc((float**)&d_B, nbytes);
    cudaMalloc((float**)&d_C, nbytes);

    // transfer data from host to device
    memcpy(d_A, h_A, nbytes, cudaMemcpyToDevice);
    memcpy(d_B, h_B, nbytes, cudaMemcpyToDevice);

    // set up execution
    int ilen = 512;
    dim3 block(ilen);
    dim3 grid((nElem+block.x)/block.x);

    // invoke kernel at host side
    sumArrays<<<grid, block>>>(d_A, d_B, d_C);

    // copy kernel result back to host side
    memcpy(gpuRef, d_C, nbytes, cudaMemcpyToHost);

    // check device memory
    checkResult(hostRef, gpuRef, nElem);
    cudaFree(d_A);
    cudaFree(d_B);
    free(h_A);
    free(h_B);

    // part 2: using zerocopy memory for array B
    // allocate memory
    int flags = cudaHostAllocMapped;
    cudaMalloc((void**)&h_A, nbytes, flags);
    cudaMalloc((void**)&h_B, nbytes, flags);

    // initialize data at host side
    initialData(h_A, nElem);
    initialData(h_B, nElem);
    memset(hostRef, 0, nbytes);
    memset(gpuRef, 0, nbytes);

    // pass the pointer to device
    cudaGetDevicePointer((void**)&d_A, h_A, 0);
    cudaGetDevicePointer((void**)&d_B, h_B, 0);

    // add host to host side for result checks
    sumArraysOnHost(h_A, h_B, hostRef, nElem);

    // executeZeroCopy with zero copy memory
    sumArraysZeroCopy<<<grid, block>>>(d_A, d_B, d_C);

    // copy kernel result back to host side
    memcpy(gpuRef, d_C, nbytes, cudaMemcpyToHost);

    // check device results
    checkResult(hostRef, gpuRef, nElem);

    // free memory
    cudaFree(d_C);
    cudaFreeHost(h_A);
    cudaFreeHost(h_B);
    free(hostRef);
    free(gpuRef);

    // reset device
    cudaDeviceReset();
    return EXIT_SUCCESS;
}
```

使用以下命令编译源代码：

```
$ nvcc -O3 -arch=sm_20 sumArrayZeroCopy.cu -o sumZeroCopy
```

使用 `nvprof` 收集分析信息。来自 M2090 的示例输出如下：

```
$ nvprof ../sumZeroCopy
Using Device 0: Tesla M2090 Vector size 1024 power 10 nbytes 4 KB
Time (%) | Calls Avg Max Name
27.18% | 3.77600us 1 3.77600us 3.77600us sumArraysZeroCopy
11.80% | 1.63900us 3 1.63900us 1.63900us sumArrays
25.56% | 3.55200us 3 1.18400us 1.02400us 1.50400us [CUDA memory HtoD]
35.47% | 4.92800us 2 2.46400us 2.46400us 2.46400us [CUDA memory DtoH]
```

比较 `sumArraysZeroCopy` 内核与 `sumArrays` 内核的时间。处理 1024 个元素时，从零拷贝内存运行的内核估计时间比仅使用设备内存的内核慢 2.31 倍。注意报告传输（DtoH）的时间包含了两个内核的时间，因为它们都使用 `cudaMemcpy` 用设备计算的结果更新主机。

接下来，你可以通过以下命令检查不同数组大小的性能。示例结果汇总表 4-3。

```
$ ./sumZeroCopy <size-2>
```

# 表 4-3：零拷贝内存与设备内存的比较

| 大小 | 设备内存（经过时间） | 零拷贝内存（经过时间） | 减慢倍数 |
|---|---|---|---|
| 1 K | 1.5820 us | 2.9150 us | 1.84 |
| 4 K | 1.6640 us | 3.7900 us | 2.28 |
| 16 K | 1.6740 us | 7.4570 us | 4.45 |
| 64 K | 2.3910 us | 22.586 us | 9.45 |
| 256 K | 7.2890 us | 82.733 us | 11.35 |
| 1 M | 28.267 us | 321.57 us | 11.38 |
| 4 M | 104.177 us | 1.2741 ms | 12.23 |
| 16 M | 408.03 us | 5.0903 ms | 12.47 |
| 64 M | 1.6276 ms | 20.347 ms | 12.50 |

Tesla M2090 ECC on L1 cache enabled

Slowdown = 零拷贝读取经过时间 / 设备内存经过时间

## 统一虚拟体系

计算能力为 2.0 及以上的设备支持一种名为统一虚拟体系（Unified Virtual Addressing, UVA）的特殊寻址模式，它在 CUDA 4.0 中引入，并支持 64 位 Linux 系统。通过 UVA，主机内存和设备内存共享同一个虚拟地址空间，如图 4-5 所示。

![](img/506ba3a4c9f4512233692f3f20de1f3a_183_0.png)

在 UVA 之前，你需要管理指向主机内存的指针和指向设备内存的指针。使用 UVA 后，指针引用的内存空间对应用程序代码是透明的。

在 UVA 下，使用 `cudaHostAlloc` 分配的固定主机内存具有相同的主机指针和设备指针。你可以直接将返回的指针传递给内核函数。回想上一节中的零拷贝示例，其中：

- 分配了映射的固定主机内存。
- 使用 CUDA 运行时函数获取映射的固定内存的设备指针。
- 将设备指针传递给你的内核。

有了 UVA，无需获取设备指针或管理两个物理上相同数据的指针。UVA 进一步简化了上一节中的 `sumArrayZeroCopy.cu` 示例：

```
// 在主机侧分配零拷贝内存
cudaHostAlloc(void** h_A, nBytes, cudaHostAllocMapped);
cudaHostAlloc(void** h_B, nBytes, cudaHostAllocMapped);

// 在主机侧初始化数据
initialData(h_A, nElem);
initialData(h_B, nElem);

// 使用零拷贝内存调用内核
sumArraysZeroCopy<<<grid, block>>>(h_A, h_B, d_C, nElem);
```

注意，`cudaHostAlloc` 返回的指针被直接传递给内核。使用 UVA 的更新后的代码可以在 Wrox.com 上的 `sumArrayZerocpyUVA.cu` 中找到。可以使用以下命令进行编译：

```
$ nvcc -03 -arch=sm_20 sumArrayZerocpyUVA.cu -o sumArrayZerocpyUVA
```

在运行上一节后运行测试将产生相同的性能结果。使用更少的代码生成相同的结果可以同时提高你应用程序的可读性和维护性。

## 统一内存

在 CUDA 6.0 中，引入了一种名为统一内存（Unified Memory）的新功能以简化 CUDA 编程模型中的内存管理。统一内存创建一个托管内存池，该池中的每个分配都可以用相同的内存地址（即指针）在 CPU 和 GPU 上访问。底层系统会自动在主机和设备之间的内存空间中迁移数据。这种数据移动对应用程序是透明的，大大简化了应用程序代码。

统一内存依赖于统一虚拟体系（UVA）的支持，两者是完全不同的技术。UVA 为系统中的所有处理器提供单一的虚拟内存地址。然而，UVA 不会自动将数据从一个物理位置迁移到另一个位置；这种能力是统一内存特有的。

统一内存提供了一种“单指针指向数据”模型，概念上与零拷贝内存相似。零拷贝内存分配在主机内存中，因此通过 PCIe 总线对零拷贝内存的高延迟访问会产生良好的性能。另一方面，统一内存解耦了内存和执行空间，使得数据可以根据需要透明地迁移到主机或设备，以提高局部性和性能。

托管内存指的是由底层系统自动管理的统一内存分配，并且可以与设备特定的分配（例如使用 `cudaMalloc` 过程创建的）互操作。你可以在内核中使用两种类型的内存：由系统控制的托管内存和必须由应用程序显式分配和传输的未托管内存。所有在设备内存上操作的 CUDA 操作对于托管内存也是有效的。主要区别是主机也可以引用和访问托管内存。

托管内存可以静态或动态分配。你可以通过添加修饰符将变量声明为托管变量。你可以通过以下方式动态分配托管内存：

```
__managed__ int a;
```

或者使用 `cudaMallocManaged` 函数：

```cpp
cuda_t cudaMallocManaged(void** ptr, size_t size);
```

使用后，可以使用 `cudaFree` 释放内存：

```cpp
cudaFree(ptr);
```

此外，你还可以提示系统将数据预取到主机或设备，以提高性能：

```cpp
cudaMemPrefetchAsync(ptr, size, device);
cudaMemPrefetchAsync(ptr, size, host);
```

在访问托管内存之前，可以调用 `cudaMemSynchronize()` 确保迁移已完成：

```cpp
cudaMemSynchronize();
```

## 内存访问模式

在 CUDA 中，内存访问模式对性能至关重要。由于内存访问是以块（cache line）为单位的，因此访问内存的方式会直接影响带宽。

### 合并访问（Coalesced Access）

当一个 Warp 中的多个线程同时访问连续的内存地址时，硬件会将这些请求合并为一个或少数几个事务。这就是合并访问。例如，如果一个 Warp 中的 32 个线程每个访问 4 字节的整数，且地址是连续的，硬件只需执行一个 128 字节（32 * 4）的事务。

### 非合并访问（Uncoalesced Access）

如果线程访问的地址跨越了多个内存块，硬件必须执行多次内存事务来满足这些请求。这会显著降低带宽。例如，如果线程访问的地址是随机的或跨度很大，合并就会失效。

### 跨步访问（Strided Access）

跨步访问是指线程之间以以固定的间距（步长）访问内存。虽然这仍然是有规律的，但如果步长较大，会导致合并效率的降低，从而影响性能。

## 优化建议

为了优化性能，应采取以下措施：

1. **重组数据布局**：使用结构体数组（SoA）而不是数组结构体（AoS），以确保线程访问的是连续内存。
2. **利用共享内存**：对于频繁访问的数据，将其加载到共享内存中，以减少对全局内存的压力。
3. **减少内存访问**：通过使用寄存器缓存变量来减少访问次数。

内存地址 128 160 192 224 256

![](img/506ba3a4c9f4512233692f3f20de1f3a_187_0.png)

线程 ID 0 31

图 4-8

## 全局内存读取

在 SM 中，数据通过三个缓存/缓冲区路径之一进行流水线传输，取决于所引用的设备内存类型：

- L1/L2 缓存
- 常量缓存 (Constant cache)
- 只读默认 (Read-only default)

L1/L2 缓存是默认路径。通过其他两条路径需要应用程序进行显式管理，但根据所使用的访问模式，可以带来性能提升。全局内存操作是否通过 L1 缓存取决于两个因素：

- 设备计算能力
- 编译器选项

在 Fermi GPU（计算能力 2.x）和 Kepler K40 或更新版本的 GPU（计算能力 3.5 及以上）上，可以通过编译器标志启用或禁用全局内存加载的 L1 缓存。默认情况下，Fermi 设备上的全局内存加载启用 L1 缓存，而 K40 及后续 GPU 则禁用。以下标志告诉编译器禁用 L1 缓存：

```
-Xptxas -dlcm-cg
```

在禁用了 L1 缓存 true后，所有到全局内存的加载请求将直接进入 L2 缓存；当发生 L1 缺失时，请求将由 DRAM 提供。每次内存事务可能由一个、两个或四个段执行，每个段为 32 字节。

也可以通过以下标志显式启用 L1 缓存：

```
-Xptxas -dlcm-ca
```
