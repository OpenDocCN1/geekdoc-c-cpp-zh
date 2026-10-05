

## 7.2. 卸载 (Offload)

```
hostmic_scale(v+shft, len);
sum[mc] = hostmic_sum(v+shft, len);
}
```

```c
printf(" nmic = %d\n", nmic);
/*
 * 等待 mic 返回
*/
for(int mc=0; mc < nmic; mc++) {
#pragma offload_wait target(mic:mc) wait(1)
}
```

```c
/*
 * 释放 mic 设备上的内存
*/
for(int mc=0; mc < nmic; mc++) {
long shft = mc*n/nmic;
long len = (mc+1)*n/nmic - mc*n/nmic;
#pragma offload_transfer target(mic:mc) [shft:len]:
nocopy(v[shft]:align(G4)) alloc_if(0) free_if(1)
}
double ans = 0;
for(int mc=0; mc < nmic; mc++) {
    ans += sum[mc];
}
printf(" leibniz4: sum = %e\n", ans);
```

```c
_mm_free(v);
mic_exit();
```

注意 `hostmic_scale()` 和 `hostmic_sum()` 的第一个参数是 `v+shft` 而不仅仅是 `v`。执行缩放和求和的卸载区域之前有一个信号子（signal clause）。如果涉及多个 MIC 设备，使用阻塞式卸载（blocking offloads）是没有意义的。

### 7.2.4 卸载带宽

如果 Phi/MIC 设备以卸载模式使用，宿主机与 MIC 设备之间的数据传输将产生巨大的代价。连接宿主机与 MIC 设备（通过芯片组；见图 7.1）的 PCIe 总线带宽较低。其带宽比 MIC 设备甚至宿主机内存的带宽低了一个数量级。宿主机与 Xeon Phi 协处理器之间的数据传输对协处理器模型的优势和实用性造成了严重限制。

为了测量宿主机与 MIC 设备之间传输的时间，我们使用如下函数：

```c
void xfer_in(double *v, long n, int nmic){
long fst[nmic+1];
for(int i=0; i <= nmic; i++)
fst[i] = i*n/nmic;

for(int mc=0; mc < nmic; mc++){
 long shift = fst[mc];
 long len = fst[mc+1] - fst[mc];
#pragma offload target(mic:mc)
in(v[shift:len]:align(64) alloc_if(0) free_if(0)) signal(1)
dummy(v+shift, len);
}

for(int mc=0; mc < nmic; mc++)
#pragma offload_wait target(mic:mc) wait(1)
}
```

该函数将数据传输到 nmic 个设备。类似的函数可以将数据从 MIC 设备传输出，或者使用内置子句（inbuilt clause）在进入卸载区域时将数据传输到 MIC 设备，并在退出时传出。

| 周期/字节 (单个 MIC) | 带宽 (单个 MIC) | 周期/字节 (两个 MIC) | 带宽 (两个 MIC) |
|---|---|---|---|
| IN | 0.42 | 6.48 GB/s | 0.40 | 6.75 GB/s |
| OUT | 0.42 | 6.48 GB/s | 0.40 | 6.75 GB/s |
| INOUT | 0.81 | 3.24 GB/s | 0.77 | 3.51 GB/s |

表 7.3：向单个 MIC 设备或同时向两个 MIC 设备传输数据时的卸载带宽。以周期/字节为单位，周期为 2.7 GHz AVX 宿主机的。

表 7.3 显示，数据可以以后近 7 GB/s 的速率移入或移单个 MIC 设备。该速率接近 PCIe 总线的峰值额。如果数据在进入卸载区域时输入 MIC 设备，并在退出时从 MIC 设备输出，带宽将几乎减半。使用 inout 子句时，流入和流出无法重叠。

在同时向两个 MIC 设备传输时，带宽几乎保持不变。带宽无法翻倍，因为两个设备都在同一条总线上。数据传输的延迟处于毫秒级。

**练习 7.2.1.** 编写一个程序来计算长数组的和，并将部分工作外包给系统中的每个 Phi 设备。你预计该程序会产生任何加速效果吗？

**练习 7.2.2.** 编写一个程序，在单次迭代中将二维数组（具有周期性边界）的每个条目替换为北、南、东、西条目的平均值。该程序必须将部分计算外包给系统中的每个 Phi 设备。如果只执行几次迭代，你预计会有加速吗？如果迭代次数很大又如何？

**练习 7.2.3.** 假设一个矩阵（维度可以假设足够大）分布在宿主机和 Phi 协处理器之间。编写一个转置该矩阵的程序。讨论由于处理器与协处理器之间的异构性带来的困难。

## 7.3 两个示例：FFT 和矩阵乘法

### 7.3.1 FFT

第 7.3.1 节查看了在 MKL 库内部实现的快速傅里叶变换 (FFT)。对于较小的 $n$，Phi/MIC 设备上的 FFT 速度是 AVX 的两倍。对于较大的 $n$（如 $n=2^{26}$），FFT 似乎没有经过良好优化，在 Phi/MIC 设备上的速度慢了 8 倍以上。即使是 FFT 也只能达到峰值带宽的 15%，这一事实说明了指标有多大的误导性。为了接近峰值带宽，FFT 是比较 Phi 与其 AVX 宿机的良好基础。它是最常用的算法之一。与 LINPACK 基准测试不同，内存访问的代价无法完全隐藏。使用 FFT 类来测量 MIC 设备以及宿主机上的 FFT 耗。

```c
__declspec(target(mic))
class FFT {
private:
    DFTI_DESCRIPTOR_HANDLE handle;
public:
    FFT(int n, long count);
    ~FFT();
    void fwd(double*f){
        DftiForward(handle, f);
    }
    void bwd(double*f){
        DftiBackward(handle, f);
    }
};
```

__declspec(target(mic))
class FFT {
private:
    DFTI_DESCRIPTOR_HANDLE handle;
public:
    FFT(int n, long count);
    ~FFT();
    void fwd(double*f){
        DftiForward(handle, f);
    }
    void bwd(double*f){
        DftiBackward(handle, f);
    }
};

（注：此处原文代码块似乎存在重复或乱码，已根据指令保留代码格式且不翻译）

注意，hostmic_scale() 和 hostmic_sum() 的第一个参数是...

第 7.3.1 节查看了在 MKL 库内部实现的快速傅里叶变换 (FFT)。对于较小的 $n$，Phi/MIC 设备上的 FFT 速度是 AVX 的两倍。对于较大的 $n$（如 $n=2^{26}$），FFT 似乎没有经过良好优化，在 Phi/MIC 设备上的速度慢了 8 倍以上。即使是 FFT 也只能达到峰值带宽的 15%，这一事实说明了指标有多大的误导性。为了接近峰值带宽，FFT 是比较 Phi 与其 AVX 宿机的良好基础。它是最常用的算法之一。与 LINPACK 基准测试不同，内存访问的代价无法完全隐藏。使用 FFT 类来测量 MIC 设备以及宿主机上的 FFT 耗。

```c
__declspec(target(mic))
class FFT {
private:
    DFTI_DESCRIPTOR_HANDLE handle;
public:
    FFT(int n, long count);
    ~FFT();
    void fwd(double*f){
        DftiForward(handle, f);
    }
    void bwd(double*f){
        DftiBackward(handle, f);
    }
};
```

（注：原文提供的文本中存在大量重复和乱码的片段，翻译已根据“不要重复输出原文”的原则对具有逻辑的段落进行了对齐处理，但由于原文文本本身存在严重的逻辑重复和格式错误，此处呈现了核心逻辑的翻译。）

第 7.3.1 节查看了在 MKL 库内部实现的快速傅里叶变换 (FFT)。对于较小的 $n$，Phi/MIC 设备上的 FFT 速度是 AVX 的两倍。对于较大的 $n$（如 $n=2^{26}$），FFT 似乎没有经过良好优化，在 Phi/MIC 设备上的速度慢了 8 倍以上。即使是 FFT 也只能达到峰值带宽的 15%，这一事实说明了指标有多大的误导性。为了接近峰值带宽，FFT 是比较 Phi 与其 AVX 宿机的良好基础。它是最常用的算法之一。与 LINPACK 基准测试不同，内存访问的代价无法完全隐藏。使用 FFT 类来测量 MIC 设备以及宿主机上的 FFT 耗。

### 7.3.2 矩阵乘法

能够接近理论峰值的算法并不多。这些算法相对于它们访问的数据需要大量的算术运算。此外，它们的结构允许隐藏对同一数据的多次访问代价。数值代数是此类算法的主要来源。

在 $C = C + AB$ 中，$A, B, C$ 都是 $n \times n$ 矩阵，对于较大的 $n$，每个字节的数据都会执行大量的算术运算。

| n | AVX | AVX | MIC | MIC |
|---|---|---|---|---|
| Cycles log2 | Cycles/Byte | Cycles log2 | Cycles/Byte |
| 64 | 0.19 | 0.07 | 0.11 | 0.04 |
| 1,024 | 0.17 | 0.11 | 0.09 | 0.06 |
| 8,192 | 0.16 | 0.13 | 0.15 | 0.12 |
| 8,192 × 8,192 | 2.16 | 4.26 | 17.55 | 28.52 |

表 7.4：尺寸为 $n$ 的复 FFT 消耗的周期。对于 2.7 GHz AVX 宿主机（全称见表 A1）和 Phi/MIC 协处理器，报告的数字都是宿主机周期。

Xeon Phi 指令

在深入研究 Phi 架构之前，回到图 7.2 并总结 Phi 架构的几个特征。每个 Phi/MIC 核心可以调度运行多四个线程。硬件在单个周期内在线程之间切换。它倾向于轮询调度，并且永远不会执行同一个线程在

