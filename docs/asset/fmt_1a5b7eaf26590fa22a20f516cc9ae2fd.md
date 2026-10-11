
对于密度函数 `$f^D$` 的极大值 `$x^*$`，基于中心的簇是子集 `C ⊂ D`，其中 `x ∈ C` 被 `$x^*$` 吸引且 `$f^D(x*) ≥ ξ$`。如果点 `x ∈ D` 被 `$f^D(x^*) < ξ$` 的局部极大值 `$x^*$` 吸引，则称这些离群值。

`OptGrid` 选择一组投影。这些投影用于寻找最优簇。投影是因为它们控制了点的密度，而切割平面将具有低密度。每个切割面的选择是为了使其具有最小的点并分离两个密集的半空间。在构建函数的每个步骤之后，该算法被递归地应用于簇。在每一轮递归中，`OptGrid` 只维护上一轮递归密度中的数据对象。算法 `OptGrid` 描述在算法 33 [10, 12] 中。

`OptGrid` 的时间复杂度为 `O(N log N)`，其中 `N` 是数据点数量，`d` 是数据的维度。这对于高维数据库聚类非常高效。然而，在定位嵌入高维数据库低维子空间的簇时，它的性能可能较差，其递归方法每一步都会减少维度 [10]。

# 算法 33 OptiGrid 算法

**输入：** 数据集 `D`，`q`，`min_cut_score`

1. 确定收缩投影集 `P = {P_0, P_1, …, P_k}` 并计算数据集 `D` 的所有投影：`P(D), i = 1, 2, …, k`；
2. 初始化划分平面列表 `BEST_CUT ← Φ`，`CUT ← Φ`；
3. 对于 `i = 0` 到 `k`
4. `CUT ←` 最佳划分 `P_i(D)`；
5. `CUT_SCORE ←` 最佳划分 `P_i(D)`；
6. 在 `BEST_CUT` 中插入所有得分 `≥ min_cut_score` 的划分平面；
7. 如果 `BEST_CUT = Φ` 则
8. 将 `D` 作为聚类返回；
9. 否则
10. 从 `BEST_CUT` 中选择得分最高的 `q` 个划分平面，并使用这 `q` 个划分平面构建多维网格 `G`；
11. 将所有数据点插入 `G`，并将确定的高密度网格单元添加到聚类 `C_i`；
12. 精炼 `C_i`；
13. 对于 `C` 中的所有聚类 `C_j`
14. 对 `C_j` 执行相同的过程；
15. 结束循环
16. 结束如果
17. 结束循环

对于用户而言，这种困难仅根据研究的数据确定。然而，该算法的特殊情况可以认为是 `CLIQUE` 的一种更有效的变体。也就是说，如果使用的投影在每个维度上的密度估计是均匀的，并且有足够的划分平面，那么可以实现更高效且准确的聚类，且其时间复杂度在维度上不再是指数级的。

#### 6.5.4 OptiGrid 的变体

在本节中，我们考虑了 `OptiGrid` 的变体，这些变体旨在解决网格结构的可扩展性问题，特别是关于可用内存、网格检索的效率，以及划分平面的选取标准。

### 6.5.4.1 O-Cluster：一种可扩展的方法

`Milenova` 提出了 `O-Cluster`（正交划分）[20] 来解决 `OptiGrid` 的三个局限性：内存大小的可扩展性、确定划分平面是否最优的标准，以及对噪声的敏感性。`O-Cluster` 通过对原始数据使用随机采样技术解决了第一个局限性，只有歧义（ambiguous）的数据点保留在缓冲区中。作为 `OptiGrid` 的一种变体，`O-Cluster` 使用并行划分策略来定位数据中的高密度区域。`O-Cluster` 使用了收缩投影，但也建议使用统计检验来验证划分平面的质量。统计检验检查密度之间的统计显著性，标准的 `χ²` 测试。如果发现了统计显著性，则通过这种网格进行划分平面。

`O-Cluster` 也是一种递归方法。在对所有投影进行划分测试后，选择最优的一个来划分数据。分层树结构用于将数据划分为矩形区域。主要步骤总结在算法 34 中。

# 算法 34 O-Cluster 算法

1. 加载数据缓冲区。
2. 计算活跃划分的直方图。
3. 为活跃划分寻找“最佳”划分。
4. 标记歧义和“冻结”划分。
5. 划分活跃划分。
6. 重新加载缓冲区。

`O-Cluster` 的复杂度近似 `O(Nd)`，其中 `N` 是数据点数量，`d` 是维度。然而，`Hinnebruck` 和 `Keim` 声称高维噪声数据的聚类证明存在超线性下界 [12]。他们的证明草稿解决了给定 `O(N)` 数量的数据必须搜索的问题，即对于随机噪声没有常数时间。此外，`OptGrid` 的复杂度受插入网格结构时间的影响。他们断言并行插入平面为 `O(Nq)`，其中 `q` 是平面数量，`f` 是插入时间；由于插入时间是常数 `f`，`O-Cluster` 使用二叉树且为 `O(Ns)`，其中 `s` 是二叉树的深度，但未提供划分深度的最坏情况分析。`O-Cluster` 显示了小缓冲区的可扩展性。

虽然 `O-Cluster` 可以处理均匀噪声，但其性能随噪声的增加而下降。与 `OptGrid` 不同，它也有划分聚类的倾向，因为它于过度划分数据空间且使用的直方图无法充分匹配密度分布。然而，由于递归深度限制，`OptGrid` 在处理嵌入高维特征空间的低维子空间的聚类时可能会遇到困难 [10]。

### 6.5.4.2 CBF：基于单元的过滤

`Chang` 和 `Jin` 提出了基于单元的过滤（Cell-Based Filtering）[4]，解决了网格结构的可扩展性、内存中大型数据集的处理以及网格检索的效率。它还为划分平选取提供了明确的标准。（基于单元的过滤）[4] `Chang` 和 `Jin` 解决了网格结构的可扩展性、内存中大型数据集的处理以及网格检索的效率。它还为划分平面的提供了明确的标准。（基于单元的过滤）[4] `Chang` 和 `Jin` 解决了网格结构的可扩展性、内存中大型数据集的处理以及网格检索的效率。它还为划分平面的提供了明确的标准。（基于单元的过滤）[4] `Chang` 和 `Jin` 解决了网格结构的可扩展性、内存中大型数据集的处理以及网格检索的效率。它还为划分平面的提供了明确的标准。（基于单元的过滤）[4] `Chang` 和 `Jin` 解决了网格结构的可扩展性、内存中大型数据集的处理以及网格检索的效率。它还为划分平面的提供了明确的标准。（基于单元的过滤）[4] `Chang` 和 `Jin` 解决了网格结构的可扩展性、内存中大型数据集的处理以及网格检索的效率。它还为划分平面的提供了明确的标准。

# 数据聚类：算法与应用

| 经典算法 | 轴偏移网格算法 | 自适应网格算法 |
| :--- | :--- | :--- |
| | 全维度算法 | `GRIDCLUS` `STING` `WaveCluster` `GIDLC` `NSGC` `AMR` |
| **静态数据** | `BANG-clustering` `STING+` | `ASGC` `ADCC` (`ACICA+`) | |
| | 高维算法 | `GCHL` `GCA` `OptGrid` | `CLIQUE` |
| | | `O-cluster` `CBF` `EN-ENCLUS` | `MAFIA` |
| **流式数据** | `D-Stream` `Ducstream` | `SGCS` | |

图 6.3: 各基于网格的算法之间的关系。

## 参考文献

- [1] Rakesh Agrawal, Johannes Gehrke, Dimitrios Gunupulos, and Prabhakar Raghavan. 用于数据挖掘应用的高维数据自动聚类. 见 Proceedings of the 1998 ACM SIGMOD International Conference on Management of Data, SIGMOD '98, pages 94–105, New York, USA, ACM.
- [2] Mounir Bechini, Angel Goglin, Guillaume Rasche, and Noureddine Mouaddib. 模糊结果的多维基于网格的聚类. 研究报告, INRIA, 2008. DOI: https://hal-archives.archives.fr/hal-00034654/en
- [3] Pavel Berkhin. 数据挖掘技术综述. 技术报告, San Jose, CA, 2002.
- [4] Jae-Woo Chang and Du-Seok. 用于数据挖掘应用中大型高维数据的基于单元格的方法. 见 Proceedings of the 2002 ACM Symposium on Applied Computing, SAC '02, pages 503–507.
- [5] Yixin Chen and Li Tu. 用于实时流式数据的基于密度的聚类. 见 Proceedings of 13th ACM SIGKDD International Conference on Knowledge Discovery and Data Mining, KDD '07, pages 133–142.
- [6] Chun-Hung Cheng, Ada Wai, and Fu Yi. ENCLUS: 基于熵的数值数据子空间聚类. 见 Proceedings of ACM SIGKDD International Conference on Knowledge Discovery and Data Mining, (KDD-99), 1999.
- [7] Martin Ester, Hans-Peter Kiel, Josef Star, and Xiaowe Xu. 一种带噪声的大型空间数据库聚类发现的基于密度算法. 见 KDD'96, pages 226–231.
- [8] Jin Gao, Jianhong Li, Zhaotong Zhang, and Pang-Ming Tan. 一种基于密集单元的增量聚类算法. 见 Proceedings of 9th Pacific-Asia Conference on Advances in Knowledge Discovery and Data Mining, PAKDD’05, pages 420–425, Berlin, Heidelberg, Springer-Verlag.
- [9] Peter Grabachev and Arkady Borisov. 分类中的网格聚类方法. 见 Proceedings of the International Conference on Parallel Computing in Electrical Engineering, pages 425–426.
- [10] Chaojun Ma, Guojan Jan, and Jianhong Wu. 数据聚类：理论、算法与应用. SIAM, 2007.
- [11] Alexander Hinneburg and Daniel A. Keim. 一种带噪声的大型媒体聚类方法. 见 Proceedings of the 4th International Conference on Knowledge Discovery and Data Mining, pages 58–65. AAAI Press.
- [12] Alexander Hinneburg and Daniel A. Keim. 最优网格聚类：迈向打破高维聚类的维度诅咒. 见 VLDB’99, pages 506–517. Springer Kaufmann, 1999.
- [13] Klaus Heinrich. 网格文件系统：应用的实现与案例研究. 技术报告, ETH Zurich, 1985.
- [14] M.R. Liao and V. Mohan. 基于网格的算法综述. International Journal of Engineering Science and Technology, 2(8):3441–3446, 2010.
- [15] Wei-liang Liao, Ying Liu, and Al Choudhury. 使用自适应网格划分的基于网格的聚类算法，2004.
- [16] Nancy P. Lin, Chun-I Chang, Nien-yi Yan, Hao-En Chen, Hung-Jen Chen, and Wei-Hua Hao. 一种自适应分治聚类算法. 见 Proceedings of the 6th International Conference on Applied Computer Science–Volume 6, A’07, pages 155–159, 2007.
- [17] Nancy P. Lin, Chun-I Chang, Nien-yi Yan, Hao-En Chen, Hung-Jen Chen, and Wei-Hua Hao. 一种偏移交叉聚类算法. WTOS, 7(3):175–184, 2008.
- [18] Eden W.M. Ma and Tony W.S. Chow. 一种新的网格聚类算法. Pattern Recognition, 37(3):503–514, 2004.
- [19] S Mahran and K. Mahar. 使用网格加速基于密度的聚类. 见 8th IEEE International Conference on Computer and Information Technology, pages 35–40, 2008.
- [20] B. Milova and Marcos Campos. O-cluster: 大维度集合的可扩展聚类. 见 Proceedings of the IEEE International Conference on Data Mining, pages 290–297.
- [21] H. Hages, S. Goil, and A. Choudhury. 用于大型数据集的高效可扩展子空间聚类, 技术报告 CPDC-RR-9901 Center for Parallel and Distributed Computing.
- [22] Nam Hun Park and Won Suk Lee. 基于流数据的统计基于网格聚类. SIGMOD Record, 33(1):32–37, 2004.
- [23] Abdol Hamid Pilevar and M. Sukumar. GCHL: 用于大型空间数据的网格聚类算法. Pattern Recognition Letters, 26(7): 9–10.
- [24] Rakesh Agrawal, Johannes Gehrke, Dimitrios Gunupulos, and Prabhakar Raghavan. 用于数据挖掘应用的高维数据自动聚类. 见 Proceedings of the 1998 ACM SIGMOD International Conference on Management of Data, SIGMOD '98, pages 94–105, New York, USA, ACM.
- [25] Mounir Bechini, Angel Goglin, Guillaume Rasche, and Noureddine Mouaddib. 模糊结果的多维基于网格的聚类. 研究报告, INRIA, 2008. DOI: https://hal-archives.archives.fr/hal-00034654/en
- [26] Pavel Berkhin. 数据挖掘技术综述. 技术报告, San Jose, CA, 2002.
- [27] Jae-Woo Chang and Du-Seok. 用于数据挖掘应用中大型高维数据的基于单元格的方法. 见 Proceedings of 2002 ACM Symposium on Applied Computing, SAC '02, pages 503–507.
- [28] Yixin Chen and Li Tu. 用于实时流式数据的基于密度的聚类. 见 Proceedings of 13th ACM SIGKDD International Conference on Knowledge Discovery and Data Mining, KDD '07, pages 133–142.
- [29] Chun-Hung Cheng, Ada Wai, and Fu Yi. ENCLUS: 基于熵的数值数据子空间聚类. 见 Proceedings of ACM SIGKDD International Conference on Knowledge Discovery and Data Mining, (KDD-99), 1999.
- [30] Martin Ester, Hans-Peter Kiel, Josef Star, and Xiaowe Xu. 一种带噪声的大型空间数据库聚类发现的基于密度算法. 见 KDD'96, pages 226–231.
- [31] Jin Gao, Jianhong Li, Zhaotong Zhang, and Pang-Ming Tan. 一种基于密集单元的增量聚类算法. 见 Proceedings of 9th Pacific-Asia Conference on Advances in Knowledge Discovery and Data Mining, PAKDD’05, pages 420–425, Berlin, Heidelberg, Springer-Verlag.
- [32] Peter Grabachev and Arkady Borisov. 分类中的网格聚类方法. 见 Proceedings of the International Conference on Parallel Computing in Electrical Engineering, pages 425–426.
- [33] Chaojun Ma, Guojan Jan, and Jianhong Wu. 数据聚类：理论、算法与应用. SIAM, 2007.
- [34] Alexander Hinneburg and Daniel A. Keim. 一种带噪声的大型媒体聚类方法. 见 Proceedings of the 4th International Conference on Knowledge Discovery and Data Mining, pages 58–65. AAAI Press.
- [35] Alexander Hinneburg and Daniel A. Keim. 最优网格聚类：迈向打破高维聚类的维度诅咒. 见 VLDB’99, pages 506–517. Springer Kaufmann, 1999.
- [36] Klaus Heinrich. 网格文件系统：应用的实现与案例研究. 技术报告, ETH Zurich, 1985.
- [37] M.R. Liao and V. Mohan. 基于网格的算法综述. International Journal of Engineering Science and Technology, 2(8):3441–3446, 2010.
- [38] Wei-liang Liao, Ying Liu, and Al Choudhury. 使用自适应网格划分的基于网格的聚类算法，2004.
- [39] Nancy P. Lin, Chun-I Chang, Nien-yi Yan, Hao-En Chen, Hung-Jen Chen, and Wei-Hua Hao. 一种自适应分治聚类算法. 见 Proceedings of the 6th International Conference on Applied Computer Science–Volume 6, A’07, pages 155–159, 2007.
- [40] Nancy P. Lin, Chun-I Chang, Nien-yi Yan, Hao-En Chen, Hung-Jen Chen, and Wei-Hua Hao. 一种偏移交叉聚类算法. WTOS, 7(3):175–184, 2008.
- [41] Eden W.M. Ma and Tony W.S. Chow. 一种新的网格聚类算法. Pattern Recognition, 37(3):503–514, 2004.
- [42] S Mahran and K. Mahar. 使用网格加速基于密度的聚类. 见 8th IEEE International Conference on Computer and Information Technology, pages 35–40, 2008.
- [43] B. Milova and Marcos Campos. O-cluster: 大维度集合的可扩展聚类. 见 Proceedings of the IEEE International Conference on Data Mining, pages 290–297.
- [44] H. Hages, S. Goil, and A. Choudhury. 用于大型数据集的高效可扩展子空间聚类, 技术报告 CPDC-RR-9901 Center for Parallel and Distributed Computing.
- [45] Nam Hun Park and Won Suk Lee. 基于流数据的统计基于网格聚类. SIGMOD Record, 33(1):32–37, 2004.
- [46] Abdol Hamid Pilevar and M. Sukumar. GCHL: 用于大型空间数据的网格聚类算法. Pattern Recognition Letters, 26(7): 9–10.

## 第 7 章：非负矩阵分解用于聚类

### 7.1 引言

非负矩阵分解（`NMF`）是一种强大的技术，用于将非负矩阵 `V` 分解为积 `WH`，其中 `W` 和 `H` 都是非负矩阵。该方法在各个领域（包括聚类）受到了广泛关注，是因为其非负约束产生了一种比主成分分析（`PCA`）更具解释性的表示。

### 7.2 NMF 公式

`NMF` 问题通常被建模为一个约束优化问题：
$$\min_{W,H \ge 0} f(V, WH)$$
其中 `f(V, WH)` 是衡量原始数据与其近似之间距离的代价函数。常用的代价函数包括：

- **欧式距离**: `f(V, WH) = 1/2 ||V - WH||_F^2`
- **KL 散度**: `f(V, WH) = Σ_{i,j} (V_{ij} log V_{ij}/(WH)_{ij} - V_{ij} + (WH)_{ij})`
- **L1 范数**: `f(V, WH) = Σ_{i,j} |V_{ij} - (WH)_{ij}|`

`NMF` 问题通常使用迭代算法求解，例如乘法更新规则、坐标下降或替代最小二乘法。

### 7.3 NMF 聚类能力

一旦获得了矩阵 `W` 和 `H`，就可以通过将样本分配给一个或多个聚类来执行聚类。由于 `H_{ij}` 表示样本 `j` 属于聚类 `i` 的程度，可以采用几种聚类策略：

- **硬聚类**: 每个样本 `j` 恰好分配到一个聚类。我们将样本 `j` 分配给 `H_{ij}` 中值最大的聚类 `i`：`c_j = argmax_i H_{ij}`。
- **软聚类**: 每个样本 `j` 分配给所有聚类，权重由 `H_{ij}`。这对于可能属于多个聚类的数据有用。
- **阈值法**: 将样本分配给 `H_{ij}` 超过特定阈值的聚类。

基于 `NMF` 的聚类对于高维稀疏数据（例如文本文档或图像数据）特别有效，其中非负约束有助于有效地捕捉潜在结构。

### 7.1 引言

最近，非负矩阵分解（`NMF`）在各种聚类任务中的应用取得了显著进展。`NMF` 将一个输入矩阵分解为两个低秩的非负矩阵。虽然 `NMF` 可以用于传统的数据分析，但近期人们对 `NMF` 表现出的极大兴趣源于新发现的 `NMF` 在解决聚类数据挖掘和机器学习问题方面的优势。特别是，使用均平方误差作为成本函数的 `NMF` 等同于松弛的 `K-means` 聚类，这是应用最广泛的无监督学习算法。此外，使用 `I` 散度作为成本函数的 `NMF` 等同于概率隐语义索引等。本章旨在对用于聚类的矩阵因子分解方法进行全面的综述。我们概述了基于 `NMF` 聚类的理论基础，提供了 `NMF` 各种不同变体的概述，并探讨了 `NMF` 算法中的若干实际问题。我们还总结了近期使用基于 `NMF` 方法解决许多其他聚类问题（包括协同聚类、监督聚类和共识聚类）的进展，并讨论了某些未来的研究方向。

### 7.1.1 背景

`NMF` 最初是为了矩阵因子的“部分与整体”解释而提出的，它吸引了大量的关注，并被证明在各种应用场景和环境中是有用的 [88]，如化学计量学 [128]、模式识别 [70]、多媒体数据分析 [26]、文本挖掘 [130, 91]、文档摘要 [89, 118]、DNA基因表达分析 [11]、金融数据分析 [43]以及社交网络分析 [128, 13, 19]。`NMF` 可以追溯到20世纪70年代（见 [6] 中的笔记），并由 `Paatero` 和 `Tapper` [38] 广泛研究。`Lee` 和 `Seung` [67] 的工作使 `NMF` 在机器学习和数据挖掘领域受到了广泛。`NMF` 的算法扩展已适应各种目标函数 [29] 和各种数据分析问题，包括分类 [71] 和协同过滤 [106]。许多研究专注于 `NMF` 的进一步计算方法。此外，学者们还提出了 `NMF` 的各种扩展和变体，以及 `NMF` 是 NP 硬的复杂性问题 [56, 7, 37, 39, 111, 95, 113, 38]。

然而，`NMF` 的真正威力在于它解决具有挑战性的数据挖掘和模式识别问题的能力。事实上，已经证明 [35, 37] 使用均平方误差作为成本函数的 `NMF` 等同于松弛的 `K-means` 聚类，这是应用最广泛的无监督学习算法。此外，使用 `I` 散度作为成本函数的 `NMF` 等同于概率隐语义索引，另一种在文本分析中常用的无监督学习方法。得益于聚类能力，`NMF` 近期在数据挖掘领域引起了大量关注。

在本章中，我们对矩阵因子分解方法提供了全面的综述。为了适应数据挖掘领域更广泛的读者，我们的综述更多地关注概念基础和解释，而不是详细的推导。然而，需要提醒读者，`NMF` 是一个如此巨大的领域，真正全面的综述几乎是不可能的，因此我们的综述可能有些杂杂。鼓励感兴趣的读者查阅其他论文以进一步阅读。读者还应该注意，在我们的介绍中，许多数学描述经过了修改以适应数据挖掘问题。

本章的其余部分结构如下：7.1 节的剩余部分介绍了 `NMF` 的基本公式；7.2 节概述了基于 `NMF` 聚类的理论基础，并展示了 `NMF` 与各种聚类方法之间的等价结果；7.3 节演示了 `NMF` 的聚类能力并分析了 `NMF` 在聚类分析中的优势；7.4 节提供了 `NMF` 算法发展的概述，并讨论了 `NMF` 算法中的实际问题；7.5 节提供了许多不同 `NMF` 变体的概述；7.6 节总结了近期使用基于 `NMF` 的方法解决许多其他聚类问题（包括协同聚类、监督聚类和共识聚类）的进展。最后，7.7 节总结了本章并讨论了未来的研究方向。

### 7.1.2 NMF 公式

设输入数据 `X = (x_1, …, x_n)` 包含 `n` 个数据列向量集合。我们将 `X` 分解为两个：

$$X ≈ FG^T,$$

其中 `X ∈ R^{p × n}, F ∈ R^{p × k}`, 且 `G ∈ R^{n × k}`。通常，`p < n` 且 `F, G` 的秩远低于 `X` 的秩，即 `k < min(p, n)`。`F, G` 通过最小化一个成本函数得到。

$$\min_{F,G ≥ 0} J_{Sse} = ||X - FG^T||^2.$$

在本章中，隐式假设范数是 Frobenius 范数。假设 `F, G` 满足秩非递减条件。另一种成本函数是所谓的 `I` 散度：

$$\min_{F,G ≥ 0} J_{do} = Σ_{i=1}^n [ X_{ij} log X_{ij}/(FG^T)_{ij} - X_{ij} + (FG^T)_{ij} ].$$

很容易证明当 `x=1` 时，不等式 `I(x) ≥ 0` 成立。量 `I(u,v) = u log(u/v) - u + v` 被称为 `I` 散度。

## 7.2 用于聚类的 NMF：理论基础

虽然 `NMF` 可以用于传统的数据分析，但近期对 `NMF` 的极度兴趣源于新发现的 `NMF` 在解决聚类数据挖掘和机器学习问题方面的优势。在这里我们概述：
- (1) `NMF` 与 `K-means` 的关系
- (2) `NMF` 与 `I` 散度的关系
- (3) `NMF` 与谱类的关系

### 7.2.1 NMF 与 K-means

`K-means` 算法是 Logic常用的方法之一。设 `X = (x_1, …, x_n)` 为数据。我们将它们分为 `K` 个类。`K-means` 目标写为：

$$J_{means} = Σ_{i=1}^n Σ_{k=1}^K h_{ik} ||x_i - μ_k||^2,$$

其中当 `x_i` 属于第 `k` 类时，`h_{ik}=1`，否则为 0。`μ_k` 是第 `k` 类的质心。这可以重写为：

$$J_{means} = Σ_{i=1}^n ||x_i - Σ_{k=1}^K h_{ik} μ_k||^2.$$

### 7.2.2 NMF 与概率语义索引

概率隐语义索引（`PLSI`）是一种基于统计模型的无监督学习方法，并已成功应用于文档聚类。`PLSI` 最大化似然：

$$J_{PLSI} = Σ_{i=1}^n Σ_{j=1}^m X_{ij} log P(w_i, d_j),$$

其中联合发生概率分解为：

$$P(w_i, d_j) = Σ_k P(w_i|z_k)P(d_j|z_k)P(z_k),$$

假设给定 `z_k` 时，`w_i` 和 `d_j` 条件独立。

定理 2 `PLSI` 等于使用 `I` 散度的 `NMF`。
(A) `PLSI` 的目标函数与使用 `I` 散度的 `NMF` 目标函数等同。
(B) 我们可以将 `FG^T` 表示为 `F D̂ G^T`，其中 `F, D̂, G^T` 满足概率归一化：`Σ_{i=1}^n F_{ik}=1, Σ_{j=1}^m G_{jk}=1, Σ_{k=1}^k D̂_{kk}=1`。

### 7.2.3 用于谱聚类的 NMF 与核 K-means

对于对称矩阵 `W`，期望得到 `W ≈ HH^T` 分解。以下定理指出其在文档聚类中的用处：

定理 3 正交对称 `NMF`
$$\min_{H≥0} ||W - HH^T||^2, \text{s.t.} } H^T H = I.$$

等同于核 `K-means` 聚类。

# 用于聚类的非负矩阵分解：综述

研究还表明，对称矩阵分解作为非负矩阵分解的一种特例，等价于复杂的归一化切分聚类 [100]。给定图的邻接矩阵 `W`，可以很容易看出下面的矩阵分解

```
