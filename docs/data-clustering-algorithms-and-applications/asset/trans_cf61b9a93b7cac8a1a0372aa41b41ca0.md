

# 数据聚类：算法与应用

指向其他数据仓库的链接 STATOO [71] 和 David Dowe 的数据链接 [72]。后者还提供了关于数据挖掘案例研究和竞赛的在线资源。

从 Kd 仓库 [73] 和其他数据挖掘竞赛 [74] 可以获取更多大规模的数据集。这些数据集不仅规模巨大，而且是从真实世界的问题中收集的，带来了许多挑战。聚类通常被用于解决此类真实世界的挑战，因为这些问题中的许多通常属于无监督类别。在统计数据方面，Github 数据集归档 [75] 是一个被广泛使用的数据集合。

上述提到的真实世界数据集外，还有一个基础聚类问题套件 [47]，它提供了一个合成生成的 2D 和 3D 数据集的简单集合。这提供了一些具有不同尺寸、形状和密度的测试数据集。

针对特定类型的数据，有许多资源可用。对于时间序列聚类，UCR 时间序列网络 [36] 提供了用于聚类的非常长的连续数据。另一个时间序列数据库可以在 [37] 获取。对于网络数据，由斯坦福大学的 Jure Lesovec 托管的 SNAP 仓库 [40] 提供了大量的网络数据集。

为了测试文档聚类的性能，有几个可用的文本文档仓库。一些最流行的文本文档包括 Reuters [76]、20NewsGroups [77]、TREC [78] 和 Cora [79]。

为了评估生物学聚类，有大量的网站托管基因表达 (GEO) 仓库 [68]，其中包含了一个全面的基因表达数据集以及用于生成这些数据的源文件。基因表达模型选择器（Gene Expression Model Selector）提供了一个最广泛使用的基因表达数据集简单仓库 [69]，其他癌症特异性基因表达数据集可以在 [70] 获取。同样，为了测试生物网络聚类算法的性能，有很多包含蛋白质相互作用的数据库。最流行的有 DIP（相互作用蛋白质数据库）[66]、BioGRID [67]、STRING（相互作用基因/蛋白质检索字符串）[65] 和 MIPS（哺乳动物蛋白质相互作用数据库）[64]。最后一个资源连接到其他几个相互作用数据库。

为了评估序列聚类算法，在 [63] 可以获得几个生物学序列数据库仓库。最广泛使用的仓库是用于核酸序列的 GenBank [61] 和 EMBL [62]，以及用于蛋白质序列的蛋白质信息资源 (PIR) [60] 和 UniProt [59]。

在图像应用背景下，机器学习和计算机视觉社区的研究人员已使用聚类来解决图像的自动分组和图像分割。聚类有助于图像数据库的高效组织和检索。ImageCLEF [82] 和 ImageNet [83] 是广泛使用的图像数据仓库，用于演示图像数据检索任务的性能。数据聚类也可用于图像分割。来自卡内基·梅隆大学的视觉与自主系统中心图像数据库 [80] 和伯克利分割数据集 [81] 可用于测试图像分割问题的聚类性能。提供图像数据库的网站详细列表列于 [84] 和 [85] 中。

## 24.4 总结

本章总结了从书籍、综述以及商业和非商业软件软件包方面数据聚类的关键资源。虽然许多综述从技术或数据类型的方面探讨了数据聚类的不同方面，但在创建一个涵盖该主题现代文献的单一整合书籍方面似乎存在空白。本书旨在填补这一空白。

## 数据聚类的教育与软件资源

## 参考文献

- [1] E. Achert, S. Goldhofer, H.-P. Kriegel, E. Schubert, and A. Zimek. Evaluation of clusterings – metrics and visual support. In ICDE Conference, pages 1285–1288, 2012. http://elki.dbs.ifi.lmu.de/wiki/Algorithms#n
- [2] C. Aggarwal, and C. Zhai. A survey of clustering algorithms, In Mining Data, pages 77–128, 2012.
- [3] M. Anderberg. Cluster Analysis for Applications. Academic Press, 1973.
- [4] A. Baraldi and P. Blonda. A survey of fuzzy clustering algorithms for pattern recognition. I. IEEE Transactions on Systems, Man, and Cybernetics, Part B, 29(6):778–795, 1990 (文中说是1999年，请检查上下文)
- [5] A. Baraldi and P. Blonda. A survey of fuzzy clustering algorithms for pattern recognition. II. IEEE Transactions on Systems, Man, and Cybernetics, Part B: 29(6):786–801, 1999.
- [6] P. Berkh. A survey of data mining techniques. Grouping Multidimensional Data, pages 25–71, 2006.
- [7] A. Bifet, G. Holmes, P. Pfringer, H. Kranen, T. Jansen, and T. Seidl. MOA: Massive online, a framework for stream classification and clustering. Journal of Machine Learning Research-Proceedings Track, 11:44–50, 2010. http://moa.cms.waikato.ac.nz/publications/
- [8] S. Bochee, K. Faust, G. Lima-Mendez, O. Sand, R. Janky, G. Vanderstocken, and J. Deville. Netweaver: A toolbox for the analysis of biological networks, clusters, and patterns. Nucleic Acids Research, 36(Web issue), July 2008.
- [9] B. Duran. Cluster Analysis: A Survey. Springer-Verlag, 1974.
- [10] M. B. Eisen, P. T. Spellman, O. Brown, and D. Botstein. Cluster analysis and display of genome-wide experiments. Proceedings of the National Academy of Sciences, 95(25):14683–14688, 1998. http://rana.lbl.gov/Eisen.htm
- [11] M. Filipponi, F. Casamastra, F. Masulli, and S. Rovetta. A survey of kernel and spectral methods for clustering. Pattern Recognition, 41(1):176–190, 2008.
- [12] S. Fortunato. Community detection in graph, 48(3):75–174, 2010.
- [13] A. Frank, and A. Asuncion. Machine Machine Learning Repository, Irvine, CA: University of California, School of Information Science, 2010. http://archive.ics.edu
- [14] G. Gan, C. Ma, and J. Wu. Data Clustering: Theory, Algorithms, and Applications. SIAM, Society for Applied Mathematics, 2007.
- [15] J. A. Hartigan. Clustering Algorithms. John Wiley and Sons, 1975.
- [16] E. Hruschka, R. Campello, F. Freitas, and Leon De Carvalho. A survey of evolutionary algorithms for clustering. IEEE Transactions on Systems, Man, and Cybernetics, Part C, 39(2):133–155, 2009.
- [17] A. Jain. Data clustering: beyond k-means. Pattern Recognition Letters, 31(8):651–666, 2010.
- [18] A. Jain and R. Dubes. Algorithms for Clustering Prentice Hall, 1988.
- [19] A. Jain, M. Murty, and P. Flynn. Data clustering: A review. ACM Computing Surveys (CSUR), 31(3):264–323, 1999.
- [20] D. Chiang, T. Kang, and A. Zheng. Analysis for gene expression data: A survey. IEEE Transactions on Knowledge and Data Engineering, 16(11):1370–1386, 2004.
- [21] L. Kaufman and P. Rousseau. Groups in Data: An Introduction to Cluster Analysis. Wiley-Interscience, 2005.
- [22] H.-P. Kriegel, P. Kröger, and A. Zimek. Clustering high-dimensional data: A survey on subspace clustering, pattern-based clustering, and correlation clustering. ACM Transactions on Knowledge Discovery from Data (TKDD), 3(1):1–58, 2009.
- [23] T. Liao. Clustering of time series data–A survey. Pattern Recognition, 38(11):1857–1874, 2005.
- [24] U. von Luxburg. A tutorial on spectral clustering, Statistics and Computing, 17(4):395–416, 2007.
- [25] S. Madeira and A. Oliveira. Bioclustering for biological data analysis: A survey. IEEE/ACM Transactions on Computational Biology and Bioinformatics, 1(1):24–45, 2004.
- [26] B. Mirkin. Clustering for Data Mining: A Data Recovery Approach. Chapman and Hall/CRC, Boca Raton, 2005.
- [27] E. Muller, S. Gnemann, I. Asset, and T. Seidl. Evaluating clustering in subspace projections of high dimensional data. PVLDB, 2(1):1270–1281, 2009.
- [28] F. Murtagh. A survey of recent advances in hierarchical clustering. The Computer Journal, 26(4):354–359, 1983.
- [29] L. Parsons, E. Haque, and H. Liu. Subspace clustering for high dimensional data: A review. ACM SIGKDD, 6(1):90–105, 2004.
- [30] S. Schaeffer. Graph clustering. Computer Science Review, 1(1):27–64, 2007.
- [31] P. Willett. Recent trends in hierarchical document clustering: A critical review. Information Processing & Management, 24(5):577–597, 1998.
- [32] R. Xu and D. Wunsch. Survey of clustering algorithms. IEEE Transactions on Neural Networks, 16(3):645–678, 2005.
- [33] R. Xu and D. Wunsch. Clustering. Wiley-IEEE Press, 2008.
- [34] Y. Zhao, G. Karypis, and F. Fayyad. Hierarchical clustering algorithms for document datasets. Data Mining and Knowledge Discovery, 10(2):141–168, 2005.

