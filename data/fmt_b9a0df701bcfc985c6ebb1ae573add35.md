
与连续序列的情况一样，挑战在于数据对象之间创建相似性函数。在这种情况下，通常使用`Hamming distance`、`编辑距离`和最长公共子序列等相似性函数。关于用于离散序列的相似性函数的讨论可以参见 [58]。离散序列聚类背景下出现的另一个关键问题是，一组序列的中间表示和摘要表示在计算上可能是密集型的。对于可以使用平均方法的数值数据，要为离散序列找到此类表示要困难得多。一种提供相对均衡匹配水平的常用表示是`后缀树`。`CLUSE`[85] 中提出了使用后缀树进行聚类的方法。

生成模型可用于模拟序列之间的距离并创建聚类聚合的概率模型 [76]。一种特别常用的方法是使用隐马尔可夫模型（`HMMs`）。关于隐马尔可夫模型的入门介绍可以参见 [70]。隐马尔可夫模型可用于生成一种特殊的混合混合，其中模型的不同组件之间相互依赖。第二层混合建模可以从这些不同的 `HMM` 创建聚类。序列聚类的大部分工作是在生物学数据背景下进行的。关于该主题的详细调查可以参见 [33, 49, 64]。第 16 章提供了序列算法的讨论，尽管本章提供了其他类型生物数据聚类算法的综述。

## 1.3.6 聚类网络数据

图和网络是所有数据表示中最基础（最通用）的。这是因为每个数据点都可以表示为相似图，边上带有相似性值。事实上，谱聚类（`spectral clustering`）方法可以看作所有类型聚类与图聚类之间最通用的连接。然而，只要可以在任意数据对象之间定义相似性函数，就可以使用谱聚类来进行分析。图聚类在经典文献中已广泛研究，特别是在二分图和多路图划分的背景下。所有多路划分算法中最经典的是 `Kernigh-Lin` 方法 [56]。此类方法可以与图粗化方法结合，提供高效的解决方案。此类方法被称为多级划分技术。该类别中一种特别受欢迎的算法是 `METIS` [53]。

文献中常用多种方法来从图中创建划分：

- *生成模型（Generative Models）*：如本章所述，只要存在适当的方法将混合的每个组件定义为概率分布，就可以为几乎任何聚类问题定义生成模型。生成模型的示例可以在 [77] 中找到。
- *经典组合算法（Classical Combinatorial Algorithms）*：这些方法使用网络流 [13] 或迭代组合技术从底层图创建划分。应该指出，即使是贪心算法，在重复多次后，通常也被认为可以创建高质量的划分 [51]。确定哪些划分在不同划分之间是良好平衡的理想的，因为绝对值最小的切分（cut）通常包含单个划分和其他剩余划分中的大部分节点。在创建划分方面，不同类型的目标函数，如不均划分（unequal cut）、归一化划分（normalized cut）和比例划分（ratio cut），在聚类平衡和解的质量之间提供了不同的权衡 [73]。应该指出，由于划分是一个组合优化问题，它们可以被建模为整数规划。
- *谱方法（Spectral Methods）*：谱方法可以看作是代表图划分优化整数规划的线性规划松弛。可以为不同类型的划分构建不同的目标函数，例如未归一化划分、比例划分和归一化划分。因此，这些线性规划的连续解可以用于为节点创建多维嵌入，并在其基础上应用传统的 `k-means` 算法。可以证明这些线性规划采取特别方便的形式，其中图拉普拉斯矩阵（`graph Laplacian`）的广义特征向量对应于优化问题的解。
- *非负矩阵分解（Nonnegative Matrix Factorization）*：由于图可以表示为邻接矩阵，非负矩阵分解可用于将其分解为低秩矩阵。可以将矩阵分解方法应用于节点-节点邻接矩阵或节点-边邻接矩阵，以获得不同的见解。也可以容易地结合技术和结构来增强矩阵 [69]。虽然上述方法代表了重要聚类方法的采样，但许多其他目标函数可以用于基于模块化的（modularity-based）图切划分 [24]。此外，在社交网络背景下，问题变得更具挑战性，内容可能既不在节点也不在边上。关于网络聚类的调查可以发现 [36, 72]。第 17 章讨论了网络聚类算法。

# 聚类分析简介

用于监督聚类过程。例如，一种非常简单的监督形式是使用种子点（seeding），将相应类别的文档作为（某些）种子提供给如 `k-means` 等代表性聚类算法。近年来，谱方法也被大量应用于半监督聚类问题。在这些方法中，对标签进行拉普拉斯平滑（`Laplacian smoothing`）以生成聚类。这允许以半监督的方式学习低维数据表面，因为它与底层聚类相关。半监督聚类领域有时也被称为受限聚类（constrained clustering）。第 20 章可能对半监督聚类的受限算法进行很好的讨论，并特别关注基于图的算法。

## 1.4.3 多视图和基于集合的见解

如上所述，聚类过程中的主要问题之一是可能存在不同类型的类。在没有监督的情况下，聚类过程中数不眼花的可能性有时会给分析师带来困扰，特别是从解释性的角度来看。这些被称为备选聚类（alternative clusters），在技术上代表了不同视角的行为。在许多情况下，提供显著不同的不同聚类方案可以为分析师提供关于底层数据关键聚类属性的见解。这一领域也被称为多视图聚类（multiew clustering）。

多次聚类的最简单方法是简单多次运行聚类算法，然后检查不同的聚类方案以确定哪些是不同的。另一种不同的方法是使用谱方法来创建近似正交的划分（orthogonal cuts）。记住，拉普拉斯矩阵的特征向量代表图中的备选划分，而最小的特征代表最好的。因此，通过使用 2-means 算法嵌入每个编码器，可以创建一个与其它（正交）特征向量创建的聚类不同的聚类。特征向量的正交性非常重要，因为它意味着嵌入的表示非常不同。此外，最小的特征向量代表最好的聚类，而与后续逐渐较大的特征向量不同的聚类则代表了逐渐次优的解决方案。因此，这种方法不仅提供了彼此之间截然不同的备选聚类，还对不同方案的质量提供了排名。第 21 章提供了对备选方法的讨论。

在许多情况下，可以将不同的备选聚类方法结合，使用基于集合的技术（ensemble-based techniques）来创建更稳健的解决方案。其想法是，不同聚类的输出组合可以提供关于属性之间相互关系的更稳健的视图。不同备选方案的输出可以用元算法（meta-algorithm）的输入，以组合来自不同算法的结果。这种方法提供了一种更稳健的聚类解决方案。第 22 章提供了基于集合的聚类方法的讨论。

## 1.4.4 基于验证的见解

给定一个特定的聚类，我们如何知道聚类的质量究竟如何？虽然一种可能的方法是使用合成数据来确定输入和输出聚类之间的匹配，但仅依赖合成数据并不完全令人满意。结果是，合成数据可能特定于某种算法，可能无法容易推广到任意数据。

因此，在真实数据集的基础上使用验证标准是理想的。在聚类问题的背景下，质量标准不像许多其他数据问题（如分类）那样清晰，因为在分类中，外部验证标准可以以标签的形式备用。因此，使用一个或多个标准可能会在无意中偏向不同的算法。正如接文讨论所暗示的，聚类是一个由于其无监督的性质而往往无法进行量化的过程。尽管如此，许多技术对底层结构提供了部分理解。一些常用的聚类验证技术如下：

- 文献中的常用方法是使用案例研究来说说明类的主观质量。虽然案例研究提供了直观的见解，但它们对于提供更严谨的质量量化并不有效。使用这种方法通常很难从定量角度比较两种聚类方法。
- 聚类的特定测量值（如聚类半径或密度）可用于提供质量衡量。这里的问题是，这些衡量可能会以不同的方式偏向不同的算法。例如，`k-means` 方法在平均聚类半径方面通常优于基于密度的聚类方法，而基于密度的方法在估计聚类密度方面可能优于 `k-means` 算法。这是因为当使用同一标准进行聚类目的时，存在循环逻辑。这在评估过程中会导致偏差。另一方面，可能基于特定的聚类合理地比较类型非常的算法（例如 `k-means` 的两种变体）。
- 在许多数据集中，标签与数据点相关。在这种情况下，可以通过聚类与数据标签之间的相关性来衡量聚类质量。如果标签没有在聚类过程中被使用，这提供了一个外部验证标准。然而，这种方法并不是完美的，因为类别标签并不总是与数据中的自然聚类对齐。尽管如此，这种方法仍被认为比上述讨论的两种方法更“公正”。并常用于聚类评估。

第 23 章提供了对聚类算法常用的验证方法的详细讨论。

## 1.5 讨论与结论

聚类是数据挖掘的最基础问题之一，因为其在客户细分、目标营销和数据摘要方面广泛的应用。文献中提出了许多类方法，例如概率方法、基于距离的方法、基于网格的方法和谱方法。聚类问题与降维之间有密切的关系，特别是通过投影聚类。高维数据由于数据数量的增加通常具有挑战性。流式方法通常只对数据进行一次扫描。聚类的许多变体和改进可以用于提高聚类过程中获得的质量。数据类型的多样性增加了聚类问题的丰富性。

# 数据聚类：算法与应用

- [18] S. Basu, I. Davidson, and K. Wagstaff. 约束聚类：理论进展、算法与应用, *Chapman and Hall*, 2008.
- [19] M. Belkin and P. Niyogi. 用于降维和数据表示的拉普拉斯特征映射, *Neural Computation*, 15(6), 2003.
- [20] P. Perkin. 聚类挖掘技术综述. 多维数据分组, 25–71, 2006.
- [21] K. Beyer, J. Goldstein, U. Shaft, and R. Ramakrishnan. 近邻在何时是有意义的？*ICDT Conference*, 2001.
- [22] D. Blei, A. Ng, and M. Jordan. 隐狄利利克分配, *Journal of Machine Learning Research*, 3993–1022, 2003.
- [23] K. Chakrabrabarti and S. Mehrotra. 局部降维：高维空间索引的新方法. *VLDB Conference Proceedings*, 89–100, 2004.
- [24] A. Clauset, M. E. J. Newman, and C. Moore, 大型网络中的社区结构发现, *Physical Review* 70:066111, 2004.
- [25] D. Cutting, K. Jarger, and J. Tukey. 散布/聚集：一种基于聚类的大文档集浏览方法. *ACM SIGIR Conference*, 318–329, 1992.
- [26] R. Cordeiro, C. Traina Jr., A. Traaina, J. López, U. Kang, and C. Faloutsos. 层次聚类超大规模多维数据集. *KDD* 690–698, 2011.
- [27] A. P. Dempster, N. M. Laird, and D. B. Rubin. 通过EM算法从不完整数据中获得极大似然, *Journal of the Royal Statistical Society, B*, 39(1):1–38, 1977.
- [28] J. Dean and S. Ghehemwat. MapReduce: 一种灵活的数据处理技术, *Communication of the ACM*, 53:72–77, 2010.
- [29] I. Dhillon. 使用二分谱图划分文档和单词进行共聚类, *ACM KDD Conference*, 2001.
- [30] I. Dhillon, S. Mallela, and D. Modha. 信息论共聚类, *ACM KDD Conference*, 2003.
- [31] B. Duran. 聚类分析：综述. *Springer-Verlag*, 1974.
- [32] G. Das and H. Mannila. 类别数据库的基于相似性量. *PKDD Conference*, 201–210, 2000.
- [33] M. B. Eisen, P. T. Spellman, P. O. Brown, and D. Botstein. 基因组范围表达模式的聚类分析与展示. *Proceedings of the National Academy of Sciences*, 95(25):14863–14868, 1998. http://www.nlm.nih.gov/EisenSoftware.html
- [34] M. Ester, H.-P. Kriegel, J. Sander, and X. Xu. 一种用于带噪声的大型空间数据库聚类的基于密度算法. *ACM KDD Conference*, 226–231, 1996.
- [35] M. Filippone, F. Casara, F. Masulli, and S. Rovetta. 聚类核与谱方法综述. *Pattern Recognition*, 41(1):176–190, 2008.
- [36] S. Fortunato. 图中的社区检测, *Physics Reports*, 48(3–5):75–174, 2010.

# 聚类分析导论

- [37] G. Gan, C. Ma, and J. Wu. 数据聚类：理论、算法与应用. *SIAM, Society for Industrial and Applied Mathematics*.
- [38] V. Ganti, G. Jehrke, and R. Ramakrishnan. 使用摘要对类别数据进行聚类. *ACM KDD*, 1999.
- [39] D. Gibson, J. Kleberg, and P. Raghav. 类别数据聚类：基于动态系统的方法. *VLDB Conference*, 1998.
- [40] S. Guha, R. Rastogi, and K. Shim. ROCK: 用于数据的鲁棒聚类算法. *Information Systems*, 25(5):345–366, 2000.
- [41] S. Guha, R. Rastogi, and K. Shim. SURE: 用于大型数据库的高效聚类算法. *ACM SIGMOD*, 1998.
- [42] D. Gunopulos and G. Das. 时间序列相似性量与时间序列索引, *ACM SIGMOD Conference*, 2001.
- [43] A. Hin, C. Aggarwal, and D. Keim. 高维空间中的最近邻. *VLDB Conference*, 2000.
- [44] A. Hin, D. Keim, and M. Wawnik. 高维数据的视觉化挖掘. *Computer Graphics and Applications*, 19:22–31, 1999.
- [45] T. Hofmann. 概率隐索引. *ACM SIGIR Conference*, 1999.
- [46] A. Jain. 数据聚类：50年回顾. *Pattern Recognition*, 31(8):651–666, 2010.
- [47] A. Jain and R. Dubes. 聚类算法. *Prentice Hall*, 1988.
- [48] A. Jain, M. Murty, and P. Flynn. 数据聚类：综述. *ACM Computing Surveys (CSUR)*, 31(3):264–323, 1999.
- [49] D. Jiang, C. Tang, and A. Zhang. 基因表达数据聚类, *IEEE Transactions on Knowledge Discovery from Data (TKDD)*, 16(11):1370–1386, 2004.
- [50] I. Lilleosse. 主成分分析, *Springer*, 2002.
- [51] D. R. Karger. 流量中的随机采样, *STOC*, 648–657, 1994.
- [52] L. Kaufman and P. Rousseeuw. 数据中的分组：聚类分析导论. *Wiley-Interscience*, 2005.
- [53] G. Kawasaki and V. Kumar. 不规则图的多级k路划分. *Journal of Parallel and Distributed Computing*, 48(1):96–129, 1998.
- [54] H.-P. Kriegel, P. Kaiser, and A. Zimek. 高维数据聚类：子空间聚类、模式聚类与相关性综述. *ACM Transactions on Knowledge Discovery from Data (TKDD)*, 3(1):1–58, 2009.
- [55] D. D. Lee and H. S. Seung. 通过非负矩阵分解学习对象的部分, *Nature*, 401:788–791, 1999.
- [56] B. W. Kernighan and S. Lin. 图划分的高效启发式程序, *Bell Sys. Journal*, 49:291–307, 1970.

# 数据聚类：算法与应用

- [57] C. Ding, X. He, and H. Simon. 关于非负矩阵分解与谱聚类的等效性. *SDM Conference*, 2005.
- [58] D. Gusfield. 字符串、树与序列算法, *Cambridge University Press*, 1997.
- [59] J-G. Lee, J. Han, and K.-Y. Wang. 轨迹聚类：一种划分与分组框架, *SIGMOD Conference*, 593–604, 2007.
- [60] T. Liao. 时间序列数据聚类——综述. *Pattern Recognition*, 38(11):1857–1874, 2005.
- [61] H. Liu and H. Motoda. 特征选择计算方法, *Chapman and Hall (CRC Press)*, 2007.
- [62] L. Liu, R. Jin, C. Aggarwal, and Y. Shen. 不确定图上的可靠聚类, *ICDM Conference*, 2012.
