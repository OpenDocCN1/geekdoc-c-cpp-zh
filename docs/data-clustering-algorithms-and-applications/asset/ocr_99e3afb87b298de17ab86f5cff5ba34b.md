# Data Clustering: Algorithms and Applications

![](bbox=[0.247, 0.098, 0.752, 0.373])

The paradigm of density-based clustering has been proposed to address all of these requirements. Density-based clustering can be considered as a non-parametric method, as it makes no assumptions about the number of clusters or their distribution.

Density-based clusters are connected, dense areas in the data space separated from each other by sparser areas. Furthermore, the density within the areas of noise is assumed to be lower than the density in any of the clusters. Given an index structure that supports query regions, density-based clusters can be efficiently computed by performing at most one region query per database object. Sparse areas in the data space are treated as noise and are not assigned to any cluster.

It is worth noting that the algorithms that have been referred to in the literature of density-based clustering have various predecessors that have already explored some of the ideas. In particular, Wishart [33] explored ways to avoid the so-called chaining effect in single-link clustering, which is caused by a small number of noisy data points that connect sets of points that in principle form separate clusters. First, nondense points, that have fewer than k neighbors within a distance of r, are removed. Second, single-link clustering is employed to cluster the remaining points. Finally, nondense points may be allocated to one of the clusters according to some criterion. We would also like to point out the relationship between the paradigms of density-based clustering and mean-clustering [8].

The mean shift procedure is an iterative procedure that replaces each point by the weighted mean of its neighboring points, where the weight is determined by some kernel function, and it converges to the nearest stationary point of the underlying density function. Mean shift clustering, where narrow clusters create singleton clusters, while wide clusters create one, and intermediate clusters create a natural number of clusters. As opposed to density-based clustering, in mean-shift clustering, the neighborhood membership is weighted (is instead of Boolean), the minimum number of points does not need to be specified, and there is no guarantee that clusters are connected.

A density-based clustering algorithm needs to answer several key questions:

+   - How is the density estimated?

FIGURE 5.1: k-means with k = 3 on a sample 2-dimensional dataset.

© 2014 by Taylor & Francis Group, LLC