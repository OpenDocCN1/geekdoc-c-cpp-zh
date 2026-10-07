
![](img/b94d85a2e934001944bcc21abd9a9943_324_0.png)

FIGURE 12.9: A Support Vector Machine tries to maximize the margin of separation between the hyperplane and the training data, which typically consists of samples from two classes. SVMs have been previously used for clustering. After the SVM is trained, new objects are predicted to belong to a class (as defined by the separating hyperplane) according to a measure of the distance between the testing data and the hyperplane.

have switched to the other class label. The SVM is retrained after each relabeling of the low confidence objects. This continues until no more progress can be made. Progress is determined by an increasing value of sensitivity+specificity, nearly reaching 2. The repetition of the above process limits local minima traps [72].

The SVM clustering approach provides a way to cluster datasets without prior knowledge of the data’s clustering characteristics or the number of clusters. This method is not biased towards the shape of the clusters, and unlike the SVM-Internal Clustering approach the formulation is not fixed to a single kernel class. Nevertheless, there are robustness and consistency issues that arise in realistic applications of SVM-External Clustering.

## 12.5 Conclusion

Desired features of categorical clustering algorithms for different applications include speed, minimal parameters, robustness to noise and outliers, redundancy handling, and object order dependence. Desirable clustering features are used as evaluation criteria for clustering algorithms. Categorical clustering algorithms are separated into various approaches: partitioning (e.g., $k$-Modes),

hierarchical (e.g., ROCK, Chameleon, LIMBO), density-based (e.g., MULIC, CACTUS, CLICKS, CLPE), model-based (e.g., COBWEB, Autoclass). Some algorithms can handle categorical and numerical data (k-Prototypes, BILCOM). Within an approach, inheritance relationships between clustering algorithms summarize common features and improvements they make upon another. Table 12.1 and 12.2 summarize benefits and drawbacks of categorical clustering algorithms. For improved analysis of categorical datasets, it is important to match clustering algorithms to the requirements of an application.

The benefits and drawbacks of categorical clustering algorithms can be a basis for matching them to an application. Speed and accuracy are two competing goals in the design of categorical clustering algorithms. Making a fast algorithm usually involves trading off precision of the result. On the other hand, producing the most accurate result is not necessarily easy. A set of probabilistically justified goals for categorical clustering would serve as a framework for approximation algorithms [54, 63]. This would allow designing and comparing categorical clustering algorithms on a more formal basis.

## Bibliography

- [1] B. Adryan and R. Schuhl. Gene ontology-clustering of gene expression data. Bioinformatics 20(16):2851–2852, 2004.
- [2] C. Aggawal, J. Han, W. Wang, and P. S. Yu. A framework for projected clustering of high dimensional data. In Proceedings of the 30th VLDB Conference (VLDB '04), Toronto, Canada, pages 852–863, 2004.
- [3] C. Aggawal and P. S. Yu. Finding generalized clusters in high dimensional spaces. In Proceedings of the SIGMOD, 70–81, 2000.
- [4] R. Agrawal, J. Gehrke, D. Gunopoulos, and P. Raghavan. Automatic subspace clustering of high dimensional data for data mining applications (1998). In Proceedings ACM-SIGMOD '98 International Conference on Management on Data, pages 94–105. Seattle, Washington, June 1998.
- [5] H. Akaike. A new look at statistical model identification. IEEE TAC 19:716–723, 1974.
- [6] M. R. Anderberg. Cluster Analysis for Applications. Academic Press, New York, 1973.
- [7] B. Andropoulos. Clustering algorithms for categorical data. PhD Thesis, Department of Computer Science & Engineering, University Toronto, Toronto, Canada, 2006.
- [8] B. Andropoulos, An, V. Tzeropos, and X. Wang. Clustering large software systems at multiple layers. Elsevier Information and Software Technology (IST) 49(3):244–254, 2007.
- [9] B. Andropoulos, An, V. Tzeropos, and X. Wang. Multiple layer clustering of large software systems. In Proceedings of the 12th IEEE Working Conference on Reverse Engineering (WCRE 2005), pages 79–88, Pittsburgh, PA (Carnegie Mellon), November 2005.
- [10] B. Andropoulos, An and X. Wang. Bi-level clustering of mixed categorical and numerical biomedical data. International Journal of Data Mining and Bioinformatics (IJDMB) 1(1):19–56, 2006.

## Data Clustering: Algorithms and Applications

- [11] B. Andreopoulos, A. An, and X. Wang. Finding molecular complexes through multilayer clustering of protein interaction networks. International Journal of Bioinformatics Research and Applications (IJBRA) 3(1):65–85, 2007.
- [12] B. Andreopoulos, A. An, and X. Wang. Hierarchical density-based clustering of categorical data and a simplification. In Proceedings of the 11th Pacific-Asia Conference on Categorical Discovery and Data Mining (PKDD 2007), Springer LNCS 4426/2007, pages 11–22, Nanjing, May 22–25, 2007.
- [13] B. Andreopoulos, A. An, X. Wang, M. Faloutos, and M. Schroeder. Clustering by common finds locally localating protein mediating molecules. Bioinformatics 23(9):1124–1131, 2007.
- [14] B. Andreopoulos, A. An, X. Wang, and D. Labutte. Efficient layered density-based clustering of categorical data. Elsevier Journal of Biomedical Informatics 42(2):365–376, 2009.
- [15] B. Andreopoulos, A. An, X. Wang, and M. Schroeder. Roadmap of clustering algorithms: finding a match for a biomedical application. Briefings in Bioinformatics 10(3):297–314, 2009.
- [16] P. Andritsos, P. Tsaras, R. Miller, et al. LIMBO: Scalable clustering of categorical data. In Proceedings of the 9th International Conference on Extending Database Technology EDB’04, pages 123–146, Heraklion, Greece. March 14–18, 2004.
- [17] M. Ankert, M. Breunig, H.P. Kriegel, and J. Sander. OPTICS: Ordering points to identify the clustering structure. SIGMOD, 49–60, 1999.
- [18] G. Baker and C. Hogue. An automated method for finding molecular complexes in large protein interaction networks. BMC Bioinformatics 4(2), 2003.
- [19] D. Barbara, Y. Li, and J. Couto. COOLCAT: An entropy-based algorithm for categorical clustering. In Proceedings of CIK 2002, pages 582–589, 2002.
- [20] R. Bellazzi and B. Zupan. Towards knowledge-based gene expression data mining. Journal of Bioinformatics 40(6):777–802, 2007.
- [21] P. Perkins. Survey of Clustering Data Techniques. Accrue Software, Inc. report. San Jose, CA. 2002.
- [22] S. Boriah, V. Chandola, and V. Kumar. Similarity measures for categorical data: A comparative evaluation. In Proceedings of the Eighth SIAM International Conference on Data Mining, pages 243–254, 2008.
- [23] D. Brown. Efficient functional clustering of protein sequences using the Dirichlet process. Bioinformatics 24(16):1765–1771, 2008.
- [24] M. Brown, W. Grundy, D. Lin D, et al. Knowledge-based analysis of microarray expression data by using support vector machines. PNAS 97(1):262–267, 2000.
- [25] T. Burnaby. On a method for weighing a similarity coefficient, employing the concept of information. Mathematical Geometry 2(1):25–38, 1990.
- [26] G. Das and H. Mannila. Context-based similarity measures for categorical databases. In Proceedings of PKDD 2000, 24th European Conference on Principles of Data Mining and Knowledge-Discovery, Pages 201–210, Springer-Verlag, London, UK, 2000.

## Clustering Categorical Data

- [27] Z. Dezso, Z.N. Oltvai, and A.L. Barabas. Bioinformatics of experimentally protein complexes in the yeast Saccharomyces cerevisiae. Genome Research 13, 2450–2454, 2003.
- [28] C. Ding, X. He, H. Za. Adaptive dimension reduction for clustering high dimensional data. In Proceedings of ICDM 2002, pages 107–114, 2002.
- [29] M. Ester, H.P. Kriegel, J. Sander, X. Xu. A density-based algorithm for discovering clusters in large spatial databases with noise. KDD pages 226–231, 1996.
- [30] G. Even, J. Naor, S. Rao, and B. Schiefer. Fast approximate graph partitioning algorithms. SIAM Journal on 28(6):2187–2214, 1999.
- [31] Fisher D. Knowledge acquisition via incremental conceptual clustering. Machine Learning 2:139–172, 1987.
- [32] V. Ganti, J. Gehrke, and R. Ramakrishnan. CACTUS-clustering categorical data using summaries. In Proceedings of KDD'99 pages 73–83, San Diego, CA, US, 1999.
- [33] I. Gat-Viks, R. Sharan, and R. Shamir. Scoring clustering solutions by their biological relevance. Bioinformatics 19(18):2381–2389, 2003.
- [34] D. Gibson, J. Kleiberg, and P. Raghavan. Clustering categorical data: An approach based on dynamical systems. In Proceedings of 24th International Conference on Very Large Databases (VLDB'98), pages 311–332, New York City, US, August 24–27, 1998.
- [35] A. Gionis, A. Hinneburg, P. Papadimitriou, and P. Tsaras. Dimension induced clustering. In Proceedings of KDD'05, pages 1–60, 2005.
- [36] D. W. Goodall. A new similarity index based on probability. Biometrics 22(4):882–907, 1996.
- [37] A. D. Gordon. Classification, 2nd Edition. London: Chapman and Hall CRC, 1999.
- [38] J. Grambeier and A. Rudolph. Techniques of cluster algorithms in data mining. Data Mining and Knowledge Discovery 6:303–360, 2002.
- [39] S. Guha, R. Rastogi, and K. Shim. ROCK: A Robust clustering algorithm for categorical attributes. Information Systems 25(5): 345–366, 2000.
- [40] S. Guha, R. Rajeev, and S. Kyuseok. CURE: An efficient clustering algorithm for large databases. In Proceedings of ACM SIGMOD '98, pages 73–84, Seattle, US, 1998.
- [41] J. Han and M. Kara. Data Mining: Concepts and Techniques, 2nd edition, Morgan Kaufmann, 2006.
- [42] J. A. Hartigan. Clustering Algorithms. New York: Wiley. 1975.
- [43] Z. He, X. Xu, S. Deng et al. Squeezer: An efficient algorithm for clustering categorical data. Journal of Computer Science and Technology 17(5):611–624, 2002.
- [44] A. Hinneburg and D.A. Keim. An efficient approach to clustering in large multimedia databases with noise. KDD, 55–68, 1999.
- [45] D. Huang and W. Pan. Incorporating biological knowledge to distance-based clustering analysis of microarray gene expression data. Bioinformatics 22(10):1259–1268, 2006.
- [46] Z. Wang. Clustering large data sets with mixed numeric and categorical values. Knowledge discovery and data mining: Techniques and applications. World Scientific, 1997.
