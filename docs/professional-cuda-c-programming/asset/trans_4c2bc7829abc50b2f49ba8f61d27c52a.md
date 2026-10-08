

// 将此块的结果写入全局内存
if (tid == 0) g_data[blockIdx.x] = idata[0];
}

使用以下执行配置启动此内核函数：
reduceCompleteUnrollWarp8<<<grid.x / 8, block>>>(d_idata, d_data, size);

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

表 3-5 汇总了本文涵盖的所有并行归约实现的结果。

## 表 3-5：归约内核性能

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

## 表 3-5：归约内核性能

| 内核 | 时间 (S) | 步进加速 | 累积加速 |
|---|---|---|---|
| 邻域（分支） | 0.011722 | | |
| 邻域（无分支） | 0.009321 | 1.26 | 1.26 |
| 交叉交叉 | 0.006967 | 1.34 | 1.68 |
| 展开 8 个块 | 0.001422 | 4.90 | 8.24 |
| 展开 8 个块 + 最后一个 Warp | 0.001355 | 1.05 | 8.65 |
| 展开 8 个块 + 循环 + 最后一个 Warp | 0.001280 | 1.06 | 9.16 |
| 模板内核 | 0.001253 | 1.02 | 9.35 |

