
零拷贝内存（Zero-copy memory）是映射到设备地址空间的锁页（不可分页）内存。
你可以使用以下函数创建一个映射的、锁定的 `cudaHost` 内存区域：

```
cudaError_t cudaAlloc(void **pHost, size_t count, unsigned int flags);
```

该函数分配 `count` 字节的页锁（page-locked）且可设备访问的主机内存。
由此函数分配的内存必须使用 `cudaFreeHost` 释放。`flags` 参数允许对分配内存的特殊属性进行进一步配置：

- cudaHostAllocDefault
- cudaHostAllocPortable
- cudaHostAllocMapped

cudaHostAllocDefault 使 `cudaHostAlloc` 的行为与 `cudaMallocHost` 相同。
设置 `cudaHostAllocPortable` 返回的锁页内存可以被所有 CUDA 上文使用，而不仅仅是执行分配的那个。`cudaHostAllocWriteCombined` 返回组合写入内存，在某些系统配置下，它可以通过 PCI Express 总线传输得更快，但大多数主机无法高效地读取它。因此，对于由主机写入、设备读取的缓冲区（通过映射锁页内存或主机到设备传输实现），组合写入内存是一个很好的选择。与零拷贝内存最相关的标志是 `cudaHostAllocMapped`，它返回映射到设备地址空间中的内存。

你可以使用以下函数获取设备指针内存：

```
cudaError_t cudaGetDevicePointer(void **Device, void *pHost, unsigned int flags);
```

该函数返回一个指向设备内存的指针，设备可以通过该指针访问映射的锁页内存。`Flag` 参数保留留以后备使用。如果不设置，则必须设置为零。

将零拷贝内存作为设备内存的补充并进行频繁的读写操作会显著降低性能。因为每次映射内存的内存事务都必须经过 PCIe 总线，与全局内存相比，增加了大量的延迟。你可以使用第 2 章中使用的 `sumArrays` 内核来验证零拷贝内存的性能：

```
__global void sumArraysZeroCopy(float *A, float *B, float *C, const int n) {
  int i = blockIdx.x * blockDim.x + threadIdx.x;
  if (i < n) C[i] = A[i] + B[i];
}
```

为了测试零拷贝读操作的性能，我们将 `A` 和 `B` 分配为零拷贝内存，并将 `C` 分配在设备内存中。主函数在列表 4-3 中。你可以从 Wrox.com 下载 `sumArrayZeroCopy.cu` 的源代码。

主函数包含两个部分：在第一部分，从设备内存加载数据并存储其中；在第二部分，从零拷贝内存加载数据并存储到设备内存。在开始，你还需要检查设备是否支持映射锁页内存。

为了允许内核从零拷贝内存读取，你需要将数组 `A` 和 `B` 分配为映射锁页内存。然后你可以直接在设备上初始化数组 `A` 和 `B`，而无需将它们传输到设备内存。接下来，获取映射锁页内存的设备指针供内核使用。内存分配并初始化后，调用内核。

# 列表 4-3：使用零拷贝内存求和 (sumArrayZerocopy.cu)
（列出的 main 函数）

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

