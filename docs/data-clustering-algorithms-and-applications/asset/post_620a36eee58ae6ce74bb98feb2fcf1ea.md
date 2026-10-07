
[72] M. Steeyers and S. Griffiths. Probabilistic topic models. In S. D. T. Landauer, D McNamara, and W. Kintsch, Latent Semantic Analysis: A Road to Meaning. Laurence Erlbaum, 2006.

[73] M. Steeyers, P. Smyth, M. Rosen-Zvi, and T. L. Griffiths. Probabilistic author-topic models for information discovery. In KDD, pages 306–315, 2004.

[74] Y. W. Teh, M. I. Jordan, M. J. Beal, and D. M. Blei. Clustering among related groups: Hierarchical dirichlet processes. In NIPS, 2004.

[75] D. Titterington, A. Smith, and M. Makov. Statistical Analysis of Finite Mixture Distributions, volume 38. John Wiley & Sons, 1985.

[76] N. Ueda and R. Nakano. Deterministic annealing EM algorithm. Neural Networks, 11(2):271–282, 1998.

[77] N. Ueda, R. Nakano, Z. Ghahramani, and G. Hinton. SMEM algorithm for mixture models. Neural Computation, 12(9):2109–2128, 2000.

[78] M. J. Wainwright and M. I. Jordan. Graphical models, exponential families, and variational inference. Foundations and Trends in Machine Learning, 1(1–2):1–305, 2008.

[79] C. Wallace and D. Dowe. Minimum message length and Kolmogorov complexity. The Computer Journal, 42(4):270–283, 1999.

[80] H. Wallach. Topic modeling: Beyond bag-of-words. In Proceedings of the 23rd international Conference on Machine Learning, pages 977–984. ACM, 2006.

[81] S. Zhong and J. Ghosh. Generative model-based document clustering: A comparative study. Knowledge and Information Systems, 8(3):374–384, 2005.

# Chapter 4

# A Survey of Partitional and Hierarchical Clustering Algorithms

Chandan K. Reddy
Wayne State University
Detroit, MI
reddy@cs.wayne.edu

Bhanukiran Vinzamuri
Wayne State University
Detroit, MI
bhanukiri.ranv@wayne.edu

- 4.1 Introduction ............................................................................................................................................................ 88
- 4.2 Partitional Clustering Algorithms ................................................................................................................................. . . 89
    - 4.2.1 K-Means Clustering ................................................................................................................................................. . . . 89
    - 4.2.2 Minimization of Sum of Squared Errors ................................................................................................................ 90
    - 4.2.3 Factors Affecting K-Means ..................................................................................................................................................... . . 91
        - 4.2.3.1 Popular Initialization Methods ............................................................................................................................................ . . 91
        - 4.2.3.2 Estimating the Number of Clusters .................................................................................................................................... . . 92
    - 4.2.4 Variations of K-Means ................................................................................................................................................................... . 93
        - 4.2.4.1 K-Medoids Clustering ........................................................................................................................................................ . . 93
        - 4.2.4.2 K-Medians Clustering ........................................................................................................................................................ . . 94
        - 4.2.4.3 K-Modes Clustering ....................................................................................................................................................................... . . 95
        - 4.2.4.4 Fuzzy K-Means Clustering ..................................................................................................................................... . . 95
        - 4.2.4.5 X-Means Clustering ....................................................................................................................................................................... . . 95
        - 4.2.4.6 Intelligent K-Means Clustering ...................................................................................................................................... . . 96
        - 4.2.4.7 Bisecting K-Means Clustering ...................................................................................................................................... . . 97
        - 4.2.4.8 Kernel K-Means Clustering ................................................................................................................................... . . 97
        - 4.2.4.9 Mean Shift Clustering ........................................................................................................................................................ . . 98
        - 4.2.4.10 Weighted K-Means Clustering ......................................................................................................................................... . . . 98
        - 4.2.4.11 Genetic K-Means Clustering ................................................................................................................................... . . . 99
    - 4.2.5 Making K-Means Factors ..................................................................................................................................................................... . 100
- 4.3 Hierarchical Clustering Algorithms ................................................................................................................................... . 100
    - 4.3.1 Agglomerative Clustering ..................................................................................................................................................... . . . 101
        - 4.3.1.1 Single and Complete Link .......................................................................................................................................... . . 101
        - 4.3.1.2 Group Averaged and Centroid Agglomerative Clustering ................................................................................ . . 102
        - 4.3.1.3 Ward's Criterion ................................................................................................................................................... . . 103
        - 4.3.1.4 Agglomerative Hierarchical Clustering Algorithm ....................................................................................... . . 103
        - 4.3.1.5 Lance-Williams Dissimilarity Update Formula ...................................................................................... . . 103
    - 4.3.2 Divisive Clustering ................................................................................................................................................... . . 104
        - 4.3.2.1 Issues in Divisive Clustering .................................................................................................................------- . . 104
        - 4.3.2.2 Divisive Hierarchical Clustering Algorithm ...................................................................................................... . . 105
        - 4.3.2.3 Minimum Spanning Tree-Based Clustering ................................................................................................... . . 105
- 4.3.3 Other Hierarchical Clustering Algorithms 106
- 4.4 Discussion and Summary 106
- Bibliography 107

# 4.1 Introduction

The two most studied clustering algorithms are partitional and hierarchical clustering. These algorithms have been heavily used in a wide range of applications primarily due to their simplicity and ease of implementation relative to other clustering algorithms. Partitional clustering algorithms aim to discover the groupings present in the data by optimizing a specific objective and iteratively improving the quality of the partitions. These algorithms generally require user parameters to choose the prototype points that represent each cluster. For this reason they are called prototype-based clustering algorithms.

Hierarchical clustering algorithms, on the other hand, approach the problem of clustering by developing a binary tree-based structure called the dendrogram. Once the dendrogram is constructed, one can automatically choose the right number of clusters at the tree at different levels to obtain different clustering solutions for the same dataset without rerunning the algorithm. Hierarchical clustering can be achieved in two different ways, namely, bottom-up and top-down clustering. Though both of these approaches utilize the dendrogram while clustering the data, they may yield entirely different sets of results depending on the criterion used during clustering process.

Partial methods need to be provided with a set of initial seeds (or clusters) which are improved iteratively. Hierarchical methods, on the other hand, can start with the individual data points in single clusters and build the clustering. The role of the distance metric is also different in both of these algorithms. In hierarchical clustering, the distance metric is initially applied on the data points at the base level and then progressively applied on subclusters by choosing absolute representative points for the subclusters. In the case of partial methods, in general, the representative points chosen at different iterations can be virtual points such as the centroid of the cluster (which is nonexistent in the data).

This chapter is organized as follows. In Section 4.2, the concepts of partial clustering are introduced and the related algorithms in this field are discussed. More specifically, Subsections 4.2.1–4.2.3 will discuss the widely studied K–Means clustering algorithm and highlight the major factors involved in these algorithms such as initialization methods and estimating the number of clusters. Subsection 4.2.4 will highlight the distinctive features of each of these algorithms and their advantages are also featured. Section 4.3.1 and 4.3.2 will discuss the agglomerative and divisive hierarchical clustering algorithms, respectively. We will also highlight the differences between the algorithms in both of these categories. Subsection 4.3.3 will briefly discuss the other prominent hierarchical clustering algorithms. Finally, in Section 4.4, we will conclude our discussion highlighting the merits and drawbacks of both families of clustering algorithms.
