

图 14.12 中的性能分析显示，计算时间的主要部分花费在复杂的矩阵-矩阵乘法（zgemm）上，这对应于式 (14.7)、(14.10)、(14.11) 和 (14.12) 中的运算。分析中第二个突出的热点是对称秩 2 更新 zher2k，它也在子空间对角化和正交化期间发生。因此，这些 BLAS 函数是卸载的自然目标。

Intel Math Kernel Library 提供的自动卸载是一种将最耗时的矩阵运算卸载到 Intel Xeon Phi 协处理器的选项。然而，由于算法允许在主机执行期间将一些大型数组保留在协处理器上，对卸载执行和数据传输进行更明确的控制可以大幅节省数据传输时间。此外，部分数据传输可以与主机执行异步进行，以进一步重叠计算和通信。

由于 GPAW 中的高级算法是用 Python 实现的，pyMIC 接口提供了一种非常方便的方式来控制数据传输和卸载执行。图 14.14 显示了一个初始化实网格上数组的例程片段，并且只需做最小的修改即可使数组也在协处理器上分配。稍后，如果输入数组的类型为 OffloadArray，则矩阵乘法将按图 14.15 所示进行卸载。图 14.16 显示了如何异步传输数据并与主机执行重叠。

尽管 GPAW 存在混合 MPI/OpenMP 版本，但在大多数实际情况下，纯 MPI 实现目前更快。因此，每个主机处理器核心一个 MPI 任务的执行模型是最合适的。由于典型的硬件配置每个节点包含一个或两个协处理器，因此 MPI 任务的数量会多于协处理器的数量。因此，协处理器被划分为更小的部分，使得每个 MPI 任务仅利用协处理器的部分。由于 MKL 在协处理器上使用 Intel OpenMP 运行时，因此可以通过 KMP_PLACE_THREADS 环境变量以直接的方式实现这一点。根据协处理器的数量和每个节点的主机核心数，包装脚本可以为每个 MPI 任务生成适当的 KMP_PLACE_THREADS 值，如图 14.17 所示。该包装脚本的灵感来自于《High Performance Parallelism Pearls, volume 1》第 17 章中展示的协处理器分区。

```
1  from gpaw.mic import stream
2  # ...
3
4  def zeros(self, n=(), dtype=float, global_array=False,
5      pad=False, usemic=False):
6      array = self._new_array(n, dtype, True, global_array, pad)
7      if usemic:
8          oa = stream.bind(array)
9          stream.sync()
10         return oa
11     else:
12         return array
```

**图 14.14**  
gd_zeros.py: 在 GPAW 的数组初始化方法中使用 OffloadArrays。

```python
def integrate(self, a_xg, b_yg=None,
             global_integral=True, hermitian=False,
             _transposed_result=None):
    # ...
    if isinstance(a_xg, mic.OffloadArray):
        result_yx_mic = stream.bind(result_yx)
        stream.sync()

    # ...
    if isinstance(a_xg, mic.OffloadArray):
        mic_gemm(self.dv, a_xg, a_yg, 0.0, result_yx_mic, 'c')
    else:
        gemm(self.dv, a_xg, a_yg, 0.0, result_yx, 'c')

    if isinstance(a_xg, mic.OffloadArray):
        result_yx_mic.update_host()
        stream.sync()

    # ...
    return result_yx
```

**图 14.15**  
gd_integrate.py: GPAW 中使用卸载数组的矩阵乘法。

```python
if use_mic:
    psit_xG.update_device()
    wfs.apply_pseudo_hamiltonian(kpt, hamiltonian,
                                 psit_xG.array,
                                 result_xG.array)
    result_xG.update_device()
    stream.sync()
else:
    wfs.apply_pseudo_hamiltonian(kpt, hamiltonian, psit_xG,
                                 result_xG)
```

**图 14.16**  
gpaw_async.py: GPAW 中的异步数据传输。

```
1 #!/bin/bash
2
3 # cores per node is given as input variable
4 ppn=$1
5 shift
6 rank=$PMI_RANK
7
8 # number of devices in the system
9 ndev=2
10
11 # number of cores per device
12 nphcores=61
13 nphcores=$((nphcores - 1))
14
15 # number of threads per physical core
16 tpc=4
17
18 # ranks per device
19 rpd=$((ppn / ndev))
20 if [ "$rpd" == "0" ]; then
21     rpd=1
22 fi
23
24 # physical cores per device
25 ncores=$((nphcores / rpd))
26
27 # partition number of the current rank on its device
28 partition=$((rank % rpd))
29
30 # offset for the current rank
31 offset=$((ncores * partition))
32
33 # build core selection string
34 places="${ncores}c,${tpc}t,${offset}o"
35
36 # fire up the actual run
37 MIC_KMP_AFFINITY=compact,verbose MIC_KMP_PLACE_THREADS=$places $@
```

**图 14.17**  
affinity_wrapper.sh: 用于为多个 MPI 任务分区协处理器的脚本。

## PyFR

PyFR 框架是我们将在本章中探索的另一个完整应用。它以不同的方式使用 pyMIC，将协处理器集成到使用 PyFR 框架的应用中。

### 概述

PyFR 是一个开源 Python 框架，用于求解形式为

∂u/∂t + ∇·f(u,∇u) = S(x,t) (14.13)

的对流-扩散问题，其中 u(x,t) 是表示解的状态向量，f 是通量函数，S 是源项。对流-扩散类型问题的典型例子是流体动力学的可压缩 Navier-Stokes 方程。PyFR 基于 Huynh 的通量重构 (FR) 方法。在 FR 中，首先将感兴趣的计算域离散化为符合网格的元素。在每个元素内部，定义了两组点：一组在元素内部，通常称为解点，另一组在元素边界上，称为通量点。

FR 的目标是获得 ∇·f 的近似值，该近似值位于与解相同的多项式空间中，可用于向前推进时间。实现这一点需要两种不同类型的运算 (i) 在通量/解点之间移动量，以及 (ii) 在单个解点或一对通量点处求取值（例如 f）。在移动量时，例如从解点到通量点，每个通量点的值被给出为该量在每个解点处的加权和

q_{e,i}^{(f)} = Σ_j α_{e,i j} q_{e,j}^{(u)} (14.14)

其中 q 表示量，e 为元素编号，i 为通量点编号，α_{e,i j} 是编码数值方法的系数矩阵。这可以识别为矩阵-向量乘积；或者在 N 个元素的模拟中，为 N 个矩阵-向量乘积。如果量首先从物理空间映射到参考空间，则 α_{e,i j} 系数对给定类型的每个元素都相同。因此，上述运算可以简化为单个矩阵-矩阵乘积。根据精度阶数，PyFR 在 ~50% 到 ~85% 的墙钟时间内花费在执行此类乘法上。剩余时间花费在逐点运算上。这些核是 f(in1[i], in2[i], ..., &out1[i]) 形式的推广。由于迭代之间没有数据依赖，逐点核既易于并行化，又高度受可用内存带宽限制。

### 运行时代码生成

PyFR 旨在支持各种现代硬件平台。虽然矩阵乘法可以卸载到厂商提供的 BLAS 库，但逐点运算必须为每个关键平台单独编写代码。这在将新物理添加到代码方面构成了进入壁垒，并进一步代表了重大的维护负担。为避免这种情况，PyFR 中的逐点核以基于 Mako 模板引擎的类 C 领域特定语言指定。该语言利用了至少对于逐点运算而言——主要并行编程语言
