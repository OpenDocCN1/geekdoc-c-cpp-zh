

# 列表 4-6（续）

```cpp
// 设置内核 
switch (iKernel) {
    case 0:
        kernel = &copyRow;
        kernelName = "CopyRow";
        break;

    case 1:
        kernel = &copyCol;
        kernelName = "CopyCol";
        break;
}

// 运行内核
iStart = seconds();
kernel << grid, block >>>(d_C, d_A, nx, ny);
cudaDeviceSynchronize();
iElaps = seconds() - iStart;

// 计算有效带宽
float iband = 2*nx*ny*sizeof(float)/1e9/iElaps;
printf("effective bandwidth %f GB/n grid (%d,%d) block (%d,%d) %f\n", kernelName, iElaps, grid.x, grid.y, block.x, block.y, iband);

// 检查内核结果
if (iKernel1) {
    cudaMemcpy(gpuRef, d_C, nBytes, cudaMemcpyDeviceToHost());
    checkResult(hostRef, gpuRef, nx*ny, 1);
}

// 释放主机和设备内存
cudaFree(d_A);
cudaFree(d_C);
free (h_A);
free (hostRef);
free (gpuRef);

// 重置设备
cudaDeviceReset();
return EXIT_SUCCESS;
```

在启用 L1 加载缓存时编译代码：

```bash
$ nvcc -arch=sm_20 -Xptxas -dlcram=ca transpose.cu -o transpose
```

运行以下命令以检查两个拷贝内核的性能：

```bash
$ ./transpose 0
$ ./transpose 1
```

在禁用 ECC 的 Fermi M2090 上，两个拷贝内核的性能如表 4-4 所示。测量提供了一个上界（约为理论峰值带宽的 70%）和一个下界（约为理论峰值带宽的 33%）。

# 表 4-4：内核的有效带宽（启用 L1 缓存）

| 内核 | 带宽 | 与峰值带宽的比例 |
| --- | --- | --- |
| 理论峰值带宽 | 177.6 GB/s | 上界: 70.76% |
| CopyRow: 按行加载/存储 | 125.67 GB/s | |
| CopyCol: 按列加载/存储 | 58.7 GB/s | 下界: 33.09% |

块大小：16 x 16；矩阵大小：2,048 x 2,048；有效带宽单位：GB/sec

# 朴素响应：按行读取与按列读取

基于实现，朴素的行内核内核实现非常简单。这个版本的 transpose naiveRow 按行和列进行转置：

```cpp
global void transposeRow(float *out, float *in, const int nx,
    const int ny) {
    unsigned int ix = blockDim.x * blockIdx.x + threadIdx.x;
    unsigned int iy = blockDim.y * blockIdx.y + threadIdx.y;

    if (ix < nx && iy < ny) {
        out[ix * ny + iy] = in[iy * nx + ix];
    }
}
```

通过交换读和写索引，我们产生了朴素的列内核转置内核。这个版本按行加载列并按行存储：

```cpp
global void transposeCol(float *out, float *in, const int nx,
    const int ny) {
    unsigned int ix = blockDim.x * blockIdx.x + threadIdx.x;
    unsigned int iy = blockDim.y * blockIdx.y + threadIdx.y;

    if (ix < nx && iy < ny) {
        out[ix * ny + iy] = in[iy * nx + ix];
    }
}
```

为这些内核向内核 switch 语句添加了以下情况：

```cpp
case 2:
    kernel = &transposeNaiveRow;
    kernelName = "NaiveRow";
    break;
```

```cpp
case 3:
    kernel = &transposeNaiveCol;
    kernelName = "NaiveCol";
    break;
```

在启用 L1 缓存的情况下重新编译代码并运行以下命令来测量这两个内核的性能。结果总结在表 4-5 中。

```bash
$ ./transpose 2
$ ./transpose 3
```

# 表 4-5：内核的有效带宽（启用 L1 缓存）

| 内核 | 带宽 | 与峰值带宽的比例 |
|---|---|---||
| NaiveRow : 加载行/存储列 | 64.16 GB/s | 36.13% |
| NaiveCol : 加载列/存储行 | 81.64 GB/s | 45.97% |

NaiveCol 方法的性能优于 NaiveRow 方法。如之前解释过的，这种性能差异的一个可能原因是，某些访问到 L1 缓存的步长读取完全没有被使用，但它们仍然留在缓存中，并可能导致未来的访问产生缓存命中。为了验证这一点，请尝试在禁用 L1 缓存的情况下重新编译（-xpt -dlcm=cg）。

运行以下命令以获取未启用 L1 缓存加载的所有内核的性能。表 4-6 中的结果清楚地表明，禁用缓存加载对步长访问模式有巨大影响。

```bash
$ ./transpose 0
$ ./transpose 1
$ ./transpose 2
$ ./transpose 3
```

# 表 4-6：内核的有效带宽（禁用 L1 缓存）

| 内核 | 带宽 | 备注 |
|---|---|---|
| CopyRow : 按行加载/存储 | 128.07 GB/s | 上界 |
| CopyCol : 按列加载/存储 | 40.42 GB/s | 下界 |
| NaiveRow : 加载行/存储列 | 63.79 GB/s | 步长写入/合并读取 |
| NaiveCol : 加载列/存储行 | 47.13 GB/s | 步长读取/合并写入 |

块大小：16 x 16；矩阵大小：2,048 x 2,048；有效带宽单位：GB/sec

你还可以使用下面的命令通过 `nvprof` 直接检查缓存加载。结果总结在表 4-7 中。

```bash
$ nvprof --devices 0 --metrics throughput,throughput ./transpose 16 16 2048
```

# 表 4-7：内核的吞吐量（启用 L1 缓存）

| 内核 | 吞吐量 |
|---|---|
| CopyRow : 按行加载/存储 | 131.46 GB/s | 65.32 GB/s |
| CopyCol : 按列加载/存储 | 47.67 GB/s | 118.52 GB/s |
| NaiveRow : 加载行/存储列 | 129.05 GB/s | 64.31 GB/s |
| NaiveCol : 加载列/存储行 | 64.33 GB/s | 40.02 GB/s |

块大小：16 x 16；矩阵大小：2,048 x 2,048 结果显示，在启用 L1 缓存的情况下，步长读取获得了最高的吞吐量。接下来你可以检查

# 表 4-8：内核的效率（启用 L1 缓存）

| 内核 | 效率 |
|---|---|
| CopyRow : 按行加载/存储 | 49.8% |
| CopyCol : 按列加载/存储 | 25% |
| NaiveRow : 加载行/存储列 | 50.0% |
| NaiveCol : 加载列/存储行 | 100% |

# 展开转置

接下来，你将使用展开（unrolling）技术来提高转置带宽。此示例中展开的目标是为线程分配更多工作以增加内存请求。以下是展开因子为行的实现。引入了两个新索引：一个用于行，另一个用于列。

```cpp
global void transposeUnrollRow(float *out, float *in, const int nx,
    const int ny) {
    unsigned int ix = blockDim.x * blockIdx.x + threadIdx.x;
    unsigned int iy = blockDim.y * blockIdx.y + threadIdx.y;

    unsigned int ti = iy*nx + ix; 行访问
    unsigned int to = ix*ny; // 列访问

    if (ix+3*blockDim.x < nx && iy < ny) {
        out[to] = in[ti];
        out[to] + ny*blockDim.x] = in[ti+blockDim.x];
        out[to] + ny*2*blockDim.x] = in[ti+2*blockDim.x];
        out[to] + ny*3*blockDim.x] = in[ti+3*blockDim.x];
    }
}
```

交换行和宽度索引会产生类似的展开列式实现：

```cpp
global void transposeUnrollCol(float *out, float *in, const int nx,
    const int ny) {
    unsigned int ix = blockDim.x * blockIdx.x + threadIdx.x;
    unsigned int iy = blockDim.y * blockIdx.y + threadIdx.y;

    unsigned int ti = iy*nx + ix; // 行访问
    unsigned int to = ix*ny + iy; // 列访问

    if (ix+3*blockDim.x < nx && iy < ny) {
        out[ti] = in[blockDim.x*ny];
        out[ti] + 2*blockDim.x*ny] = in[ti+2*blockDim.x*ny];
        out[ti] + 3*blockDim.x*ny] = in[ti+3*blockDim.x*ny];
    }
}
```

在内核 switch 语句中添加以下代码时，在添加展开之前必须调整 switch 的网格大小。

```cpp
case 4:
    kernel = &transposeUnrollRow;
    kernelName = "Unroll4Row";
    grid.x = (nx+block.x*4-1)/(block.x*4);
    break;

case 5:
    kernel = &transposeUnrollCol;
    kernelName = "Unroll4Col";
    grid.x = (nx+block.x*4-1)/(block.x*4);
    break;
```

