

blocks 从块列表中移除并处理下一阶段。此外，可以设置 C_t 的最小值（称为 minCt），例如在多插槽情况下，minCt 可以设置为插槽数。在分配内存时，会遍历各阶段，在 cc-NUMA 感知的实现中，正确的核心可以触及内存的适当区域。我们对分割的启发式终止标准是，不将 T 维度分割成超过四个 MinCt 块。

至此，核心到阶段的分配设置已完成；然而，能够查找块如何分配到阶段的信息也很重要。这是在文件 dslash_body.h 中 Dslash 的构造函数里完成的，该文件位于 include/qphix 中，我们在图 9.15 中展示。这里，对于每个线程，我们设置了它在每个阶段应处理的块。对于每个阶段，线程 ID 被拆分为核心 ID 和 SMT 线程 ID。核心 ID（cid）被拆分为 T 坐标和 Y-Z 坐标（分别为 binfo.cid_t 和 binfo.cid_yz），并且计算块原点的坐标 binfo.by、binfo.bz 和 binfo.bt 以及块的时序范围 binfo.nt。

## SMT 线程

在 Intel Xeon Phi 协处理器的每个核心上有四个 SMT 线程可用，我们可以想象多种遍历 Y-Z 块的方式。我们在图 9.16 中展示了三种可能的方式。最终，我们选择让用户通过指定 S_y 和 S_z 作为 Y-Z 网格的维度来指定 SMT 线程的“形状”。Y-Z 块中的晶格位点随后在 SMT 线程之间交错。最简单的是描述 Y 交错的情况（S_y = 4，S_z = 1）。在这种情况下，线程 0 将处理 Y 坐标为 y 的位点，线程 1 将处理 Y 坐标为 y + 1 的位点，线程 2 将

```
#pragma omp parallel shared(num_phases)
{
    int tid = omp_get_thread_num();
    int cid = tid / n_threads_per_core;
    int smtid = tid - n_threads_per_core * cid;
    int ly = Ny/By;
    for(int ph =0; ph < num_phases; ph++){
        const CorePhase& phase = s->getCorePhase(ph);
        BlockPhase& binfo = block_info[num_phases*tid+ph];
        int nActiveCores = phase.Cyz * phase.Ct;
        if( cid > nActiveCores ) continue;
        binfo.cid_t = cid / phase.Cyz
        binfo.cid_yz = cid - binfo.cid_t * phase.Cyz;
        int syz = phase.startBlock + binfo.cid_yz;
        binfo.bz = syz / ly;
        binfo.by = syz - binfo.bz * ly;
        binfo.bt = (Nt*binfo.cid_t) / phase.Ct;
        binfo.nt = (Nt*(binfo.cid_t+1)) / phase.Ct - binfo.bt;
        binfo.by *= By;
        binfo.bz *= Bz;
        int ngroup = phase.Cyz*Sy*Sz;
        binfo.group_tid = tid % ngroup;
    }
} // OMP parallel
```

### FIGURE 9.15

Load balancing block phase set-up in dslash_body.h.

![](img/16cb41208935c5f22dd1044f03f2e31b_206_0.png)

### FIGURE 9.16

We show three possible ways for four SMT threads to traverse the sites in a block: lexicographic in Y interleaved (left), a 2 × 2 block in Y-Z interleaved (middle) or scanning along Y for four separate Z-coordinates interleaved (right).

处理 Y 坐标为 y + 2 的位点，线程 3 将处理 y + 3。然后线程 0 将处理 y + 4，线程 1 将处理 y + 5，依此类推，本质上以字典顺序遍历块。另一种替代方案是将子块分配给每个 SMT 线程。例如，在块 (B_y,B_z) = (4,4) 的情况下，我们可以让每个线程处理一个 2 × 2 子块。然而，我们将自己限制在交错遍历上，希望 SMT 线程在位点之间交错可以改善 L1 缓存中的共享。

## 晶格遍历

现在有了来自负载平衡的阶段知识、SMT 线程布局以及向量化的具体细节，我们可以查看晶格遍历的简化形式。我们展示了文件 dslash_body.h 中函数 DyzPlus 的一些代码，如图 9.18 所示，其中删除了大量次要细节和预取指针的计算以提高清晰度。完整代码可在源代码包中找到。需要强调的关键点如下：每个线程遍历阶段，首先确定其在该阶段的块或是否空闲。一旦找到块，T、Z 和 Y 的循环就如我们所期望的那样进行。Z 循环以 Sz 的增量进行，Y 循环以 ngy*Sy 的增量进行（代码中实际拼写错误为 nyg），其中 Sy 和 Sz 是 SMT 线程网格维度。X 循环遍历 SOAs（nvecs 是棋盘化 X 维度中 SOA 长度的数量）。

在 Z 和 T 维度访问当前 X-Y 块的邻居是直接的，一旦 Z 和 T 坐标已知，其块就可以被识别。它们由指针 tfBase（T 前向）、tbBase（T 后向）、zfBase 和 zbBase 指向。

然而，由于在 X 和 Y 上的向量化，访问这些维度的邻居很棘手，因为它可能需要来自相邻块的数据。我们在图 9.17 中展示了一个简单情况。根据 Y 坐标，给定颜色（例如红色）的第一个位点可能确实是该 Y 坐标在晶格中的第一个位点（图中 xodd=0）。在这种情况下，其前向邻居可以以直接的方式来自另一棋盘的第一个块。然而，也可能给定棋盘的第一个位点实际上是晶格中的第二个位点（xodd=1）。在这种情况下，前向邻居位点实际上来自其他颜色的两个不同块，必须将其混合在一起。此外，由于周期性边界条件，必须区分输出块是否位于 X 维度的开头或结尾（换行到另一端的块）或不位于开头或结尾的情况。必要的偏移量在构造函数中预先计算到数组 xb0ffs_x0_xodd（X 维度起始处的后向邻居）和 xf0ffs_xn_xodd（X 维度末尾的前向邻居）中，以及

![](img/16cb41208935c5f22dd1044f03f2e31b_207_0.png)

### FIGURE 9.17

Locating neighbors in the forward X-direction, in a simple case with an X-Y tile size of 2 × 1. In the top diagram, we show the sites as they appear in the lattice. We show the forward neighbors needed by the first two red-sites in each row by connecting them to their partner sites with arrows. In the lower diagram, we have separated the differently colored sites into separate arrays, which are then tiled over. For the first red tile on line xodd=0, one needs only the same corresponding blue tile. However, for the first red tile on line xodd=1, the neighboring blue sites come from two blue tiles and need to be blended.

xbOffs_xodd（后向 X 邻居偏移）和 xfOffs_xodd（前向 X 邻居偏移）用于其他情况。同样，也存在类似的偏移数组来识别 Y 方向的邻居。

图 9.18 中 X 循环的最后步骤是确定是否处于 xodd=0 或 xodd=1 的情况，并根据 x 坐标从预先计算的偏移中适当选择到 xfOffs、xbOffs（分别为后向和前向 X 偏移）以及 Y 方向的 ybOffs 和 yfOffs。指针 oBase 是输出旋量的 Y-Z 块基址的指针，gBase 是规范场的相应部分的指针。其他计算的量（在源代码中但此处未打印）主要是为该线程的工作下一迭代的预取指针。

一旦所有工作完成，代码最终调用 dslash_plus_vec 函数，该函数执行此循环中识别的指针的 Dslash 工作。这是代码生成器生成的代码，我们现在将考虑它。

## 使用 QphiX-codegen 进行代码生成

我们现在考虑如何为关键函数 dslash_plus_vec 及其变体编写内核。为此，我们决定编写一个代码生成器，可以在代码分发中 qphix-codegen 子目录下找到，也可从 GitHub 获取（参见“更多信息”部分）。

我们编写代码生成器的最初动机如下：首先，我们希望最终将预取插入代码以改善内存流量。当代码拆分为许多小的内联函数时，这很 awkward。让一个小代码生成器生成整个向量（以及后来的 X-Y 块）Dslash 内核的完全内联主体是有意义的。使用代码生成器还允许我们使用编译器内在函数并直接访问流式存储、gather、loadpack 和其他指令。代码生成器的第二个特点是，一旦我们编写了

