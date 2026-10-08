

```cpp
global void readOffset(float *A, float *B, float *C, const int n,
    int offset) {
    unsigned int i = blockIdx.x * blockDim.x + threadIdx.x;
    unsigned int k = i + offset;
    if (k < n) C[i] = A[k] + B[k];
}
```

为了验证转换后的内核代码的正确性，也应对相应进行修改：

```cpp
void sumArrayOnHost(float *A, float *B, float *C, const int n,
    int offset) {
    for (int idx = offset, k = 0; idx < n; idx++, k++) {
        C[k] = A[idx] + B[idx];
    }
}
```

主函数如列表 4-4所示。你应该熟悉这段代码的大部分内容。你可以从网站下载 `readSegment.cu` 的完整代码。offset 的默认值为零，但可以通过命令行参数覆盖。

# 列表 4-4: 使用带偏移量的内存读取 (readSegment.cu) (列出的唯一 main 函数)

```cpp
int main(int argc, char **argv) {
    // 设置设备
    int dev = 0;
    cudaDeviceProp devProp;
    cudaDeviceGetProperties(&devProp, dev);
    printf("%s starting at %d\n", argv[0]);
    printf("device: %s\n", devProp.name);
    cudaSetDevice(dev);

    // 设置数组大小
    int nElem = 1<<20; // 归约元素总数
    printf("array size: %d\n", nElem);
    size_t nBytes = nElem * sizeof(float);

    // 设置汇总的偏移量
    int blockSize = 512;
    int offset = 0;
    if (argc > 1) offset = atoi(argv[1]);
    if (argc > 2) blockSize = atoi(argv[2]);

    // 执行配置
    dim3 block (blockSize,1);
    dim3 grid ((nElem+block.x-1)/block.x,1);

    // 分配主机内存
    float *h_A = (float*)malloc(nBytes);
    float *h_B = (float*)malloc(nBytes);
    float *hostRef = (float*)malloc(nBytes);
    float *gpuRef = (float*)malloc(nBytes);

    // 初始化主机数组
    initialData(h_A, nElem);
    memmove(h_B,h_A,nBytes);

    // 主机端汇总
    sumArraysOnHost(h_A, h_B, nElem, offset);

    // 分配设备内存
    float *d_A,*d_B,*d_C;
    cudaMalloc((float**)&d_A, nBytes);
    cudaMalloc((float**)&d_B, nBytes);
    cudaMalloc((float**)&d_C, nBytes);

    // 将数据从主机拷贝到设备
    cudaMempy(d_A, h_A, nBytes, cudaMemcpyHostToDevice);
    cudaMempy(d_B, h_B, nBytes, cudaMemcpyHostToDevice);

    // 内核 1:
    double iStart = seconds();
    warmup <<< grid.x, grid.y >>> (d_A, d_B, d_C, nElem, offset);
    cudaDeviceSynchronize();
    elIaps = seconds() - iStart;
    printf("warmup <<< %d, %d >>> offset %d elapsed %f sec\n", grid.x, block.x, offset, iElaps);

    iStart = seconds();
    readoff <<< grid.x, block.y >>> (d_A, d_B, d_C, nElem, offset);
    cudaDeviceSynchronize();
    elIaps = seconds() - iStart;
    printf("readoff <<< %d, %d >>> offset %d elapsed %f sec\n", grid.x, block.x, offset, iElaps);

    // 将结果拷贝回主机端并检查设备结果
    cudaMempy(gpuRef,d_C, nBytes, cudaMemcpyDeviceToHost);
    checkResult(hostRef, gpuRef, nElem-offset);

    // 将结果拷贝回主机端并检查设备结果
    cudaMempy(gpuRef,d_B, nBytes, cudaMemcpyDeviceToHost);
    checkResult(hostRef, gpuRef, nElem-offset);

    // 将内核结果拷贝回主机端并检查设备结果
    cudaMempy(gpuRef,d_C, nBytes, cudaMemcpyDeviceToHost);
    checkResult(hostRef, gpuRef, nElem-offset);

    // 释放主机和设备内存
    cudaFree(d_A);
    cudaFree(d_B);
    cudaFree(d_C);
    free(h_A);
    free(h_B);

    // 重置设备
    cudaDeviceReset();
    return EXIT_SUCCESS;
}
```

使用以下命令编译代码：

```bash
$ nvcc -03 -arch=sm_20 readSegment.cu -o readSegment
```

你可以尝试不同的偏移量。下面是来自 Fermi M2050 的示例输出：

```
$ ./readSegment 0
readOffset << 32768, 512 >>> offset 0 0.001820 sec
$ ./readSegment 11
readOffset << 32768, 512 >>> offset 11 0.001949 sec
$ ./readSegment 128
readOffset << 32768, 512 >>> offset 128 0.001820 sec
```

使用 `offset=11` 会导致数组 A 和 B 的内存加载未对齐。这种情况的运行时间也较慢。你可以通过收集全局加载效率的信息来验证这些未对齐访问是性能损失的原因：

```
gld_efficiency = Requested Global Memory Load Throughput /
RequiredGlobal Memory Load Throughput
```

Required Global Memory Load Throughput 包含了需要多次内存事务的重放加载指令（replay load instructions），而 Requested Global Memory Load Throughput 不包含。

你可以使用 `nvprof` 配合 `readSegment` 测试收集 `gld_efficiency` 指标：

```
$ nvprof ./readSegment 0
$ nvprof ./readSegment 11
$ nvprof ./readSegment 128
```

（注：原文中存在大量重复的段落，译文已根据要求保留逻辑并去重复）

全局加载效率的示例结果：

| Offset | Global Load Efficiency |
| :--- | :--- |
| 0 | 100.00% |
| 11 | 49.81% |
| 128 | 100.00% |

