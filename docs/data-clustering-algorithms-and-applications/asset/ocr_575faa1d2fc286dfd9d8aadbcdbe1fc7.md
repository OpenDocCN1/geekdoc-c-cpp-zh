# Time-Series Data Clustering

to classification or clustering tasks. According to the Liao classification, the algorithm of Vlachos et al. is placed in the feature-based category, as it operates on a reduced-dimensionality approximation of the original time series using the Haar wavelet basis. In [36] the researchers describe an extension to the work presented in [53], where the same approach is followed, in this work with Expectation Maximization (EM) method serving the clustering process. EM is more a soft version of *k-means* than a fundamentally different approach, in the sense that each object has a degree of membership in each cluster, whereas *k-means* each object must belong to exactly one cluster. The major difference between EM and *k-means* is that EM produces a richer variety of cluster shapes than *k-means*, which favors spherical clusters.

# 15.5.2 Hierarchical Clustering

There are two types of hierarchical clustering, *agglomerative* and *divisive*. Agglomerative clustering starts by regards each data object as a different cluster and continues by searching the most similar pair of clusters. The most similar pair is merged into one cluster and the process continues until the desired number of clusters is reached.

+   * Single linkage: In single linkage selection, the distance between two clusters is defined as the shortest distance among all their member objects. Specifically, the single-link distance between clusters $C_i$ and $C_j$ is the following:

```
$$$D_{SL}(C_i, C_j) = \min_{x \in C_i, y \in C_j}(\text{dist}(x,y)) \quad (15.5)$$
```

where $dist$ is the chosen distance measure.

+   * Complete linkage: In complete linkage selection, the distance between two clusters is defined as the longest distance among all their member objects. Specifically, the complete-link distance between clusters $C_i$ and $C_j$ is the following:

```
$$$D_{CL}(C_i, C_j) = \max_{x \in C_i, y \in C_j}(\text{dist}(x,y)) \quad (15.6)$$
```

where $dist$ is the chosen distance measure.

+   * Average linkage: In average linkage selection, the distance between two clusters is defined as the average distance among all their member objects. Specifically, the average-link distance between clusters $C_i$ and $C_j$ is the following:

```
$$$D_{AV}(C_i, C_j) = \text{avg } x \in C_i, y \in C_j(\text{dist}(x,y)) \quad (15.7)$$
```

where $dist$ is the chosen distance measure.

*Divisive* hierarchical clustering is the inverse process of agglomerative hierarchical clustering in that it starts by regards the whole dataset as a single cluster and continues by recursively dividing into smaller ones.

Hierarchical clustering has better visualization capabilities than *k-means*, as the clustering forms a dendrogram. To *k-means*, it takes no parameters and can be stopped and traced back at any point to the desired level. Its major drawback is its quadratic computational complexity which makes hierarchical clustering practically useful only for small datasets. As opposed to *k-means clustering*, the hierarchical algorithm is a deterministic algorithm, which means when applied on the same dataset it provides the same results in every run.