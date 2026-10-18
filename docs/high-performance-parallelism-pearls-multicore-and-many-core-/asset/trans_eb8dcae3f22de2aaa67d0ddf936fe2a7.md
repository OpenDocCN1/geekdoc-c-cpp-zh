

![](img/16cb41208935c5f22dd1044f03f2e31b_94_0.png)

# 图 4.1

SW 算法中的数据依赖。

在 DP 矩阵计算中，每个单元依赖于其左侧、上方和左上（对角）相邻单元，如图 4.1 所示。这种依赖关系也意味着同一次对角线上的所有单元可以并行计算，并且可以按照从左上角到右下角的次对角线顺序在线性空间内进行计算。在给定评分方案下，最优局部比对得分对应于矩阵 H 中的最大值。整体计算具有 O(mn) 的二次计算复杂度；在需要和不需要检索最优比对的情况下，空间复杂度分别为 O(m+n) 和 O(min(m, n)) 的线性空间复杂度。请注意，本章我们只关心计算最优局部比对得分，而不关心获得该最优得分的实际比对。

我们假设在比对矩阵中，S1 垂直放置，S2 水平放置，且 m ≤ n（见图 4.1）。将比对矩阵视为笛卡尔平面上的二维坐标空间，我们假设原点位于左上角，水平坐标 x（对应列）从左到右递增，垂直坐标 y（对应行）从上到下递增。因此，对于对角线 d（0 ≤ d < m + n − 1）上的单元，其坐标 (y, x)（其中 x 为列索引，y 为行索引）与 d 的关系可表示为 x + y = d。可以看出，起始行索引 srow 可通过计算对角线 d 与直线 y = 0 或 x = n − 1 的交点来确定，结束行索引 erow 可通过 d 与直线 y = m − 1 或 x = 0 的交点来确定。基于上述观察，我们计算对角线 d 的 srow 和 erow 为 srow = max(0, d − n + 1) 和 erow = min(d, m − 1)。对于分块矩阵中的外部对角线也可以进行类似的计算（见图 4.2）。

## 单协处理器上的并行化

我们在单个协处理器上的并行化基于 scale-and-vectorize 方法。我们首先将 DP 矩阵划分为大小为 α × β 的分块，并使用 OpenMP 将它们分配到一组线程上。我们将这种基于分块的对角线称为外部对角线。分块 DP 矩阵的布局如图 4.2 所示。我们的分块方案在概念上将比对矩阵重新组织为大小为 R × C 的分块 DP 矩阵，其中 R = ⌈m/α⌉，C = ⌈n/β⌉。在分块比对矩阵中，外部对角线 d（0 ≤ d < R + C − 1）上的所有分块的计算可以独立进行。在每个分块内，我们可以

![](img/16cb41208935c5f22dd1044f03f2e31b_95_0.png)

# 图 4.2

分块 DP 矩阵的布局。

因此，可以使用基于 512 位 SIMD 向量中指令级并行的向量化技术，并行计算同一次对角线上的单元。我们将分块内的次对角线称为内部对角线。

在启用多线程时，我们将分块比对矩阵配置为具有 C = T（其中 T 等于线程数）列（因此 β = ⌈n/T⌉），以便在指令级和线程级利用率之间进行权衡。对于向量化，我们将 512 位 SIMD 向量拆分为 16 个通道，每个通道占 32 位。在我们的算法中，向量通道数用 V 表示，等于 16。在我们的实现中，我们默认使用 α = V，同时允许用户通过参数指定其值（必须是 V 的倍数）。

## 使用 OpenMP 的多线程

在任意外部对角线 D 上，T 个线程并行计算外部对角线上的所有分块（见图 4.2）。在进入下一条外部对角线之前，线程需要进行同步。每个分块需要来自上方相邻分块的 H 和 E 值对、来自左方相邻分块的 H 和 F 值对，以及来自左上相邻分块的一个 H 值。线程之间必要的通信实现如下。

- 垂直方向：我们分配一个大小为 O(n) 的全局水平（GH）缓冲区，用于存储整个比对矩阵的上方 H（H_up）和上方 E（E_up）值。在此上下文中，“全局”表示这些缓冲区在我们的 OpenMP 并行区域中可见并由所有线程共享。在计算过程中，单元可以通过其在比对矩阵中的全局列索引（记为 globalCol）访问所需的 H_up 和 E_up 值。在分块内，我们从 GH 缓冲区读取 H_up 和 E_up 值对来计算第一行，然后用最后一行的所有单元新计算出的 H 和 E 值对更新该缓冲区。

```
#pragma omp parallel firstprivate(GV,GD) default(shared)
for (d=0; d < R+C-1; ++d) {
    sExtRow = max(0,d-C+1);
    eExtRow = min(d,R-1);
    load the per-thread maximum score lmaxScore;
    #pragma omp barrier
    #pragma omp for schedule(static,1) nowait

    for (r=sExtRow; r <= eExtRow; ++r)
        compute all cells in tile(r,d-r);
    save lmaxScore to a global variable;
    swap the input and output of GV and GD;
}
reduce to get the optimal local alignment score;
```

# 图 4.3

多线程计算的内核（参见 AlignCoreTiling.cpp 中的 _swKernelShared() 函数）。

- 水平方向：我们分配 C 个全局垂直（GV）缓冲区，每个缓冲区包含 α 个元素，用于存储 α 个左侧 H（H_left）和左侧 F（F_left）值对。分块比对矩阵的每一列 c（0≤c<C）恰好有一个 GV 缓冲区。所有 GV 缓冲区通过（循环）缓冲流水线进行通信，其中列 c 上的每个分块从第 c 个 GV 缓冲区读取 H_left 和 F_left 值以计算第一列，并将最后一列所有单元新计算出的 H 和 F 值写入第 (c+1) 个 GV 缓冲区。

- 对角方向：我们为分块比对矩阵的每一列 c 分配一个单元素全局对角（GD）缓冲区，用于存储相应分块所需的对角 H（H_diag）值。所有 GD 缓冲区以与 GV 缓冲区相同的方式更新。

图 4.3 展示了在外部对角线上进行计算的协处理器内核。在进入当前对角线计算的 for 循环之前，我们通过屏障（barrier）同步所有线程。我们使用 nowait 子句移除了紧随循环之后的隐式屏障。此外，通过静态调度策略（即 schedule(static, 1)），每次将一个分块分配给一个线程。我们的意图是让具有连续 ID 的线程沿对角线访问连续的向量大小元素。这种调度策略与“平衡”亲和性相结合，使每个核内驻留的四个线程具有良好的数据局部性，从而能够受益于 L1/L2 缓存层次结构。

## 使用 SIMD 内建函数的向量化

分块被分配给一个线程，然后通过 SIMD 向量化进行计算。我们将分块分割为 α/V 个条带，每个条带包含 V 行，并从上到下逐条带完成整体计算。这种条带化计算在每个线程内部进行，通过减少空闲向量通道数和指令数来提高每个线程内的向量化效率。在分块内，GH、GV 和 GD 缓冲区是复用的，因此我们

```
Compute the column index globalCol of the stripe in the
alignment matrix;
Compute the starting index startIndex of the GV buffer
for the stripe;
for (i=16; i < numTileCols; ++i, ++globalCol) {
    vHUp = _mm512_set1_epi32(GH[globalCol].h);
    vEUp = _mm512_set1_epi32(GH[globalCol].e);
    vWUp = _mm512_alignr_epi32(vF, vHUp, 15);
    vHUp = _mm512_alignr_epi32(vH, vHUp, 15);
    vE = _mm512_sub_epi32(vEUp,vGapExtend);
    vTmp = _mm512_sub_epi32(vHUp,vGapOE);
    vE = _mm512_max_epi32(vE,vTmp);
    vF = _mm512_sub_epi32(vF,vGapExtend);
    vTmp = _mm512_sub_epi32(vH,vGapOE);
    vF = _mm512_max_epi32(vF,vTmp);
    Compute the substitution score vSubScore;
    vH = _mm512_add_epi32(vHDiag, vSubScore);
    vTmp = _mm512_max_epi32(vE,vF);
    vH = _mm512_max_epi32(vH,vZero);
    vH = _mm512_max_epi32(vH,vTmp);
    lmaxScore = _mm512_max_epi32(lmaxScore,vH);
    vHDiag = vHUp;
    Save the H and E values for the cell on the last
    row of the stripe
}
Save the H and F values for the cell on the last column
of the stripe;
```

# 图 4.5

步骤 2 的向量化计算内核（参见 AlignCoreTiling.cpp 中的 _swKernelShared() 函数）。

## 使用 MPI 跨多个协处理器进行并行化

我们在协处理器集群上的分布式并行化基于 MPI 卸载模型设计，该模型仅在主机 CPU 上启动 MPI 进程，并利用进程内的卸载能力将部分工作负载卸载到相应的协处理器上。在此模型中，协处理器之间的通信必须由主机通过卸载指令显式管理。跨多个 Intel Xeon Phi 协处理器的分布式方法的核心思想基于二级分块。我们进一步将比对矩阵划分为更大的块，大小为 αₘₚᵢ × βₘₚᵢ，将矩阵重新组织为 Rₘₚᵢ = ⌈m/αₘₚᵢ⌉ 行和 Cₘₚᵢ = ⌈n/βₘₚᵢ⌉ 列（见图 4.6）。

我们将相应的对角线称为块对角线。此类对角线内的所有块分布在一个协处理器网络上，每个块分配给一个协处理器。在任何块内，在单个协处理器上采用前述分块方法的一种变体，该变体会额外处理由其他 MPI 进程计算的中间数据。与分块方法类似，

