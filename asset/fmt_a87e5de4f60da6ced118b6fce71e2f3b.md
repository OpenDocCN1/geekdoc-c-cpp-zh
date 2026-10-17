
我们注意到，在静态情况下，也可以添加一个背景聚类以提高估计过程的稳健性。然而，在数据流中这是不可行的，因为背景集合模型可能需要多次遍历才能有效构建。[48] 中的工作通过使用具有衰减函数属性的聚类配置（cluster profile），以在线方式维持了这些属性。我们注意到，聚类配置类似于 [12] 中引入的凝结液滴概念。核心算法（`OCTS`）是维护一个动态聚类集，通过使用相似性计算将文档逐渐分配到这些聚类中。[48] 已经展示了如何高效地利用聚类配置为每个迁入的文档计算 `$p(d|C_j)$`。该值随后被用于确定与不同聚类的相似性，并将文档分配到其最最近的聚类中。我们注意到，[12] 中的方法在以下方面具有许多相似之处：(a) 聚类配置的维护；(b) 使用聚类配置（或凝结液滴）计算相似性并将文档分配到最相似的聚类；以及 (c) 用于决定何时创建新的单例聚类或替换旧聚类的规则。

两种算法之间的主要区别在于计算聚类相似性的技术。`OCTS` 算法使用概率计算 `$p(d|C_j)$` 来计算聚类相似性，它在计算过程中考虑了相位信息。关于 `OCTS` 的一个观察是，它允许非常相似的聚类在当前集合中共存。这减少了不同聚类的空间。[48] 中还提出了另一种算法 `OCTM`，它允许合并非常相似的聚类。在每次分配之前，它会检查相似聚类对是否可以根据相似性进行合并。如果是，则允许这些聚类及其相应的聚类配置进行合并。[48] 中给出了关于不同聚类算法及其有效性的详细实验结果。关于文本聚类算法的全面综述可以在 [15] 的数据聚类和流算法章节中找到。

## 10.8 流聚类的其他场景

数据流聚类是一个基础性问题，并且出现了其他领域，在这些领域中数据自然出现在流式背景下。在本节中，我们将对这些不同的数据领域进行简要介绍，并提供相关文献索引。

# 流聚类算法综述

### 10.8.1 不确定数据流的聚类

不确定数据经常出现在传感器数据或其他硬件技术（如 RFID）的文中，当数据收集过程中存在显著误差时。在许多此类情况下，数据中的误差可以以统计参数（如标准差）或概率密度函数（pdfs）的形式进行近似。统计信息增加了噪声数据的丰富性，并提供了关于数据中可靠性较低部分的信息，因此在挖掘过程中应该对其予以强调。

在此背景下，[13] 提出了一种名为 `UMicro` 的方法用于对不确定数据流进行聚类。该方法通过增加关于聚类中数据点不确定性的额外信息来增强微簇（microclusters）。这些信息被用于提高分配时距离函数的质量。这种方法在不确定数据流的投影聚类案例中 [4, 60] 得到了进一步改进。我们在这里不对这些方法进行详细讨论，这些方法将在章节的后续关于不确定数据聚类的部分进行讨论。

### 10.8.2 图流的聚类

图流是由许多社交和信息网络中以边为中心的活动创建的。取决于应用场景，存在许多不同类型的流和聚类模型。这些不同模型如下：

- 流是一个对象序列，每个对象都是一个包含节点和边子集的小图。我们希望通过节点和边之间的相似性来确定流中的相似对象。例如，DBLP 题文献网络有一个对应于作者论文的迁入图流。确定具有相似结构的对象聚类可能是有意义的。[14] 提出了一种解决该问题的算法，称为 `Gmicro`。微聚类表示被扩展以处理边，并在边上使用草图压缩（sketch compression）以减少海量边密度的影响。

- 流是一个对象序列，每个对象都是一个包含节点和边子集的小图。我们希望确定在这些对象中频繁共同出现且相互紧密连接的节点集。[8] 提出了一种使用 `minhash` 图流摘要的方法。

- 流是对象或边的序列。目标是确定图中的稠密节点聚类。

该问题具有特别的通用性，并且与动态社区检测问题相关。在此背景下，提出了一种利用边流的结构化蓄水采样 [16] 创建图动态模式的方法。[19] 中的工作旨在检测离群值，该过程的关键步骤是从边流中动态生成节点聚类。[28] 中的工作进一步完善了 [16] 的结构化蓄水采样技术，以便为图流中的节点聚类提供更有效的方法。

在许多情况下（如社交网络），内容信息与网络结构相关联。例如，Twitter 流中的推文既有结构又有内容。这些被称为社交流。此类流的聚类需要同时使用结构信息和文本内容。[9] 中的工作设计了聚类社交流的方法。基于草图（Sketch-based）的方法用于总结社交流中的内容并将其用于聚类过程。此外，[9] 显示了这种方法如何用于事件检测。

在传统的流模型中，假设允许对数据进行一次遍历，且可用内存是有限的。[19] 提出了一种在弱流模型中确定稠密子图的技术，在该模型中允许多次遍历，内存量与输入大小无关（常数）。这种方法能够随图的大小呈对数级增长。

### 10.8.3 数据流的分布式聚类

在传感器网络的背景下，数据流仅在分布式设置中可用，对数据聚类的一种自然方法是将所有数据传输到中央服务器。不幸，由于必须传输的数据量巨大，这种方法在成本上非常昂贵。因此，设计一种能够减少不同处理器之间通信成本的方法至关重要。[27] 提出了一种在每个节点上进行局部聚类并将这些聚类合并为单一聚类的方法。该方法的一个引人特征是对聚类质量提出了一个近似界。[27] 提出的另一种分布式聚类方法是并行猜测算法。

针对数据流聚类还存在许多方法。例如，[61] 提出了一种使用 `k-means` 方法的分布式数据聚类技术。[57] 中找到另一种通过维护在线离散化来降低维度和通信成本的流聚类方法。最后，[66] 提出了一种使用 `EM` 方法的数据流聚聚类。

## 流数据聚类算法综述

异构活动流。这一研究方向也引起了社区的关注。这是图流场景下的进一步复杂性层次。

此外，对来自多个源的流进行聚类，并同时学习不同流之间动态关系的本质，也将将非常有意义。

## 参考文献

- [1] C. Aggarwal. Data Streams: Models and Algorithms, Springer, 2007.
- [2] C. Aggarwal. A Framework for clustering massive-domain data streams. In ICDE Conference, pages 102–113, 2009.
- [3] C. Aggarwal. On change diagnosis in evolving data streams. In IEEE TKDE, 17(5), pages 587–600, 2005.
- [4] C. Aggarwal. On high-dimensional projected clustering of uncertain data streams, IEEE ICDE Conference, pages 1152–1154, 2009.
- [5] C. Aggarwal, J. Han, J. Wang, and P. Yu. A framework for clustering data streams. In VLDB Conference, pages 81–92, 2003.
- [6] C. Aggarwal, J. Han, J. Wang, and P. Yu. A framework for projected clustering of high dimensional data streams. In VLDB Conference, pages 852–863, 2004.
- [7] C. Aggarwal, J. Han, P. Yu, and R. Jin. On high dimensional projected clustering of data streams, Data Mining and Knowledge Discovery Journal, 10(3):251–273, 2005.
- [8] C. Aggarwal, Y. Li, P. Yu, and R. Jin. On dense pattern mining in graph streams, VLDB Conference, pages 975–984, 2002.
- [9] C. Aggarwal and K. Subbian. Event detection in social streams, SIAM Conference on Data Mining, pages 624–635, 2012.
- [10] C. Aggarwal, C. Procopiuc, J. Wolf, P. Yu, and J.-S. Park. Fast algorithms for projected clustering. In ACM SIGMOD Conference, pages 61–72, 1999.
- [11] C. Aggarwal and P. Yu. Finding generalized projected clustering in high dimensional spaces. In ACM SIGMOD Conference, pages 70–81, 2000.
- [12] C. Aggarwal and P. Yu. A framework for clustering massive text and categorical data streams. In SIAM Conference on Data Mining, pages 479–483, 2006.
- [13] C. Aggarwal and P. Yu. A framework for clustering uncertain data streams, IEEE ICDE Conference, pages 150–159, 2008.
- [14] C. Aggarwal and P. Yu. On clustering graph streams, SDM Conference, pages 478–489, 2010.
- [15] C. Aggarwal and C. X. Zhang, Mining Data Text, 2012.
- [16] C. Aggarwal, Y. Zhao, and P. Yu. Outlier detection in graph streams, ICDE Conference, pages 399–409, 2011.

# 数据聚类：算法与应用

- [17] R. Agrawal, J. Gehrke, D. Dunopulos, and P. Raghavan. Automatic subspace clustering of high dimensional data for data applications. In ACM SIGMOD Conference, pages 94–105, 1998.
- [18] M. Ankerst, M. Breunig, H.-P. Kriegel, and J. Sander. OPTICS: Ordering points to identify the clustering structure. In ACM SIGMOD Conference, pages 49–60, 1999.
- [19] B. Bahmani, R. Kumar, and V. Vassilitskii. Densest subgraph mining in streaming and MapReduce, VLDB Conference, pages 454–465, 2012.
- [20] A. Banerjee and S. Basu. Topic Models over text streams: A Study of Batch and Online Unsupervised Learning, SIAM Conference, pages 431–436, 2007.
- [21] A. Banerjee, J. Dhillon, J. Ghosh, and S. Sra. Clustering on the unit hypersphere using von Mises-Distributions. In Journal of Machine Learning Research, 6:1345–1382, 2005.
- [22] D. Blei, A. Ng, and M. Jordan. Dirichlet allocation, Journal of Machine Learning Research, 3:993–1022, 2002.
- [23] P. Bradley, U. Fayyad, and C. Reina. Scaling Clustering Algorithms to Large Databases. In ACM KDD Conference, pages 9–15, 1998.
- [24] F. Cao, M. Ester, W. Qian, A. Zhou. Density-based clustering over an evolving data stream with noise. In SDM Conference, pages 326–337, 2006.
- [25] Y. Chen and L. Tu. Density-based clustering for real time data stream. In ACM KDD Conference, pages 133–142, 2007.
- [26] G. Cormode and S. Muthukrishnan. An improved data-stream summary: The count-min sketch and its applications. Journal of Algorithms, 55(1):58–75, 2005.
- [27] G. Cormode, S. Muthukrishnan, and W. Zhuang. Conquering the divide: Continuous clustering of distributed data streams. ICDE Conference, pages 1036–1045, 2007.
- [28] A. Eldawy, R. Khandekar, and K. L. Wu. Clustering streams with an exponential-approximation of the Dirichlet multinomial distribution. ICDCS Conference, pages 289–296, 2006.
- [30] M. Ester, H.-P. Kriegel, J. Sander, and X. Xu. A density-based algorithm for discovering clusters in large spatial databases. In ACM KDD Conference, pages 226–231, 1996.
- [31] F. Farmost, J. Lewis, and C. Elkan. Scalability for clustering algorithms revisited. ACM SIGKDD Explorations, 2(1):51–57, 2000.
- [32] D. Fers. Knowledge Acquisition with incremental conceptual clustering. Machine Learning, 2:139–172, 1987.
- [33] M. Franz, T. Ward, J. McCartney, and W.-J. Zhu. Unsupervised and supervised clustering for topic tracking. ACM SIGIR Conference, pages 310–317, 2001.
- [34] G. P. C. Fung, J. X. Yu, P. Yu, and H. Lu. Parameter free bursty event detection in text streams, VLDB Conference, pages 181–192, 2005.
- [35] J. Gao, L. Li, Z. Zhang, and P.-N. Tan. An incremental data stream clustering algorithm based on dense detection. In PAKDD Conference, pages 420–425, 2005.
- [36] S. Guha, M. Meyers, N. Mishra, and L. O’Callaghan. Clustering data: Theory and practice. ICDE Conference, pages 515–528, 2000.
- [37] S. Guha, R. Rastogi, and K. Shim. CURE: An efficient clustering algorithm for large databases. In SIGMOD Conference, pages 73–84, 1998.
- [38] Q. He, C. Chang, and E. Lu. Density-based clustering for stream. SDM Conference, pages 491–496, 2007.
- [39] G. He, X. Xu, and S. Deng. Statistical grid-based data clustering. Journal of Computer Science, 17(5):611–624, 2002.
- [40] Z. He, Y. Huang, and Y. Yin. A grid-based approach for data streams, 2004.
- [41] B. Hoffman, J. Jain. Probabilistic latent semantic indexing. In SIGMOD Conference, pages 50–57, 1999.
- [42] J. Jain and R. Dubes. Clustering streams. ICDCS Conference, pages 144–155, 1998.
- [43] C. Jia, T. Sun, and X. Jin. Tracking clusters in evolving data streams over sliding windows. Data and Evolutionary Computing, 23:517–521, 2008.
- [44] L. Kaufman and P. Rousseau. Introduction to clustering. Prentice Hall, 1990.
- [45] K. Kleinberg. Bursty event detection in text streams. In KDD Conference, pages 91–101, 2002.
- [46] Z. He, T. Seidel, and T. Pal. Cell trees for data streams. ICDE Conference, pages 249–272, 2011.
- [47] Y. Rodriguez, J. Gama, and L. Lopes. A grid-based approach for multi-dimensional clustering. Knowledge and Information Systems, 38:112–128, 2007.
- [48] Y. Sun, Y. Yin, and G. Xu. Approximate clustering of data streams. VLDB Conference, pages 824–831, 2005.
- [49] M. Manku and R. Motwani. Frequency counts over data. VLDB Conference, pages 346–359, 2002.
- [51] D. Fers and J. Jain. Efficient clustering algorithms. In KDD Conference, pages 226–231, 1996.
- [52] X. Zimek, T. Pal, and T. He. Density-based clustering over high-dimensional data. ICDE Conference, pages 736–745, 2007.
- [53] L. O’Callaghan, N. Mishra, and G. He. Clustering of data streams. ICDE Conference, pages 685–694, 2005.
- [54] C. Ordonez. Clustering of data streams, VLDB Conference, pages 12–19, 2003.
- [55] N. H. Park and W. Lee. Cell trees for data clustering. Journal of Computer Science, 33:528–549, 2007.
- [56] N. H. Park and W. Lee. Statistical grid-based data clustering. SIGMOD Record, 33(1), 2004.
- [57] P. Rodriguez, J. Gama, and L. Lopes. Distributed clustering of data streams, PKDD Conference, pages 512–297, 2008.
- [58] B. W. Silverman. Density Estimation for Statistics and Data Analysis, Boca Raton, Chapman and Hall, 1986.
- [59] M. Song and H. Wang. Highly efficient incremental clustering of Gaussian Mixture Models for online data stream, SPIE, 5803:174–183, 2005.
- [60] Q. Zhang, M. Gao, and A. Zhou. Tracking high quality clusters over uncertain data streams, ICDE Conference, pages 1641–1648, 2009.
- [61] Q. Zhang, J. Liu, and W. Wang. Approximate clustering on distributed data streams, ICDE Conference, pages 1131–1139, 2008.
- [62] Q. Zhang, J. Liu, and W. Wang. Incremental clustering over multiple data streams, ICDM Conference, pages 727–732, 2007.
- [63] T. Zhang, R. Ramakrishnan, and M. Livny. BIRCH: An efficient data clustering method for very large databases. In ACM SIGMOD Conference, pages 103–114, 1996.
- [64] S. Zhong. Efficient text stream clustering. Neural networks, 18(5–6):790–798, 2005.
- [65] A. Zhou, F. Cao, W. Qian, and C. Jin. Tracking clusters in evolving data streams over sliding windows, Knowledge and Information Systems, 15(2):181–214, 2008.
- [66] A. Zhou, F. Cao, Y. Yan, C. Sha, and X. He. Distributed clustering of data streams: A fast EM-based approach, ICDE Conference, pages 736–745, 2007.

# 第11章

# 大数据聚类

Hanghang Tong
IBM T. J. Watson Research Center
Yorktown Heights, NY
htong@us.ibm.com

U Kang
KAIST
Seoul, Korea
uk@cs.cmu.edu

+   11.1 引言 ... 259
11.2 单遍聚类算法 ... 260
11.2.1 CLARANS: 与指数级搜索空间斗争 260
11.2.2 BIRCH: 与有限内存斗争 261
11.2.3 CURE: 与不规则聚类形状斗争 263
11.3 用于聚类算法的随机化技术 263
11.3.1 局部保持投影 264
11.3.2 全局投影 ... 266
11.4 并行与分布式聚类算法 268
11.4.1 通用框架 268
11.4.2 DBBC: 基于密度的聚类 269
11.4.3 ParMETIS: 图划分 269
11.4.4 PKMeans: 基于 MapReduce 的 K-Means 270
11.4.5 DisCo: 基于 MapReduce 的聚类 271
11.4.6 BoW: 基于 MapReduce 的子空间聚类 272
11.5 结论 274
参考文献 274

## 11.1 引言

随着 Web2.0 的发展，数据量正呈爆炸式增长。例如，Twitter 数据跨越 TB 级；Wikipedia 数据（例如文章和作者）规模也相当；网页点击数据据报道已达到 PB 级 [36]；2002 年 Yahoo! 网络图拥有超过 10 亿个节点和近 70 亿条条边 [27]。

另一方面，许多数据聚类算法具有很高的内在复杂度。例如，经典的 `k-means` 聚类在 `k=2` 时是 NP-hard 的。作为代表性的谱聚类算法，归一化切（NCut）也是 NP-hard [43]。因此，数据聚类的一个关键挑战在于其可扩展性，也就是说，我们如何在最小化对聚类质量牺牲的情况下，加速/扩展聚类算法。

在高级层上，许多数据聚类算法遵循以下过程：在某些初始化后（例如在 `k-means` 中随机选择 `k` 个聚类），通过迭代过程直到满足收敛标准。在每次迭代中，该算法会调整/更新每个数据点的聚类成员身份（例如在 `k-means` 中将其分配给最近的聚类中心）。因此，为了加速/扩展聚类，我们有三种基本方法：(1) 减少迭代次数（例如单遍算法）[47, 22]，(2) 减少对数据点的访问（例如通过随机化技术）[25, 38]，以及(3) 通过分布/并行化计算 [28, 13]。在本章中，我们将回顾这些类别的代表性算法。

注意，关于流数据可扩展性还有另一个重要方面，即当数据以流式模式到达时，我们可以采用批处理模式聚类算法，使得理想情况下算法能够随着新到达数据的大小进行良好扩展，而不是相对于整个数据集的大小 [16, 4, 35]。这些问题将在密度聚类的章节中独立讨论。

## 11.2 单遍聚类算法

在本节中，我们将回顾一些为大规模数据集设计的早期经典聚类算法。`CLARANS` [39, 40] 是最早使用随机搜索来应对 K-medoid 聚类中指数级搜索空间的算法之一。在 `BIRCH` [47] 中，提出了一种新的数据结构——聚类特征树（`CF-tree`），以减少输入数据超过内存大时的 I/O 成本。最后，`CURE` [22] 为每个聚类使用多个数据点来处理不规则的形状，并在层次聚类过程中进一步增加了采样。得益于这些技术，我们通常可以大幅减少聚类过程中的迭代次数。在某些极端情况下，它们通过对输入数据进行一次扫描就能产生非常好的结果。我们将这些算法统称为单遍聚类算法。

### 11.2.1 CLARANS: 与指数级搜索空间斗争

让我们从最早的代表性算法之一开始，即围绕中心点的划分（`PAM`）[32]。`PAM` 的基本思想是从每个聚类中选择一个代表性点（例如聚类中最中心的数据点）。如果我们想为 `n` 个数据点找到 `k`，算法本质上是尝试寻找 `k` 个 medoid。一旦找到了最优的 `k-medoid`，剩余的（非 medoid）数据点根据它们到 `k-medoid` 的距离分配给选定的 medoid。这遵循一个迭代过程，每次迭代中，用一个非 medoid 数据点替换当前 medoid 之一。很容易看出 `PAM` 的计算成本很高：首先，在每次迭代中，我们需要检查所有可能的 `(n-k) × k` 个配对；整个搜索空间是指数级的，我们有可能的 `k-medoid` 分配。为了解决这个问题，大型应用聚类（`CLARA`）[32] 依赖采样来缩小搜索空间。`CLARA` 不像 `PAM` 那样尝试从原始整个数据集寻找最优 `k-medoid`，而是首先从原始 `n` 个数据点中采样 `k`，然后调用 `PAM` 寻找 medoid。一旦找到最优 medoid，剩余的（未采样的）数据点根据到 `k-medoid` 的距离分配给这些聚类之一。从概念上讲，`PAM` 和 `CLARA` 都可以被视为图搜索。在图中，每个节点都是可能的聚类解决方案（即 `k-medoid`），如果节点仅在 `k-medoids` 上存在差异，则它们连接。`PAM` 从随机选择的一个 medoid 开始

![](img/b94d85a2e934001944bcc21abd9943_287.png)

**图 11.1:** 图中的节点都是可能的聚类分配（即 `k-medoid`）；且两个节点仅在一个 medoid 上不同。`PAM` (a) 从随机选择的节点开始（例如节点 3），并贪婪地移动到下一个邻居（例如节点 2）。在每次迭代中，它搜索所有可能的邻居（虚线）。`CLARA` 首先采样一个子图（阴影区域）并限制在该子图内的搜索过程。`CLARA` 也搜索整个图，但在每次迭代中，它只搜索当前节点的邻居（虚线），并贪婪地移动到其中一个邻居，直到找到更好的。基于这一点 [39, 40]，基于采样的聚类（`CLARANS`）被提出以提高效率。在 `PAM` 中，`CLARANS` 的目标是通过搜索整个图寻找局部最优解。与 `PAM` 不同，在每次迭代中，它只检查当前节点在搜索空间中的一个样本。注意 `CLARA` 和 `CLARANS` 使用采样技术来缩小搜索空间，但它们执行采样的方式不同。在 `CLARA` 中，采样是在初期进行的，而在 `CLARANS` 中，采样是在每次迭代中*动态*进行的。[39] 的实验评估显示 `CLARANS` 的动态采样策略带来了进一步改进。图 11.1 显示了 `PAM`、`CLARA` 之间的对比。

### 11.2.2 BIRCH: 与有限内存斗争

当数据超过可用内存时，I/O 成本可能会主导计算时间（例如 `PAM`，ARA）。使用层次结构的迭代减少聚类（`BIRCH`）[47] 是解决此问题的首次方法之一，它尝试减少 I/O 成本。`BIRCH` 的关键是引入了一种名为聚类特征（`CF`）的新结构以及 `CF-tree`。因此，在介绍 `BIRCH` 算法之前，让我们简单介绍这些概念。`CF` 可以被视为每个聚类的简要总结。这种动机是因为每个数据点对聚类至关重要，而我们无法在有限的主内存中保留每个数据点。另一方面，为了聚类

![](img/b94d85a2e934001944bcc21abd9943_288.png)

**图 11.2:** `CF-tree` 的图。每个节点代表一个包含最多 `B` 个子聚类的聚类。由于 `CF` 的加性，父节点的 `CF` 仅是子节点 `CF` 之和。所有叶节点连接在一起以便高效扫描。叶节点中子聚类的直径由阈值 `$T$` 限制。`$T$` 越大，树越小。聚类通常足够跟踪二阶矩。换句话说，`CF` 不仅高效，而且足以聚类整个数据集。

具体来说，一个 `CF` 是 `<N, LS, SS>`，包含聚类中数据点的数量（即零阶矩 `N`）、聚类数据点的线性和（即一阶矩 `LS`）以及聚类数据点的平方（即二阶矩 `SS`）。很容易检查 `CF` 是否满足加性；也就是说，如果我们想合并两个现有聚类，合并后的聚类的 `CF` 仅是两个原始聚类 `CF` 之和。这一特性至关重要，因为它允许我们在不访问原始数据集的情况下轻松合并两个现有聚类。

`CF-tree` 是一种高度平衡树，跟踪整个数据集的层次结构。`CF-tree` 中的每个节点代表一个由最多 `B` 个聚类组成的聚类，其中 `B` 是平衡因子。所有叶节点连接在一起以便高效扫描。此外，对于叶节点中的每个子聚类，直径上限是第二个参数 `$T$`（阈值）。显然，`$T$` 越大，`CF-tree` 的高度就越小。向 `CF-tree` 插入可以类似于 B 树的插入方式。图 11.2 展示了 `CF-tree` 的图示。

`BIRCH` 算法有两个主要步骤。首先，在插入数据点时，它通过默认阈值 `$T=0$` 的插入来构建 `CF-tree`。通过设置阈值 `$T=0$`，我们将每个数据点视为叶节点上的一个独立聚类。因此，生成的 `CF-tree` 可能会非常大，可能在扫描过程中导致内存溢出问题。如果发生这种情况，我们会增加阈值 `$T$`，并通过重新插入旧 `CF-tree` 的所有叶节点来重建 `CF-tree`。通过将数据点分组，生成的 `CF-tree` 构建了数据集的初始总结，反映了其聚类结构。

由于输入倾斜和/或按页面划分，来自初始 `CF-tree` 的聚类结构可能不够准确，无法反映真实的聚类结构。为了解决这个问题，第二个关键步骤是“全局聚类”，即对叶节点中的所有聚类进行聚类。这是通过将具有 `$n'$` 个数据点的子聚类转换 `$n'$` 次，然后运行另一种凝聚层次聚类算法或改进的聚类算法来实现。

这两个主要步骤之间，有一个可选步骤通过重新插入叶项来精炼 `CF-tree`（树压缩）。通常这会导致更紧凑的 `CF-tree`。在全局聚类步骤之后，还有另一个选项（聚类精炼），将所有数据点分配到全局聚类步骤产生的聚类中心。图 11.3 总结了 `BIRCH` 算法的总体流程图。

![](img/b94d85a2e934001944bcc21abd9a9943_289_0.png)

图 11.3：`BIRCH` 算法的流程图。

[47] 中的实证评估表明，`BIRCH` 在时间和空间效率方面始终优于之前的 `CLARANS`。它对输入数据序列的顺序也更具鲁棒性。`BIRCH` 还具有一些额外优势，例如对离群点具有鲁棒性，并且更具并行性。

## 11.2.3 CURE：应对不规则簇的斗争

在 `CLARANS` 和 `BIRCH` 中，我们都使用单个数据点来表示一个聚类。从概念上说，我们假设每个簇都是球形的，但在实际应用中，簇可能呈现出更复杂的形状，情况并非如此。另一个极端是我们可以保留每个簇中的所有数据点，但对于大型数据集来说，计算和空间成本可能过高。为了解决这个问题，使用 `CURE` [22] 的聚类方法建议使用一组特征良好的数据点来表示一个聚类。

`CURE` 本质上是一种层次聚类算法。它通过将每个数据点视为单个簇，并递归地合并现有的簇，直到只剩下 `k` 个簇。为了在每次迭代中决定合并哪些簇，它计算两个簇之间所有可能的代表点之间的最小距离。`CURE` 使用两个主要数据结构来实现高效搜索。首先，它使用堆（heap）来跟踪每个现有簇到其最近簇的距离。此外，它使用 `k-d` 树来存储每个簇的所有代表点。

为了加速计算，`CURE` 首先对输入数据进行采样，并在采样数据上分析上述过程。作者使用切尔诺夫界界（Chernoff bound）来分析所需的样本量。当原始数据量很大时，不同的簇之间相互重叠，这反过来需要较大的样本量。为了缓解这个问题，`CURE` 使用分区法来加速。具体来说，它首先将 `$n'$` 个已采样数据点划分为 `$p$` 个分区。对于每个分区，它运行部分层次聚类，直到达到预定义的簇数量或超过某些阈值。之后，它对来自 `$p$` 个分区的所有簇运行聚类（“全局聚类”）。最后，根据非采样点到代表点的距离将其分配给一个簇（“标记”）。图 11.4 总结了 `CURE` 算法的流程。

[22] 中的实证评估显示，与 `BIRCH` 相比，`CURE` 的执行时间更短。此外，与 `BIRCH` 相比，`CURE` 通过常数因子将代表点收缩到簇中心对离群点具有鲁棒性。

## 11.3 聚类算法的随机化技术

在上一节中，我们已经看到如何利用采样来加速聚类算法，例如像 `CLARA` 和 `CLARANS` 那样减少搜索空间，或者像 `BIRCH` 和 `CURE` 那样进行预聚类/部分聚类。在本节中，让我们进一步观察如何利用随机化技术来解决聚类中的可扩展性问题。
假设我们要在 `$d$` 维空间中的 `$n$` 个数据点聚类为 `$k$` 个簇。我们可以将这些数据点表示为 `$n \times d$` 数据矩阵 `$A$`；该矩阵的每一行都是 `$d$` 维空间中的一个数据点。各种随机化技术的基本思想是缩小输入数据矩阵 `$A$` 的规模，例如通过将其转换为低维 `$l$` 维空间（`$l < d$`），然后在还原后的空间上进行聚类。在本节中，我们将回顾主要的算法类型。

### 11.3.1 局部保持投影

在局部保持投影（也称为随机投影）方法中，我们将原始的 `$d$` 维数据投影到低维空间，并在概率意义上保留成对点之间的距离。在许多聚类算法中，是成对距离量决定了聚类结构。我们预期投影子空间中的聚类结果能为原始空间的结果提供相当良好的近似。
除了聚类之外，随机投影本身在各种数据挖掘任务中具有广泛的应用前景（例如相似性搜索、近重复检测）。在这里，我们将首先对典型的随机投影算法进行通用介绍，然后介绍如何在聚类设置中应用它们。

局部保持投影的一个经典结果来自 Johnson 和 Lindenstrauss [25]，可以表述如下：

**引理 11.1** 假设 `$\epsilon > 0$`，且 `n` 为整数。令 `t` 为正整数，使得 `t \geq t_0 = O(\log n/\epsilon^2)`。对于 `$\mathbb{R}^d$` 空间中具有 `n` 个数据点的任意集合 `P`，存在 `f: \mathbb{R}^d \to \mathbb{R}^t`，使得对于所有 `u, v \in P`，我们有：
```
