

1 dram_read_throughput 94.112GB/s
1 dram_write_throughput 94.110GB/s
1 Kernel: transposeSmemPad(float*, float*, int, int)
1 dram_read_throughput 62.078GB/s
1 dram_write_throughput 62.071GB/s
1 Kernel: transposeSmem(float*, float*, int, int)
1 dram_read_throughput 59.646GB/s
1 dram_write_throughput 59.636GB/s
1 Kernel: naiveGmem(float*, float*, int, int)
1 dram_read_throughput 34.791GB/s
1 dram_write_throughput 44.497GB/s
1 Kernel: copyGmem(float*, float*, int, int)
1 dram_read_throughput 94.019GB/s
1 dram_write_throughput 94.018GB/s

# 暴露更多并行性

一种简单且有效的优化技术是调整块维度以发现最佳的执行配置。表 5-6 总结了在 Tesla K40 上不同线程块的结果。块大小 16x16 表现出最佳性能，因为它通过更多的并发线程块暴露了最大的设备并行性。

表 5-6：使用不同线程块配置的转置内核的性能

| 内核 (KERNELS) | 块大小 (32x32) | 块大小 (32x16) | 块大小 (16x16) |
|---|---|---|---|---|---|---|
| | 耗时 (MS) | 带宽 (GB/S) | 耗时 (MS) | 带宽 (GB/S) | 耗时 (MS) | 带宽 (GB/S) |
| SmemUnrollPad | 0.779 | 172.21 | 0.732 | 183.34 | 0.722 | 185.66 |
| SmemUnrollPadDyn | 0.782 | 171.55 | 0.732 | 183.33 | 0.722 | 185.99 |

表 5-7 总结了 Tesla K40 的 nprof 结果，涵盖全局吞吐量和共享内存 bank 冲突。32x16 的 transposeSmemUnrollPad 配置最小化了 bank 冲突，而 16x16 的线程块配置使全局内存吞吐量最大。从这里可以得出结论：该内核受限于全局内存吞吐量而非共享内存吞吐量。

表 5-7：使用不同块大小的转置内核的性能

| 指标 (METRICS) | 块大小 (32x32) | 块大小 (32x16) | 块大小 (16x16) |
|---|---|---|---|
| gst_throughput | 87.724 GB/s | 94.118 GB/s | 95.010 GB/s |
| gld_throughput | 87.724 GB/s | 94.118 GB/s | 95.010 GB/s |
| shared_load_transactions_per_request | 2.000 | 1.000 | 1.000 |
| shared_store_transactions_per_request | 1.046 | 1.000 | 1.625 |

# 常量内存 (CONSTANT MEMORY)

常量内存是一种特殊用途内存，用于只读且被 warp 中的线程一致访问的数据。虽然常量内存在内核代码中是只读的，但从主机（host）端来看是可读可写的。

常量内存存储在设备 DRAM（如全局内存）中，并有一个专用的片上缓存。类似于 L1 缓存和共享内存，从每个 SM 的常量缓存读取的延迟比从常量内存读取低得多。每个 SM 的常量内存缓存大小限制为 64 KB。

常量内存的最佳访问模式与本书为止研究的任何其他类型的内存都不同。如果一个 warp 中的所有线程访问常量内存中的相同位置，效果是最好的。warp 内部线程对不同地址的访问会被串化，常量内存读取的成本会随 warp 内线程读取的唯一地址数量呈线性增长。

常量变量必须在全局作用域中声明并带有以下限定符：

```
__const__
```

常量内存变量的生命周期贯穿整个应用程序，并且可以通过网格内的所有线程以及主机通过运行时函数访问。使用 CUDA 独立编译功能，常量内存变量可以在多个源文件中可见（独立编译的更多细节请见第 10 章）。由于设备只能读取常量内存，必须使用以下运行时函数从主机代码初始化值：

```
cudaError_t cudaMemcpyToSymbol(const void *symbol, const void *src,
    size_t count, size_t offset, cudaMemcpyKind kind)
```

cudaMemcpyToSymbol 函数将 `src` 指向的数据拷贝到设备上 `symbol` 指定的常量位置。枚举变量 `kind` 指定传输方向。默认情况下，`kind` 为 `cudaMemcpyHostToDevice`。

# 使用常量内存实现模板计算

在数值分析领域，模板（stencil）计算对一组数据点应用函数，并更新单个点的值。模板是求解许多偏微分方程算法的基础。在一维中，围绕位置 $x$ 的九点模板会将某些函数应用到以下位置的值：

[x - 4h, x - 3h, x - 2h, x - h, x, x + 2h, x + 3h, x + 4h]

九点模板如图 5-18 所示。

![](img/506ba3a4c9f4512233692f3f20de1f3a_277_0.png)

图 5-18

九点模板的一个示例是实变量函数 $f$ 在点 $x$ 处的八阶导数中心公式。虽然理解该公式的应用很重要，但只需识别它接收上述九点作为输入并产生单个输出。该公式将在节中作为示例模板使用。

```
f'(x) = c_4(f(x+4h) - f(x-4h)) + c_3(f(x+3h) - f(x-3h))
```
