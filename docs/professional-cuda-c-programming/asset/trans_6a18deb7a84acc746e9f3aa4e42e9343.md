
全局数组索引已相应调整，如下所示，因为你只需要一半的线程块来处理该数据集。注意，这意味着对于相同的数据集，设备暴露了束（warp）级和块（block）级的并行性。图 3-25 展示了每个线程的数据访问。

```cpp
unsigned int idx = blockIdx.x * blockDim.x * 2 + threadIdx.x;
int *idata = g_idata + blockIdx.x * blockDim.x * 2;
```

![](img/506ba3a4c9f4512233692f3f20de1f3a_143_0.png)

图 3-25
向新内核添加以下代码以维护所有总和。第 0 个线程在归约之前加了两个元素。

```cuda
cudaMemcpy(d_idata, h_idata, bytes, cudaMemcpyHostToDevice);
cudaDevicesSynchronize();
istart = seconds;
reduceUnroll2 << grid.x/2, block >>> (d_idata, d_data, size);
cudaDevicesSynchronize();
elapsed = seconds - istart;
cudaMemcpy(h_idata, d_data, grid.x/2*sizeof(int), cudaMemcpyDeviceToHost);
gpu_sum = 0;
for (int i = 0; i < grid.x/2; i++) gpu_sum += h_idata[i];
printf("Unroll2 elapsed %sec gpu_sum: %d <<%d block %d>>>\n", elapsed, gpu_sum, grid.x, block.x);
```

由于每个线程处理两个数据块，你现在需要通过减小网格大小来调整内核的执行配置：`reduceUnroll2 << grid.x/2, block >>> (d_idata, d_data, size);`。

现在编译并运行代码。结果如下：

```
gpuUnroll2 elapsed 0.00340 sec gpu_sum: 21934 <<16384 block 512
```

即使如此如此，内核现在的运行速度也比原始实现快了 3.2 倍。你还能进一步提升性能吗？`reduce.cu` 文件包含了两种展开内核的实现：

- reduceUnroll4：每个线程处理 4 个块
- reduceUnroll8：每个线程处理 8 个块

相应的结果总结如下：

```
gpuUnroll2 elapsed 0.00340 sec gpu_sum: 21934 <<16384 block 512
gpuUnroll4 elapsed 0.00182 sec gpu_sum: 21934 <<8192 block 512
gpuUnroll8 elapsed 0.00142 sec gpu_sum: 21934 <<4096 block 512
```

正如你所预想的，单个线程上更少的内存加载/存储操作会产生更好的性能延迟。你可以使用设备内存读取吞吐量确认这是性能提升的原因：`nvprof --metrics dram_read`。

| 实现方式 | 设备内存读取吞吐量 |
| :--- | :--- |
| Unrolling2 | 26.295 GB/s |
| Unrolling4 | 49.546 GB/s |
| Unrolling8 | 62.764 GB/s |

## 使用展开束进行归约

可以添加 `__syncthreads` 用于块内同步。在归约内核中，它被用于每一轮中，以确保在任何线程继续下一轮之前，所有线程都已将部分结果写入全局内存。然而，考虑当只剩下 32 个线程的情况（即单个束）。因为束的执行是 SIMT，因此在每条指令后都有隐式的束内同步。归约循环的最后几次迭代可以如下展开：

```cpp
if (tid < 32) {
    volatile int *vmem = idata;
    vmem[tid] += vmem[tid + 32];
    vmem[tid] += vmem[tid + 16];
    vmem[tid] += vmem[tid + 8];
    vmem[tid] += vmem[tid + 4];
    vmem[tid] += vmem[tid + 2];
    vmem[tid] += vmem[tid + 1];
}
```

这种束避免了循环控制和线程同步。注意变量 `vmem` 使用了 `volatile` 限定符声明，这告诉编译器必须在每次赋值时都将 `vmem[tid]` 写回全局内存。如果省略了 `volatile` 限定符，此代码将无法运行，因为编译器或缓存可能会优化掉对全局内存的写入。如果全局或共享内存中的变量声明为 `volatile`，编译器会假设其值可以被线程随时更改或使用。因此，对 `volatile` 变量的任何引用都会强制直接读取或写入内存，而不仅仅复制到缓存。

基于 `reduceUnroll`，可以将展开如下添加到归约内核中：

```cuda
__global void reduceUnroll8 (int *g_idata, int *g_odata, unsigned int n) {
    // 设置线程 ID
    unsigned int tid = threadIdx.x;
    unsigned int idx = blockIdx.x*blockDim.x + threadIdx.x;
    // 将全局数据指针转换为此块的本地指针
    int *idata = g_idata + blockIdx.x*blockDim.x*8;
    // 展开 8
    if (idx + 7*blockDim.x < n) {
        int a1 = g_idata[idx];
        int a2 = g_idata[idx+1*blockDim.x];
        int a3 = g_idata[idx+2*blockDim.x];
        int a4 = g_idata[idx+3*blockDim.x];
        int b1 = g_idata[idx+4*blockDim.x];
        int b2 = g_idata[idx+5*blockDim.x];
        int b3 = g_idata[idx+6*blockDim.x];
        int b4 = g_idata[idx+7*blockDim.x];
        g_odata[idx] = a1+a2+a3+a4+b1+b2+b3+b4;
    }
    __syncthreads();

    // 全局内存中的内归约
    for (int stride = blockDim.x / 2; stride > 32; stride >>= 1) {
      if (tid < stride)
        idata[tid] += idata[tid + stride];
    }

    // 块内同步
    __syncthreads();

    // 束展开
    if (tid < 32) {
      volatile int *vmem = idata;
      vmem[tid] += vmem[tid + 32];
      vmem[tid] += vmem[tid + 16];
      vmem[tid] += vmem[tid + 8];
      vmem[tid] += vmem[tid + 4];
      vmem[tid] += vmem[tid + 2];
      vmem[tid] += vmem[tid + 1];
    }
}
```

## 完全展开归约

如果你知道循环的迭代次数，可以将其完全展开。由于 Fermi 或 Kepler 上每个块的线程数限制为 1024，请参考下代码：

```cuda
__global void reduceCompleteWarp(int *g_idata, int *g_odata, unsigned int n) {
    // 设置线程
    unsigned int tid = threadIdx.x;
    unsigned int idx = blockIdx.x*blockDim.x + threadIdx.x;
    // 将全局数据指针转换为此块的本地指针
    int *idata = g_idata + blockIdx.x*blockDim.x*8;
    // 展开 8
    if (idx + 7*blockDim.x < n) {
        int a1 = g_idata[idx];
        int a2 = g_idata[idx+1*blockDim.x];
        int a3 = g_idata[idx+2*blockDim.x];
        int a4 = g_idata[idx+3*blockDim.x];
        int b1 = g_idata[idx+4*blockDim.x];
        int b2 = g_idata[idx+5*blockDim.x];
        int b3 = g_idata[idx+6*blockDim.x];
        int b4 = g_idata[idx+7*blockDim.x];
        g_odata[idx] = a1+a2+a3+a4+b1+b2+b3+b4;
    }
    __syncthreads();

    // 完全展开内归约
    for (int stride = blockDim.x / 2; stride > 32; stride >>= 1) {
      if (tid < stride)
        idata[tid] += idata[tid + stride];
    }

    // 块内同步
    __syncthreads();

    // 束展开
    if (tid < 32) {
      volatile int *vmem = idata;
      vmem[tid] += vmem[tid + 32];
      vmem[tid] += vmem[tid + 16];
      vmem[tid] += vmem[tid + 8];
      vmem[tid] += vmem[tid + 4];
      vmem[tid] += vmem[tid + 2];
      vmem[tid] += vmem[tid + 1];
    }
}
```
