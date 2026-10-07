
# Feature Selection for Clustering: A Review

## 2.3.4 Stability

In supervised learning such as classification, stability of feature selection algorithms has gained increasing attention theover the last few years. Stability of feature selection algorithms or selection stability is the sensitivity of the selection toward data perturbation? An example of data perturbation would be a new data sample(s). Therefore, with a small amount of perturbation introduced to the data, we do not expect dramatic change in the selected features. Otherwise, the algorithm is considered to be unstable. To the best of our knowledge, selection stability in unsupervised learning has not yet been studied.

Studying stability in unsupervised learning is much easier than in the unsupervised. Due to absence of class within the label, we cannot know enough about the underlying clusters within the data. For this reason, we cannot be confident whether the new sample(s) belong to any existing clusters or they form one or more clusters. However, in supervised learning, we have a limited number of classes. Thus, a sample that does not belong to any existing class would be considered an outlier and we do not need to modify our selected set to obey outliers. So, to address the issue of feature selection stability in clustering, we discuss it with respect to a different situation.

## Predefined Clusters:

In case we have enough domain knowledge to define the possible clusters, the stability issue will be identical to the stability in supervised learning. Therefore, we expect the feature selection algorithm to be stable with the existence of a small amount of perturbation. However, if the topics do not change the data change, we might consider unstable selection.

## Undefined Clusters:

In contrast to the first case, if we do not have know about the clusters of the data, which is true in real-world situations, we generally can say that this case depends on the domain and the practitioner's desire. In streaming data, for example, we expect some kind of dataset shift or drift where the distribution and the clustering topics of the data may evolve over time. Therefore, we should have an adaptive evolving feature selection process that adjusts the features in a way that can capture the evolving structure of the data. However, we might need a stable selection for a period of time and an unstable for one period. For example, in news data clustering, we wish to have stable selection while we are not breaking news that takes the distribution to different topic.

On the other hand, subspace and projected clustering may not promote stability since they search for all possible sets of features that define clusters. In some cases, we might want to maintain stable selection on some clusters but unstable on others. For instance, if we are performing projected clustering on news data, we may want to have stable selection on clusters that do not evolve rapidly while having unstable on rapidly evolving clusters.

## Bibliography

- [1] C.C. Aggrawal, J. Han, J. Wang, and P.S. Yu. A framework for clustering evolving data streams. In Proceedings of the 29th International Conference on Very Large Data Bases—Volume 29, pages 81–92. VLDB Endowment, 2003.
- [2] C.C. Aggrawal, J. Han, J. Wang, and P.S. Yu. A framework for projected clustering of dimensional data streams. In Proceedings of the Thirtieth International Conference on Very Large Data Bases-Volume 30, pages 852–863. VLDB Endowment, 2004.
- [3] C.C. Aggarwal, J.L. Wolf, P.S. Yu, C. Prokopuc, and J.S. Park. Fast algorithms for projected clustering. ACM SIGMOD, 28(2):61–72, 1999.
- [4] T.M. Akhriz, Y. Ma, and J.L. Li. Clustering using frequent contextual term. In 2011 International Conference on Information Management, Innovation Management and Industrial Engineering (ICII), Volume 1, pages 339–342. IEEE, 2011.
- [5] S. Alelyani, W. Wang, and H. Liu. The effect of the characteristics of the dataset on the selection stability. In Proceedings of the 23rd IEEE International Conference on Tools with Artificial Intelligence, 2011.
- [6] F. Beil, M. Ester, and X. Xu. Frequent term-based clustering. In Proceedings of the Eighth ACM SIGKDD International Conference on Knowledge Discovery and Data Mining, pages 436–442. ACM, 2002.
- [7] C. Bousaidis, M.W. Mahoney, and P. Draneas. Unsupervised feature selection for the k-means clustering problem. Advances in Neural Information Processing Systems, 22:153–161, 2009.
- [8] P.S. Bradley and O.L. Mangasarian. Feature selection via concave minimization and support vector machines. pages 82–90. Morgan Kaufmann, 1998.
- [9] D. Cai, C. Chang, and X. He. Unsupervised feature selection for multi-cluster data. In Proceedings of the 16th ACM SIGKDD International Conference on Knowledge Discovery and Data Mining, pages 333–340. ACM, 2010.
- [10] A. Carvalho, R.F. Melo, S. Alelyani, H. Liu. Quantifying features using false nearly neighbors: an unsupervised approach. In Proceedings of the 2nd IEEE International Conference on Tools with Artificial Intelligence (ICTAI), pages 994–997. IEEE, 2011.
- [11] G. C. Cvalley, N. L. Talbot, and M. G. Sparse logistic regression. NIPS, 2006.
- [12] S. Das. Filters, wrappers and hybrid. In Proceedings of the Eighteenth International Conference on Machine Learning, pages 74–81. San Francisco, CA, 2001.
- [13] M. Das, K. Choi, and Y. G. Correlation-based feature selection. In Proceedings of Data Mining, pages 115–122, 2003.
- [14] S. G. Sparse k-means algorithm using noisy data. In 23rd IEEE International Conference on Artificial Intelligence (ICTAI), pages 869–872. IEEE, 2011.
- [15] R. O. Text clustering. 2nd edition. John Wiley, 2001.
- [16] J. G. Dy and C. E. Feature selection for unsupervised learning. Journal of Machine Research, 3:845–889, 2004.
- [17] J. G. Dy. Feature selection selection in unsupervised learning. In Proceedings of the 17th International Conference, pages 247–254. 2000.
- [18] M. G. Localized feature selection. Computational Methods of, 9:15–39, 2008.

# Data Clustering: Algorithms and Applications

## Feature Selection for Clustering: A Review

- [19] B. C, Y. S. Text clustering based on frequent word. Pattern Recognition Letters, 29:59–70, 2003.
- [20] L. Gong, M.K. Ng, and Z. Li. Text clustering with feature selection. Data & Knowledge Engineering, 38(3):1393–1399, 2011.
- [21] I. Guyon and A. Hall. Feature subset selection. Journal of Machine Research, 6:1157–1182, 2003.
- [22] R. Kohavi and G. H. Wrappers for feature subset selection. Artificial Intelligence, 97(1997):273–324.
- [23] T. Hastie, R. Tibirani, and J. Friedman. The Elements of Statistical Learning. Springer, 2001.
- [24] X. He, D. Cai, and P. N. Laplace score for feature selection. Advances in Neural Information Processing Systems, 18:507, 2006.
- [25] J.Z. Huang, M.K. Ng, and S. Li. Automated k-means algorithm. IEEE Transactions on Pattern Analysis and Machine Intelligence, 27(5):657–668, 2005.
- [26] A. Jain and D. Zong. Feature selection for. IEEE Transactions on Pattern Analysis and Machine Intelligence, 19:153–158, 1997.
- [27] D. Jensen and J. Neville. Linkage and autocorrelation. In ICML, 255–266, 2002.
- [28] L. Ling, M.K. Ng, and J.Z. Huang. An entropy weighting k-means clustering of high-dimensional. IEEE Transactions on Knowledge and Data Engineering, 19(8):1026–1041, 2003.
- [29] T. Joachsims. Text categorization with support vector machines: Learning with many features, 1997.
- [30] Y.S. Kim, W. Street, and F. Menczer. Evolutionary model selection in unsupervised learning. Intelligent Data Analysis, 6(6):531–556, 2002.
- [31] Y. Li, S.M. Chung, and J.D. Holt. Text clustering based on frequent word sequences. Data & Knowledge Engineering, 64(1):381–404, 2008.
- [32] Y. Li, C. Luo, and J. Hua. Localized feature selection for clustering using statistical data. Pattern Recognition Letters, 29:10–18, 2008.
- [33] Y. Li, C. Luo, and S.M. Chung. Text clustering with feature selection by. IEEE Transactions on Knowledge and Data Engineering, 20(5):641–652, 2008.
- [34] H. Liu and H. Motoda, editors. Computational Methods of Feature Selection. Chapman and Hall/CRC Press, 2007.
- [35] H. Liu and H. Motoda. Feature Selection for Knowledge Discovery and Data Mining. Kluwer Academic Publishers, 1998.
