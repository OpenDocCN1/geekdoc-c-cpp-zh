

# 生物数据聚类

存储在数据库中或通过高通量实验获得的网络。软件可以在 http://rsat.ulb.ac.be/neat/ 获取。

CD-HIT 广泛用于蛋白质和 DNA 序列聚类。可以通过 http://weizhong-lab.ucsd.edu/cd-hit/ 获取。该网站提供一个提供在线 CDHIT服务的服务器。或者，用户也可以下载该程序进行离线使用。CD-HIT 软件包包含多种针对不同生物序列定制的聚类工具。标准的 BLAST 软件包包含一个名为 BLASTclust 的程序，可对蛋白质或 DNA 序列进行聚类。BLAST 接受许多参数，可用于控制评分密度、百分比一致性和对齐长度聚类阈值的严紧性。除了聚类之外，BLASTclust 还可以用于从源数据库创建冗余序列集。以下网站 http://toolkit.tuebingen.mpg/deblastclust 提供了 blastCluster 服务器的访问。

# 16.6 讨论与总结

本章综述了在生物数据领域成功应用的不同数据聚类技术。我们讨论了不同类型的生物数据，数据聚类在这些数据中产生了具有前景且具有生物学意义的结果。对于表达数据的聚类，讨论了不同类别的聚类，即聚类、趋势聚类和时间序列聚类，以及一些标准算法。还讨论了生物网络的不同属性以及研究最广泛的网络聚类算法。各种生物序列的相似性度量和聚类算法也已得到研究。通过聚类算法，我们还讨论了所得聚类的生物学验证。

随着越来越多的生物学家熟悉数据聚类算法的进展，我们可以预见一种数据驱动的生物科学将优于假设驱动的科学。此外，我们还希望这些聚类算法提供的新见解能够驱动一系列受生物学限制的实验，从而获得关于细胞功能的更深洞察。

# 参考文献

- [1] B. Adamcek, G. Palla, I. J. Farkas, I. Derenyi, and T. Vicsek, CFinder: Locating cliques and overlapping modules in biological networks. Bioinformatics, 22(8):1021–1023, 2006.
- [2] J. S. Aguilar-Ruiz. Shifting and scaling patterns from gene expression data. Bioinformatics, 21(20):3840–3845, October 2005.
- [3] U. Alon, N. Barkai, D. A. Notterman, K. Gishgader, S. Yarradagger, D. Mackdagagger, and A. J. Levine. Broad patterns of gene expression by clustering analysis of tumor and normal colon tissues by oligonucleotide arrays. Proceedings of the National Academy of Science of the United States of America, 96(12):6745–6750, June 1999.
- [4] F. Alqadah, J. S. Bader, R. Anand, and C. K. Reddy. Query-based clustering using concept analysis. In Proceedings of SIAM International Conference on Data Mining, 648–659, 2012.
- [5] S. Altschul, W. Gish, M. Miller, E. Myers, and D. Lipman. Basic local alignment search tool. Journal of Molecular Biology, 215:403–410, 1990.
- [6] I. P. Androulak, E. Yang, and R. R. Almon. Analysis of time-series gene expression data: Methods, challenges, and opportunities. Annual Review of Biomedical Engineering, 9:205–n228, 2007.
- [7] M. Ashburn, C. Ball, J. Blake, D. Botstein, H. Butler, J. M. Cherry, A. P. Davis, K. Kolinski, S. Dwight, J. T. Eppig, M. A. Harris, D. Hill, L. Isssel-Tarver, A. Karsarski, S. Lewis, J. C. Mase, E. J. Richardson, M. Ringwald, G. M. Rubin, and G. Sherlock. GeneOntology: For the unification of biology. The Gene Ontology Consortium. Nature Genetics, 25(1):25–29, 2000.
- [8] S. Asur, D. Ucar, and S. Parthasarathy. An ensemble framework for clustering protein-protein interaction networks. Bioinformatics, 23(13):i29–i40, 2007.
- [9] G. Bader and C. Hogue. An automated method for finding molecular complexes in large protein interaction networks. BMC Bioinformatics, 4(1):2, 2003.
- [10] C. Bernhard and H. Burkhart. Measuring HMM similarity with the Bayes probability of error and its application to online handwriting recognition. Proceedings of the Sixth International Conference on Document Analysis and Recognition, ICDAR '01, pages 406–n411, 2001.
- [11] Z. Bar-Joseph. Analyzing time series gene expression data. Bioinformatics, 20(16):2493–n2503, 2004.
- [12] S. Barkow, S. Bleurer, A. Prelic, P. Zimmermann, and E. Zitler. BiCAT: A clustering analysis tool. Bioinformatics, 22(10):1282–1283, 2006.
- [13] A. Ben-Dor, B. Chor, R. Karp, and Z. Yakhini. Discovering local structure in gene expression data: The data-preserving submatrix. Journal of Computational Biology, 10(3–373–384, 2003.
- [14] A. Ben-Dor and Z. Yakhini. Clustering gene expression patterns. Proceedings of the Third International Conference on Computational Biology, RE99, pages 33–42, 1999.
- [15] S. Broh, K. Faust, G. Lima-éndez, O. Sand, R. Janky, G. Vandersten, and J. van Helden. NeAT: A toolbox for the analysis of biological networks, classes and pathways. Nucleic Acids, 36(Web Server), July 2008.
- [16] S. Bro and J. van Helden. Evaluation of clustering algorithms for protein-protein interaction networks. Bioinformatics, 7(1):488, 2006.
- [17] J. Burke, D. Davidson, and W. Hiding. A validated method for clustering EST and full-length cDNA. Genome Research, 9(11):1135–1142, 1999.
- [18] S. Busysin, O. Prokopyev, and P. Pardalos. Clustering in data mining. Computers and Operations Research, 35(9):2964–2987, 2008.
- [19] A.J. Butte and I.S. Kohane. Mutual information relevance using pairwise measures. In Pacific Symposium on Biocomputing, volume 5, pages 418–429, 2000.
- [20] C. Chead, M. P. Freed, and K. Becker. Analysis of microarray data using score transformation. Journal of Molecular Diagnostics, 5(2):73–81, May 2003.
- [21] Y. Cheng and G. Chung. Clustering of expression data. Proceedings of the Eighth International Conference on Intelligent Systems for Molecular Biology, pages 93–103, 2000.
- [22] S. Datta and S. Datta. Comparisons of statistical clustering techniques for microarray expression data. Bioinformatics, 19(4):459–466, 2003.
- [23] M. J. L. de Hoon, S. Imoto, J. Nolan, and S. Miyano. Open source clustering. Bioinformatics, 20(9):1453–1454, 2004.
- [24] F. De Smet, J. Mathys, K. Marchal, G. Thijs, B. De Meer, and Y. Moreau. Adaptive quality-based clustering of gene expression profiles. Bioinformatics, 18(5):735–746, 2002.
- [25] R. De Smet and K. Marchal. Advantages and limitations of current network inference. Nature Robotics, 8(10):717–729, 2010.
- [26] D. Dembeele and P. Kastner. Fuzzy c-means method for clustering microarray data. Bioinformatics, 19(8):973–980, 2003.
- [27] M. Deodhar, G. Gupta, J. Ghosh, and I. Dhillon. A scalable framework for discovering co-clusters in noisy data. In ICML ’09: Proceedings of the 26th International Conference on Machine Learning, pages 241–248, 2009.
- [28] P. D’haeler, S. Liang, and R. Somogyi. Genetic network inference: From co-expression clustering to reverse engineering. Bioinformatics, 16(8):707–726, 2000.
- [29] I. S. Dhillon, Y. Guan, and B. Kull. Kernel kmeans: Spectral clustering and normalized cuts. Proceedings of the Tenth SIGKDD International Conference on Knowledge Discovery and Data Mining, KDD ’04, pages 551–556, 2004.
- [30] T. Dholander, O. Sheng, K. Lemmens, B. De Meer, K. Marchal, and Y. Moreau. Query-driven module discovery in microarray data. Bioinformatics, 23(19):2573–2580, 2007.
- [31] S. Dongen. A cluster algorithm for graphs. Technical report, CWI (Centre for Mathematics and Computer Science), Amsterdam, The Netherlands, 2000.
- [32] S. Dudoit and J. Fridyland. Bagging to improve the accuracy of a clustering procedure. Bioinformatics, 19(9):1090–1099, 2003.
- [33] M. B. Eisen, P. T. Spellman, P. O. Brown, and D. Botstein. Cluster analysis and display of genome-wide expression patterns. Proceedings of the National Academy of Sciences, 95(25):14863–14868, December 1998.
- [34] A. J. Enricht and C. A. Ouzounis. GeneAGE: A robust algorithm for sequence clustering and domain detection. Bioinformatics, 16(5):451–457, 2000.
- [35] J. Ernst and Z. Bar-Joseph. STEM: a tool for the analysis of time series gene expression data. Bioinformatics, 7(1):191, 2001.
- [36] J. Ernst, G.J. Nau, and Z. Bar-Joseph. Clustering time series gene expression data. Bioinformatics, 21(Suppl 1):i55–i68, 2005.
- [37] G. Fang, R. Kuang, G. Pandey, M. Steinbach, C. L. Myers, and V. Kumar. Subspace differential expression analysis: Problem definition and a general approach. Practical Symposium on Biocomputing, pages 144–156, 2010.
- [38] B. J. Frey and D. Dueck. Clustering by passing messages between data points. Science, 315(5814):972–976, 2007.

