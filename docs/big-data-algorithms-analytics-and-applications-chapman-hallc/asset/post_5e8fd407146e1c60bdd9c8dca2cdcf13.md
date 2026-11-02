
False alarms are discarded by referring to the original data set. Noting the relationship between range and k-NN queries, the latter can be processed as follows [72]:

- (1) Find the k-NNs of the query point Q in the subspace.
- (2) Determine the farthest actual distance to Q among these k points (d_max).
- (3) Issue a range query centered on Q on the subspace with radius ε = d_max.
- (4) For all points obtained in this manner, find their original distances to Q, by referring to the original data set and ranking the points, that is, select the k-NNs.

The exact k-NN processing method was extended to multiple clusters in Reference 30, where we compare the CPU cost of the two methods as the NMSE is varied using two data sets. An offline experiment was used to determine k*, which yields a recall R ≈ 1. The CPU time required by the exact method for a sequential scan is lower than the approximate method, even when R = 0.8. This is attributable to the fact that the exact method issues a k-NN query only once, and this is followed by less costly range queries. Optimal data reduction is studied in the context of the exact query processing [73].

RCSVD was explored in Reference 14 in the context of sequential data set scans. The OP-tree index [2], which is a main memory index, which is suited for k-NN queries, is utilized in Reference 3. Two methods to make this index persistent are described in References 74 and 75. We also proposed a new index, the stepwise dimensionally increasing (SDI) index, which is shown to outperform other indices [74].

## 3.6 ALTERNATE METHOD COMBINING SVD AND CLUSTERING

The LDR method described in Reference 15 generates SVD-friendly clusters so that a higher-dimensionality reduction can be attained for the same NMSE. The description of the LDR method in what follows is based on the appendix in Reference 3.

- 1. Initial selection of centroids. H points with pairwise distances of at least threshold are selected.
- 2. Clustering. Each point is associated to the closest centroid, whose distance is less than ε or ignored otherwise. The coordinates of the centroid are the average of the associated points.
- 3. Apply SVD to each cluster. Each cluster now has a reference frame.
- 4. Assign points to clusters. Each point in the data set is analyzed in the reference frame of each cluster. For each cluster, determine the minimum number of retained dimensions so that the squared error in representing points does not exceed MaxReconDist². The cluster requiring the minimum number of dimensions N_min is determined. If N_min ≤ MaxDim, the point is associated with that cluster, and the required number of dimensions is recorded; otherwise, the point becomes an outlier.
- 5. Compute the subspace dimensionality of each cluster. Find the minimum number of dimensions ensuring that at most, FracOutliers of the points assigned to the cluster in step 4 do not satisfy the MaxReconDist² constraints. Each cluster now has a subspace.
- 6. Recluster points. Each point is associated with the first cluster, whose subspace is at a distance less than MaxReconDist from the point.
- 7. Remove small clusters. Clusters with size smaller than MinSize are removed and the corresponding points reclustered in step 6.
- 8. Recursively apply steps 1-7 to the outlier set. Make sure that the centroids selected in step 1 have a distance at least threshold from the current valid clusters. The procedure terminates when no new cluster is identified.
- 9. Create an outlier list. As in Reference 18, this is searched using a linear scan. Varying the NMSE may yield different compression ratios. The smaller the NMSE, the higher the number of points that cannot be approximated accurately.

The values for H, threshold, ε, MaxReconDist, MaxDim, FracOutliers, and MinSize need to be provided by the user. This constitutes the main difficulty with applying the LDR method. The invariant parameters are MaxReconDist, MaxDim, and MinSize. The method can produce values of H, threshold, and overall FracOutliers, which are significantly different from the inputs. The fact that the LDR method determines the number of clusters is one of its advantages with respect to the k-means method.

The LDR method also takes advantage of LBP [8,72] to attain exact query processing. It produces fewer false alarms by incorporating the reconstruction distance (the squared distance of all dimensions that have been eliminated) as an additional dimension with each point. It is shown experimentally in Reference 3 that RCSVD outperforms LDR in over 90% of cases.

## 3.7 SURVEY OF HIGH-DIMENSIONAL INDICES

Multidimensional indexing has been an active research area in the last two decades [8,16,17,70,76]. Given the distinction between point access methods (PAMs) and spatial access methods (SAMs) [16], we are interested here in PAMs for high-dimensional data. Multidimensional indexing structures can be classified as data partitioning (DP), such as R-trees, similarity search (SS)-trees, and spherical-rectangular (SR)-trees, and space partitioning (SP), such as k-d-B-trees and holey Brick (hB) trees [70]. In DP, space is partitioned in a manner such that regions have an approximately equal number of points. SP divides space into nonoverlapping regions, so that any point in the space can then be identified to lie in exactly one of the regions. Another categorization is disk-resident versus main memory-resident indices. In the former (respectively latter) case, the number of disk pages accessed and CPU time are the major performance measures.

Quad trees [77] and k-d-trees [49] are two early main memory-resident indexing structures. k-d-B-trees combine k-d-trees and B-trees [78]. R-trees [79] were designed to handle spatial data on secondary storage. R\*-trees [80] and R+-trees [81] are two improved versions of R-trees. SS-trees [5] use hyperspheres to partition the space, while SR-trees [82] use the intersection of hyperspheres and hyperrectangles to represent regions. SR-trees outperform both R\*-trees and SS-trees.

*Pyramid trees* [88] are not affected by the curse of dimensionality. The *iMinMax(0)* [89] method, which maps points from high- to single-dimensional space, outperforms pyramid trees in experiments for range queries.

*iDistance* is an efficient method for *k*-NN search in a high-dimensional space [90,91]. Data are partitioned into several clusters, and each partition has a reference point, for example, the centroids of each cluster obtained using the *k*-means clustering method [40]. The data in each cluster are transformed into a single-dimensional space according to the similarity with respect to a reference point. The one-dimensional values of different clusters are disjoint. The one-dimensional space is indexed by a B+ index, and *k*-NN search is implemented using range searches. The search starts with a small radius, but it is increased step by step to form a bigger query sphere. *iDistance* is lossy since multiple data points in the high-dimensional space may be mapped to the same value in the single-dimensional space. The SDI method is compared with the *iDistance* method in Reference 74.

A *vector approximation file* (*VA-file*) represents each data object using the cell into which it falls [9]. Cells are defined by a multidimensional grid, where dimension *i* is partitioned 2^b ways. Due to the sparsity of high-dimensional space, it is very unlikely that several points can share a cell. Nearest neighbor search sequentially scans the VA-file to determine the upper-bound and lower-bound distance from the query to each cell. This is followed by a refinement or filtering step; if the approximate lower bound is greater than the current upper bound, it is not considered further. Otherwise, it is a candidate. During the refine step, all the candidates are sorted according to their lower-bound distances.

A *metric tree* transforms the feature vector space into metric space and then indexes the metric space [92]. A metric space is a pair, ℳ = (ℱ, d), where ℱ is a domain of feature value, and d is a distance function with the following properties:

- 1. Symmetry *d(Fₓ, Fᵧ) = d(Fᵧ, Fₓ)*
- 2. Nonnegativity *d(Fₓ, Fᵧ) > 0, Fₓ ≠ Fᵧ*
- 3. Triangle inequality *d(Fₓ, Fᵧ) ≤ d(Fₓ, F_z) + d(F_z, Fᵧ)*

The search space is organized based on relative distances of objects, rather than their absolute positions in a multidimensional space.

A *vantage point (VP)-tree* [93] partitions a data set according to distances between the objects and a reference or vantage point. The corner point is chosen as the vantage point, and the median value of the distances is chosen as separating radius to partition the data set into two balanced subsets. The same procedure is applied recursively on each subset. The *multiple vantage point (mvp)-tree* [94] uses precomputed distances in the leaf nodes to provide further filtering during search operations. Both trees are built in a top-down manner; balance cannot be guaranteed during insertion and deletion. Costly reorganization is required to prevent performance degradation.

An *M-tree* is a paged metric-tree index [95]. It is balanced and able to deal with dynamic data. Leaf nodes of an M-tree store the feature vectors of the indexed objects O_j and distances
