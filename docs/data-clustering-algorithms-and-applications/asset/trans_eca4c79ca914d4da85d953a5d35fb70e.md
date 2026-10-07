

# 数据聚类：算法与应用

## 表 17.1：不同的聚类方法

| 聚类方法 | 类别 | 可调参数 | 自由软件 |
|---|---|---|---|
| 带有几何信息的划分 | 平衡二分划分 | | Chaco [77] |
| 坐标二分 | 平衡二分划分 | | Party [136] |
| 惯性二分 | 平衡二分划分 | | Chaco [77] |
| 几何二分 | 二分划分 | 重叠图参数 alpha 和 k | Chaco [77], Zoltan [179] |
| Kernigh-Lin 算法 | 划分划分 | 划分数量 k | Party [136], Chaco [77] |
| 凝聚类与分裂类算法 | 层次聚类 | 划分数量 k | Orange [38], hcluster [49] |
| 谱聚类 | 硬聚类 | 划分数量 k | Chaco [77], MATLAB 软件包 [31] |
| 马尔可夫聚类 | 软聚类 | 膨胀参数 r 控制簇的粒粒度 | MCL 软件 [166] |
| 多级划分 | 硬聚类 | 粗化与去粗化的开销 | Metis [86], Graclus [42], Chaco [77], SCOTT [134] |
| MLR-MCL | 硬/软聚类 | 膨胀参数 r，最粗糙图的大小 c | MLR-MCL 软件 [147] |
| 超图划分 | 硬聚类 | 划分数量 k，最粗糙超图中的单元数量 | PaH [26], Zoltan [179], hMetis [77] |
| 二分图划分 | 硬聚类 | | 协同聚类软件 [34], Metis [86] |
| 动态图划分 | 硬/软聚类 | | |
| 有向图划分 | 硬/软聚类 | 聚类数量，子结构的定义 | GraphCl [140] |
| 具有重叠社区的网络 | 软聚类 | | MOSES 软件 [109] |
| 概率方法 | 硬/软聚类 | | SBM & SCF 软件 [108] |

# 网络聚类

网络聚类问题的可扩展解决方案。这些包括用于处理超出单机存储能力的图和网络的可扩展、并行和分布式算法。在算法层面，依赖于图粗化的多级算法优于直接在输入图上工作的传统方法 [42, 86, 148]。流式算法 [2] 以及基于 GPU 和多核的架构感知算法提供了一种正交的方法 [21, 132]。在 Hadoop [82, 130] 等平台上的算法同样流行，因为近期存在向无共享架构的商品化集群和云计算的趋势。

- **领域知识的使用：** 在构建过程中对领域知识的利用不足已成为数据挖掘中的一个共同问题。数据挖掘领域的人员在训练阶段经常丢弃重要的领域知识，这导致他们在测试期间无法独立地验证所提方法的有效性 [131]。这种倾向往往限制了解决方案的稳健性及其科学进展。有必要重新考虑如何将领域知识纳入方法中。我们认为领域知识是获取发现的宝贵资源，因为它能有效引导整个过程。特别是现代图，众所周知与其关联有大量的价值信息和元数据。因此，需要稳健的算法，通过利用这些丰富的信息在聚类过程中产生更好的结果。

尽管网络划分问题已经研究了数十年，但与节点和边关联的大量信息的现代大型网络提出了新颖、复杂且难以克服的挑战，要求进行新的调查、新颖的技术以及稳健的创新方法来处理通用问题。需要并行和分布式系统的通用可扩展算法、基于 GPU 和多核系统的架构感知解决方案，以及使用 MapReduce [40] 框架和在云系统上的算法来处理这些不断增长的图。鉴于这是一个充满前景且令人兴奋的研究领域，我们期待未来在该主题上看到更多新颖的算法、原则方法和令人兴奋的结果。

# 致谢

感谢编辑和匿名评审员提供的宝贵意见、深刻建议和建设性反馈，这对改进本文有极大帮助。
此工作受 NSF 资助 IIS-0197070 和 NSF 资助 CCF-1217353 支持。本材料中出的任何观点、发现、结论或建议均代表作者，不一定反映美国国家科学基金会的观点。

# 参考文献

- [1] C. C. Aggarwal, Y. Xie, and P. S. Yu. Towards community detection in locally heterogeneous networks. In SDM, pages 391–402. SIAM / Omnipress, 2011.
- [2] C. C. Aggarwal, Y. Zhao, and P. S. Yu. On clustering graph streams. In SDM, pages 478–489, 2010.
- [3] Y-Y. Ahn, J. P. Bagrow, and S. Lehmann. Link communities reveal multiscaleiscale complexity in networks. Nature, 466(7307):761–764, 2010.
- [4] C. J. Albert, J. Huang, and A. B. Kahnh. Multilevel circuit partitioning. In Proceedings of the 34th ACM/IEEE Design Automation Conference, pages 530–533, 1998.
- [5] R. Andersen, F. Chung, and K. Lang. Local graph partitioning using PageRank vectors. In FOCS '06: Proceedings of the 47th Annual IEEE Symposium on Foundations of Computer Science, pages 475–486, Washington, DC, USA, 2006.
- [6] R. Andersen and K. J. Lang. Communities from seed sets. In WWW '06: Proceedings of the 15th International Conference on World Wide Web, page 232. ACM, 2006.
- [7] A. Anthony and M. desJardin. Generative models for clustering: The next generation. In AAAI Spring Symposium: Social Information Processing, pages 7–10. AAAI, 2008.
- [8] A. Asur and S. Parthasarathy. A viewpoint-based approach for interaction graph analysis. In KDD '09: Proceedings of the 15th ACM SIGKDD International Conference on Knowledge Discovery and Data Mining, pages 79–88, New York, NY, USA, 2009. ACM.
- [9] S. Asur, S. Parthasarathy, and D. Ucar. An ensemble approach for clustering scalable graphs. In LinkKDD Workshop, 2006.
- [10] S. Asur, S. Parthasarathy, and D. Ucar. An event-based framework for characterizing the evolutionary behavior of interaction graphs. In KDD '07: Proceedings of the 13th ACM SIGKDD International Conference on Knowledge Discovery and Data Mining, pages 913–921, New York, NY, USA, 2007. ACM.
- [11] A. L. Barabási. Scale-free networks. Scientific American, 288(5):60,2003.
- [12] A. L. Barabási and R. Randall. Linked: The new science of networks. American journal of Physics, 71:409, 2003.
- [13] S. T. Barnard and H. D. Simon. Fast multilevel implementation of recursive bisection for partitioned structures. Concurrency Practice and Experience, 6(2):101–118, 1994.
- [14] J. Bascom, P. Jordano, C. J. Melan, and J. M. Olesen. The nested assembly of plant-animal mutualistic networks. Proceedings of the National Academy of Sciences of the United States of America, 100(16):9383, 2003.
- [15] J. Baumes, K. Goldberg, S. Krishnasamoorthy, M. M. Ismail, and N. Preston. Communities by clustering a graph into overlapping subgraphs. In Numero Guimaes and Pedro T. Isias, IADIS, pages 97–104. IADIS, 2005.
- [16] T. Y. Berger-Wolf and J. Saif. A framework for analysis of dynamic social networks. In KDD '06: Proceedings of the 12th ACM SIGKDD International Conference on Knowledge Discovery and Data Mining, page 528. ACM, 2006.
- [17] F. Freve, L. Zhao, and M. Quiles. Overlapping community structure in complex networks using particle competition. In Proceedings of the International Conference on Artificial Intelligence and Computational Intelligence, AIIC '09, pages 619–628, Berlin-Heidelberg, 2009.
- [18] A. Z. Broder, C. S. Glassman, M. S. Manasse, and G. Zweig. Syntactic clustering of the web. Computer Networks and ISDN Systems, 29(8-13):1157–1166, 1997.

