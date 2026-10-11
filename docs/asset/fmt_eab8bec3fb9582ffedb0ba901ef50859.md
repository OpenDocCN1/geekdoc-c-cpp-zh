
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
__global__ void reduceUnroll8 (int *g_idata, int *g_odata, unsigned int n) {
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
__global__ void reduceCompleteWarp(int *g_idata, int *g_odata, unsigned int n) {
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

// 将此块的结果写入全局内存

if (tid == 0) g_data[blockIdx.x] = idata[0];

}

使用以下执行配置启动此内核函数：

`reduceCompleteUnrollWarp8<<<grid.x / 8, block>>>(d_idata, d_data, size);`

内核执行时间获得了一些微幅提升，执行速度比 `reduceUnrollWarp8` 快 1.06 倍，比原始实现快 9.16 倍。

```
gpuCmptUnrollW8 elapsed 0.001280 sec gpu_sum: 219393471 <<<grid 4096 block 512>>>
```

## 使用模板函数进行归约

虽然可以手动展开循环，但使用模板函数可以减少分支开销。CUDA 支持在设备函数上使用模板参数。你可以将块大小作为模板函数的参数，如下所示：

```cpp
template <unsigned int blockSize>
void reduceCompleteUnroll(int *g_idata, int *g_data, unsigned int n) {
 // 设置线程 ID
 unsigned int tid = threadIdx.x;
 unsigned int idx = blockIdx.x * blockDim.x * 8 + threadIdx.x;
 // 将全局数据转换为此块的本地指针
 int *idata = g_data + blockIdx.x * blockDim.x * 8;

 // 展开 8 次
 if (idx + 7*blockIdx.x < n) {
  int a1 = g_idata[idx];
  int a2 = g_idata[idx + blockIdx.x];
  int a3 = g_idata[idx + 2 * blockIdx.x];
  int a4 = g_idata[idx + 3 * blockIdx.x];
  int b1 = g_idata[idx + 4 * blockIdx.x];
  int b2 = g_idata[idx + 5 * blockIdx.x];
  int b3 = g_idata[idx + 6 * blockIdx.x];
  int b4 = g_idata[idx + 7 * blockIdx.x];
  g_idata[idx] = a1+a2+a3+a4+b1+b2+b3+b4;
 }

 syncthreads();
```

```cpp
// 原地归约并完全展开
if (blockSize <= 1024 && tid < 512) idata[tid] += idata[tid + 512];
 syncthreads();
```

```cpp
if (blockSize <= 512 && tid < 256) idata[tid] += idata[tid + 256];
 syncthreads();
```

```cpp
if (blockSize>=256 && tid < 128) idata[tid] += idata[tid + 128];
syncthreads();
```

```cpp
if (blockSize==128 && tid < 64) idata[tid] += idata[tid + 64];
syncthreads();
// Warp 展开
if (tid < 32) {
volatile int *vsmem = idata;
vsmem[tid] += vsmem[tid + 32];
vsmem[tid] += vsmem[tid + 16];
vsmem[tid] += vsmem[tid + 8];
vsmem[tid] += vsmem[tid + 4];
vsmem[tid] += vsmem[tid + 2];
vsmem[tid] += vsmem[tid + 1];
}
```

```cpp
// 将结果写入全局内存
if (tid == 0) g_odata[blockIdx.x] = idata[0];
```

与 `reduceUnrollWarp8` 的的区别是用模板参数替换了块大小。检查块大小的语句将在编译时评估，如果条件不成立会被移除，从而产生非常高效的循环。例如，如果调用内核的线程块大小为 256，则

```
blockSize>=1024 && tid < 512
```

将始终为假。编译器会自动从执行的内核中将其移除。所示的 `switch-case` 允许编译器为特定的块大小优化代码，但这意味着仅适用于某些块大小的 `reduceCompleteUnroll`。

```cpp
switch (blockSize) {
case 1024:
reduceCompleteUnroll<1024><><grid.x/8, block>>>(d_idata, d_odata, size);
break;
case 512:
reduceCompleteUnroll<512><><grid.x/8, block>>>(d_idata, d_odata, size);
break;
case 256:
reduceCompleteUnroll<256><><grid.x/8, block>>>(d_idata, d_odata, size);
break;
case 128:
reduceCompleteUnroll<128><><grid.x/8, block>>>(d_idata, d_odata, size);
break;
case 64:
reduceCompleteUnroll<64><><grid.x/8, block>>>(d_idata, d_odata, size);
break;
}
```

### 表 3-5：归约内核性能

| 内核 | 时间 (S) | 步进加速 | 累积加速 |
|---|---|---|---|
| 邻域（分支） | 0.011722 | | |
| 邻域（无分支） | 0.009321 | 1.26 | 1.26 |
| 交叉交叉 | 0.006967 | 1.34 | 1.68 |
| 展开 8 个块 | 0.001422 | 4.90 | 8.24 |
| 展开 8 个块 + 最后一个 Warp | 0.001355 | 1.05 | 8.65 |
| 展开 8 个块 + 循环 + 最后一个 Warp | 0.001280 | 1.06 | 9.16 |
| 模板内核 | 0.001253 | 1.02 | 9.35 |

与 `reduceUnrollWarp8` 的区别是用模板参数替换了块大小。检查块大小的语句将在编译时评估，如果条件不成立会被移除，从而产生非常高效的循环。例如，如果调用内核的线程块大小为 256，则

```
blockSize>=1024 && tid < 512
```

将始终为假。编译器会自动从执行的内核中将其移除。所示的 `switch-case` 结构允许编译器为特定的块大小优化代码，但这意味着仅适用于某些块大小的 `reduceCompleteUnroll`。

```cpp
switch (blockSize) {
case 1024:
reduceCompleteUnroll<1024><><grid.x/8, block>>>(d_idata, d_odata, size);
break;
case 512:
reduceCompleteUnroll<512><><grid.x/8, block>>>(d_idata, d_odata, size);
break;
case 256:
reduceCompleteUnroll<256><><grid.x/8, block>>>(d_idata, d_odata, size);
break;
case 128:
reduceCompleteUnroll<128><><grid.x/8, block>>>(d_idata, d_odata, size);
break;
case 64:
reduceCompleteUnroll<64><><grid.x/8, block>>>(d_idata, d_odata, size);
break;
}
```

表 3-5 汇总了本文涵盖的所有并行归约实现。

### 表 3-5：归约内核性能

| 内核 | 时间 (S) | 步进加速 | 累积加速 |
|---|---|---|---|
| 邻域（分支） | 0.011722 | | |
| 邻域（无分支） | 0.009321 | 1.26 | 1.26 |
| 交叉交叉 | 0.006967 | 1.34 | 1.68 |
| 展开 8 个块 | 0.001422 | 4.90 | 8.24 |
| 展开 8 个块 + 最后一个 Warp | 0.001355 | 1.05 | 8.65 |
| 展开 8 个块 + 循环 + 最后一个 Warp | 0.001280 | 1.06 | 9.16 |
| 模板内核 | 0.001253 | 1.02 | 9.35 |

子父网格之间的一致性保证。当子网格的内存与父线程完全一致时，子网格的执行有两个点：子网格开始时以及子网格完成时。父线程在调用子网格之前的所有全局内存操作都保证对子网格可见。子网格的所有内存操作在子网格完成并对其进行同步后，保证对父线程可见。

![](img/506ba3a4c9f4512233692f3f20de1f3a_151_0.png)

图 3-26

共享内存和本地内存分别是线程块或线程私有的，且在父子节点之间不可见也不具有一致性。本地内存是线程的私有存储，在线程外部不可见。在启动子网格时，将本地内存指针作为参数传递是无效的。

# GPU 上的嵌套 Hello World
