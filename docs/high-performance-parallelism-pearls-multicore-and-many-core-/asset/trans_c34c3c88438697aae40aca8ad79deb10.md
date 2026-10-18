

自动向量化内核的代码更为复杂，因为必须满足一系列约束条件才能使编译器生成预期的代码。首先，无论如何 VEC_LENGTH 都必须设为 16，其次，部分索引计算必须移出内核到特殊的 NDRange 形状中。否则，编译器无法识别连续的访问模式。

在原生 C 或 C++ 内核中，我们可以通过 Intel® Composer 包含的编译器优化报告来验证编译器是否按预期执行，或者是否仍发出 gather 和 scatter 指令。由于 Intel OpenCL 编译器不提供详细的优化报告，唯一了解编译器实际执行情况的方法就是查看汇编代码。在此过程中，我们还发现了一个影响自动向量化内核性能的对齐问题。

```
/* in the host program */
#define VEC_LENGTH 16 // for the MIC: regardless of float or double!
size_t work_dim = 2;
size_t global_work_size[] = {VEC_LENGTH, num_sigma / VEC_LENGTH};
size_t local_work_size[] = {VEC_LENGTH, 1};
clEnqueueNDRangeKernel(queue, kernel, work_dim, 0, global_work_size,
    local_work_size, 0, 0, 0);

/* in the kernel code */
#define package_id ((get_group_id(1)) * (VEC_LENGTH * 2 * DIM * DIM)) // the
    package of matrices processed by this work-group
#define sigma_id get_local_id(0) // the sigma matrix processed by this work-item

#define sigma_real(i, j) (package_id + 2 * VEC_LENGTH * (DIM * (i) + (j)) +
    sigma_id)
#define sigma_imag(i, j) (package_id + 2 * VEC_LENGTH * (DIM * (i) + (j)) +
    VEC_LENGTH + sigma_id)

#define ham_real(i, j) ((i) * DIM + (j))
#define ham_imag(i, j) (DIM * DIM + (i) * DIM + (j))
```

# FIGURE 19.4

自动向量化内核的混合 SoA 内存布局的内核调用和索引方案。编译器需要 VEC_LENGTH 为 16。需要二维 NDRange 来直接将 sigma_id 映射到 work-group 维度 0 的 local id。否则，连续的访问模式无法被识别。

```
/* in the host program */
size_t work_dim = 1;
size_t global_work_size[] = {num_sigma / VEC_LENGTH};
clEnqueueNDRangeKernel(queue, kernel, work_dim, 0, global_work_size, 0, 0, 0, 0);
/* in the kernel code */
// number of package to process == get_global_id(0)
#define package_id (get_global_id(0) * DIM * DIM * 2)

#define sigma_real(i, j) (package_id + 2 * (DIM * (i) + (j)))
#define sigma_imag(i, j) (package_id + 2 * (DIM * (i) + (j)) + 1)

#define ham_real(i, j) ((i) * DIM + (j))
#define ham_imag(i, j) (DIM * DIM + (i) * DIM + (j))
```

# FIGURE 19.5

手动向量化内核的混合 SoA 内存布局的内核调用和索引方案。我们将 work-group 形状留给 OpenCL 实现，并为每个 VEC_LENGTH 个矩阵的包创建一个 work-item。

就 OpenCL 标准而言，对齐与缓冲区类型相匹配——即标量。无法向编译器传达其他对齐方式，而且 Intel OpenCL 实现本身也不会强制执行正确的对齐。因此，向量加载是连续的但未对齐。这是已知问题，希望在未来版本中得到修复。在此之前，手动向量化会带来明显更好的性能，正如本节后面将展示的那样。

## COMPILE-TIME CONSTANTS

OpenCL 独有的优化策略是利用其运行时内核编译。OpenCL 应用程序的内核代码通过主机代码中的一组 OpenCL 库调用进行编译。这使得它能够采用仅在运行时才知道的输入值，例如 σ 矩阵的矩阵维度，并将其作为“编译时”常量传递给内核。

在 Hexciton 基准代码的情况下，这使得循环展开成为可能，并允许编译器解决更大的索引计算部分。通过在汇编代码中统计 FMA 指令（每个内部循环迭代 4 条 vfmadd 和 4 条 vfnmadd），可以轻松验证所应用的循环展开。然而，对于具有 gather 和 scatter 的内核变体，循环展开并无益处。这意味着决定是否应用循环展开的编译器某些度量在这些情况下似乎失效了。

我们还使用编译时常量将 SIMD 宽度作为 VEC_LENGTH 传递给内核。这用于索引计算以及将 real_vec_t 映射到正确的 OpenCL 向量类型，例如 Intel Xeon 处理器上的 double4 和 Intel Xeon Phi 协处理器上的 double8。

## PREFETCHING

预取是指在数据实际使用之前将其带入缓存的活动。其设计目的是掩盖从内存获取数据所需的大延迟。许多处理器会基于启发式方法自动或隐式地执行预取。也有显式预取的编程方法，可以利用程序员的专业知识及其对特定算法的了解。

OpenCL 提供了显式预取的内置函数。对于没有临时变量的手动向量化内核变体，添加如图 19.6 所示的手动预取可显著改善内核运行时间。对于所有其他变体，则无效。

影响软件预取的另一种可能性是 Intel 特定的 OpenCL 编译器选项 -auto-prefetch-level=n，其中 n 的值在 0 到 3 之间。值为 0 禁用自动预取，其他值会随后增加自动预取量。

```
for (i = 0; i < DIM; ++i) {
    // prefetch result memory for the inner loops
    j = 0;
    prefetch(&sigma_out[sigma_real(i, j)], 2 * DIM);
    for (j = 0; j < DIM; ++j) {
        for (k = 0; k < DIM; ++k) {
            /* commutator arithmetic */
        }
    }
}
```

# FIGURE 19.6

一个对手动向量化内核确实有益的显式预取示例。

根据文档，默认值 2 在大多数情况下表现最佳。较低的级别建议用于计算受限的内核。在 Intel Xeon 处理器上，我们几乎无法从此设置中测量到 Hexciton 内核的任何影响。在 Intel Xeon Phi 协处理器上，所有内核变体的级别 1-3 性能相同。

正如预期的那样，禁用自动预取会降低某些内核变体的性能。对于其他变体则没有影响。然而，对于某些变体，可以观察到超过 2× 的显著性能提升，尽管内核明显受内存限制。因此，我们建议至少在 Intel Xeon Phi 协处理器上比较值为 0 和默认值 2。有关自动软件预取的更多信息，可在“更多信息”部分末尾引用的 Intel OpenCL 优化指南中找到。

## OPENCL PERFORMANCE RESULTS

我们使用 Intel OpenCL 1.2 SDK（4.6.0.92）在 Intel Xeon 处理器（Sandy Bridge 和 Haswell）以及 Intel Xeon Phi 协处理器上评估了一大批内核变体。使用的指标是每次迭代的平均内核运行时间，测量了 50 次运行，每次 100 次迭代，外加每次 5 次预热迭代。图中误差条显示最小值和最大值。运行时间反映了 Hexciton 内核一次迭代的执行时间，用于计算 2¹⁹ 个复数 7×7 矩阵的交换子，不包括 OpenCL 缓冲区传输和主机代码执行。测量内核周围的环境会使量化生成代码的效率变得更困难。图 19.7

![](img/16cb41208935c5f22dd1044f03f2e31b_414_0.png)

# FIGURE 19.7

应用于 Hexciton 基准内核的不同优化策略的效果。我们在 Sandy Bridge 和 Haswell Intel Xeon 处理器上分别实现了 2.0× 和 1.2× 的加速，在 Intel Xeon Phi 协处理器上实现了 5.9× 的加速，相对于初始版本。

显示了不同优化策略的影响，依次应用于初始内核。我们选择此顺序，因为它在每一步都显示出改进——至少对于 Intel Xeon Phi 协处理器而言。当我们试验代码时，即使对于这样一个小内核，也必须探索一个很大的组合空间，才能最终得到这些教学变体。可下载的 Hexciton 基准代码包含比此处所示更多的内核变体。

在我们对代码的工作中，总是会出现一种优化在一种内核中实际产生负面影响，但在另一种内核中会提高性能的情况。例如，编译时常量只有在内存访问连续后才变得有益。如果更早应用，结果的循环展开会显著降低性能。不幸的后果是，优化方法，即搜索最优解的空间中的维度，不能仅仅因为在一种上下文中不成功就被放弃。然而，最重要的优化，即最不可能导致性能下降的优化，是过渡到允许连续向量加载和存储的内存布局。这需要对所应用的向量化策略有精确的了解，无论它是手动实现还是由编译器生成。虽然 Intel OpenCL 向量化器的策略有很好的文档记录，但原生 C/C++ 内核的自动向量化则要不那么明显。但对于 OpenCL 代码而言，即使不是针对特定设备，也不能对在主机程序运行时可能用于编译内核的设备特定编译器的向量化策略做出一般性假设。事实上，我们甚至不能假设目标硬件具有某种 SIMD 硬件。在 GPU-HEOM 中，OpenCL 被用作在同一编程模型、语言和工具集中为不同平台创建高效内核的手段——而不是编写单个内核并希望可移植性能的奇迹发生（尽管这个想法很有吸引力）。

图 19.8 比较了在 Intel Xeon 处理器和 Intel Xeon Phi 协处理器上，其他条件相同的情况下手动向量化和自动向量化的差异。Intel Xeon Phi 协处理器上最快的手动向量化和自动向量化代码之间的差距为 40%。原因是我们之前描述的对齐问题。它导致自动向量化代码中出现未对齐的向量加载和存储。目前，在 Intel Xeon Phi 协处理器上，OpenCL 中的手动向量化是生成高效代码的强制要求。对于 Intel Xeon 处理器，两种方法性能相似，Sandy Bridge 上只有很小的差异。在 Haswell 上，基本上没有（<1%）差异——无论是手动和自动向量化之间，还是不同内核之间。事实上，除了新的内存布局与正确的 NDRange 组合之外，任何额外的内核优化对 Haswell 架构上测量的性能都没有影响。

## PERFORMANCE PORTABILITY IN OpenCL

尽管 OpenCL 在各种同构和异构平台上提供代码可移植性，但性能可移植性则是另一回事。虽然针对不同 OpenCL 平台优化内核的总体思路可能相似，但要获得最高可实现性能需要使用平台特定的优化策略。这通常会导致优化在一种平台上提高性能，但在另一种平台上显著降低性能的情况。

有两个选择，(a) 完全放弃设备特定的优化，旨在获得单一实现，具有可移植但次优的性能，或 (b) 维护多个经过优化但设备特定的实现。是否值得付出 (b) 的努力显然取决于次优程度有多大

