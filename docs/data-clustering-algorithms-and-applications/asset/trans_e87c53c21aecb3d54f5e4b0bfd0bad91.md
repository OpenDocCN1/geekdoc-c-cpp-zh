

# 数据聚类：算法与应用

- 数字 $k$ 和 $l$ 通常较小，因此 $k \times l$ 矩阵 $G$ 也较小。此外，行向量和列向量 $r$ 和 $c$ 可以放入内存中。
- 对于每一行（或每一列），寻找最佳分配只需要 $r$、$c$ 和 $G$。它不需要其他行。

利用上述特征，将 $G、$r$ 和 $c$ 通过 MapReduce 的参数传递机制映射为 mapper。每一行（或每一列）都可以独立地处理，并分配到使成本最小的最优组。每一行（或每一列）的迭代都需要一个 map 阶段和一个 reduce 阶段，并且它遵循第 11.4.1 节所示的通用框架。mapper 读取每一行并执行本地聚类。reducer 通过收集局部信息执行全局聚类，并输出更新后的 $G$ 矩阵和 $r$ 行标签向量（列迭代为 $c$ 列标签向量）。DisCo 通过在 mapper 和 reducer 之间仅传输标签向量和 $G$ 矩阵来最小化网络流量；矩阵数据无需传输。

实验在一个 39 节点的 Hadoop 集群上进行，矩阵数据规模高达 250 万乘以 130 万。以聚合吞吐量衡量的性能随机器数量线性增长。由于 DisCo 是一种精确算法，其聚类质量与串行算法相同。

## 11.4.6 BoW：基于 MapReduce 的子空间聚类

BoW [7] 是一种基于 MapReduce 的分布式子空间聚类算法。BoW 提供了基于 MapReduce 的子空间聚类算法：并行聚类 (ParC) 和样本忽略 (SnI)。ParC 有三个步骤，如图 11.9 所示：(1) 使用 mappers 划分输入数据，使数据聚合到 reducer 中；(2) reducer 使用任何子空间聚类算法（例如作为插件的 [8]）在其分配的分区中寻找聚类；(3) 合并上一步的聚类以获得最终聚类。步骤 (1) 和 (3) 分别在 map 阶段 reduce 阶段执行，步骤 (3) 在单台机器上串行完成。

SnI 使用采样来最小化网络流量。SnI 包含如图 11.10 所示的两个阶段。在第一阶段，(1) mappers 随机采样数据（例如数据的 10%）并将结果发送给 reducer。(2) reducer 运行子空间聚类算法以找到初始聚类。在第二阶段，(3) mappers 向 reducers 发送不属于第一阶段发现的初始聚类的数据点；(4) reducers 寻找聚类；(5) 单台机器将第一阶段的初始聚类组合形成最终聚类。

![](img/b94d85a2e934001944bcc21abd9a9943_298_0.png)

**图 11.9：** 用于子空间聚类的 ParC 算法。(1) Mapper 划分数据。(2) 每个 reducer 寻找聚类。(3) 单台机器收集并合并来自 reducer 输出的所有聚类，以形成最终聚类。

![](img/b94d85a2e934001944bcc21abd9a9943_299_0.png)

**图 11.10：** 用于子空间聚类的 SnI 算法。(1) Mapper 采样数据。(2) reducer 从采样数据中找到初始聚类。(3) Mapper仅向 reducers 发送不属于第二步初始聚类的数据。(4) Reducers 寻找聚类。(5) 单台机器将第二阶段和第四阶段的聚类组合以形成最终聚类。

ParC 和 SnI 的第二阶段遵循第 11.4.1 节描述的通用框架：数据被划分、进行本地聚类、本地聚类被聚合以形成全局聚类。SnI 的第一阶段是最小化网络流量的预处理步骤。

ParC 和 SnI 也有各自的优缺点。在磁盘 I/O 次数方面，ParC 更好，因为它只需要 map-reduce 步骤，而 SnI 使用两个 map-reduce 步骤。然而，在网络流量方面，SnI 在第一阶段和第二阶段的过滤中表现更好。问题是哪种算法运行得更快？有很多参数可以回答这个问题：例如，使用的 reducer 数量、数据大小、磁盘速度、网络速度、启动成本、shuffle 阶段数据传输的成本以及采样率。BoW 将成本（运行时间）推导出参数的函数，以确定适用于不同数量 reducer 的最佳算法。BoW 在数据规模上显示出线性可扩展性。最后，我们注意到由于数据的划分，ParC 和 SnI 并不是精确算法。然而，来自 ParC 或 SnI 的聚类质量与该算法的串行版本相当。

## 11.5 结论

考虑到 (1) 数据规模爆炸式增长和 (2) 聚类的内在复杂度通常很高（例如 NP-hard），可扩展性似乎是一个“永无止境”的挑战。在本章中，我们回顾了加速聚类的技术，包括 (a) 通过“单次通过”减少迭代次数，(b) 减少输入数据复杂的随机技术，以及 (c) 加速的分布式并行算法。未来的趋势是整合所有可用技术以实现更好的可扩展性。

## 参考文献

- [1] Dimitris Achlioptas and Frank Sherry. Fast computation of low-rank matrix approximations. Journal of the ACM, 54(2), 2007.
- [2] Sanghamithra Bandopadhyay, Giannella, Ujjwal Maulik, Kun Liu, and Soumik Datta. Clustering data streams in peer-to-peer environments. Information Sciences, 16(14):1952–1985, 2006.
- [3] Chronos Bousidis, Anastasios Zou, and Petros Drineas. Random projections. In NIPS, 298–306, 2010.
- [4] Mases Chikar, Chandra Chekuri, and Rajeev Motwani. Incremental clustering and dynamic retrieval. In STOC, 626–635, 1997.
- [5] Wen-Y Chen, Yanqi Song, Hongjie Bai, and Edward Y. Chang. Parallel spectral clustering. IEEE Trans. on Pattern Analysis and Machine Intelligence, 33(3):568–586, 2011.
- [6] Cheng-Chao Chu, Sangun Kim, Yuan Yu, Gary R. Bradski, and Andrew Y. Ng. MapReduce for learning. In NIPS, 281–288, 2006.
- [7] Robinson Ferreira Cordeiro, Caetano Trainira R., Julio López, Umesh Kang, and Christos Faloutsos. Clustering very large multi-dimensional datasets. In KDD, 690–698, 2011.
- [8] Robinson Ferreira Cordeiro, Jaime M., Christos Faloutsos, and Caetano Trainira Jr. Finding clusters in subspaces of large, multi-dimensional datasets. In ICDE, 625–636, 2010.
- [9] Abhinandan Das, Mayur Dhar, Ashutosh Garg, and ShyamSundar Rajaraj. Google personalization: Scalable collaborative filtering. In WWW, 271–280, 2007.
- [10] Sanjay Gupta. Experiments with random projection. In UAI, 143–151, 2000.
- [11] J. Dean and S. Ghemawat. MapReduce: Simplified data processing. OSDI, 139–149, 2004.
- [12] Inderjit S. Dhillon, Subramanyam, and Dharmendra S. Modha. Information-theoretic co-clustering. In KDD, 89–98, 2003.
- [13] Inderjit S. Dhillon and Dharmendra S. Modha. Distributed clustering. In Large-Scale Data Data, 245–260, 1999.
- [14] P. Diaconis and J. Freedman. Asymptotics of graphical pursuit. Contemporary Mathematics, 26:189–206, 1984.
- [15] Petrov Drineas, Ravi Kannan, and Michael W. Mahoney. Fast Monte Carlo: Computing a tensor. SIAM Journal of Computing, 36(1):132–157, 2005.
- [16] Martin Ester, Hans-Peter Kriegel, Michael Wimmer, and Xiaowe Xu. Incremental clustering in a data warehouse. In VLDB, 323–333, 1998.
- [17] Martin Ester, Hans-Peter Kriegel, Jörg Sander, and Xiaowe Xu. A density-based algorithm for discovering clusters in large spatial databases. In KDD, 226–231, 1996.
- [18] Xiaoli Zheng and Carla E. Brodley. Random projection for high dimensional clustering: In ICML, 186–193, 2003.
- [19] George Forman and Bin Zhang. Clustering can be efficient and exact. SIGKDD Explorations, 2:34–38, 2000.
- [20] Z. Vedi and J. Komlos. The eigenvalues of random symmetric matrices. Combinatorica, 1:233–241, 1981.
- [21] G. H. Golub and C. Van-Loan. Matrix Computations, 2nd edition, The Johns Hopkins University, Baltimore, 1989.
- [22] Sudiputo Guha, Rajeev Rastogi, and Kyuseok Shim. CURE: An efficient algorithm for large databases. Information Systems, 26(1):35–58, 2001.
- [23] Geetha Jagannathan and Rebecca W. Wright. Privacy-preserving distributed-means clustering over arbitrarily partitioned data. In KDD, 593–599, 2005.
- [24] Eshref Januzaj, Hans-Peter Kriegel, and Martin Pfeifle. BDDC: Density based distributed clustering. In EDBT, 88–105, 2004.
- [25] W. B. Johnson and J. Lindenstrauss. Asymptotics of Lipschitz mappings to a Hilbert space. Contemporary Mathematics, 26:189–206, 1984.
- [26] U. Kang, Evangelos E. Papalexakis, Abhay Harpale, and Christos Faloutsos. Gatensor: Scaling tensor analysis over 100 times. In KDD, 316–324, 2012.
- [27] U. Kang, Hanghang Tong, Jimeng Sun, Chung-Yung Lin, and Christos Faloutsos. GBASE: A scalable and general graph management system. In KDD, 1091–1099, 2011.
- [28] U. Kang, Charalamos E. Tsourakakis, and Christos Faloutsos. Pegasus: A peta-scale graph mining system. In ICDM, 229–238, 2009.

