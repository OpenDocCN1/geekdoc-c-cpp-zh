based on the subspaces found. FINDIT employs sampling techniques like the other top-down algorithms to improve performance with very large data sets.

The δ-clusters algorithm uses a distance measure to capture the coherence exhibited by a subset of instances on a subset of attributes [66]. Coherent instances may not be close, but instead, both follow a similar trend, offset from each other. One coherent instance can be derived from another by shifting by an offset. The algorithm starts with initial seeds and iteratively improves the overall quality of the clustering by randomly swapping attributes and data points to improve individual clusters. Residue measures the decrease in coherence that a particular entry (attribute or instance) brings to the cluster. The iterative process terminates when individual improvement levels off in each cluster.

Clustering on Subsets of Attributes (COSA) assigns weights to each dimension for each instance, not each cluster [67]. Starting with equally weighted dimensions, the algorithm examines the k-NNs of each instance. These neighborhoods are used to calculate the respective dimension weights for each instance, with higher weights assigned to those dimensions that have a smaller dispersion within the k-NN group. These weights are used to calculate dimension weights for pairs of instances, which are used to update the distances used in the k-NN calculation. The process is repeated using the new distances until the weights stabilize. The neighborhoods for each instance become increasingly enriched with instances belonging to its own cluster. The dimension weights are refined as the dimensions relevant to a cluster receive larger weights. The output is a distance matrix based on weighted inverse exponential distance and is suitable as input to any distance-based clustering method. After clustering, the weights for each dimension of cluster members are compared, and an overall importance value for each dimension is calculated for each cluster.

There are many others, which are reviewed in Reference 61. The multilevel Mahalanobis-based dimensionality reduction (MMDR) [68] clusters high-dimensional data sets using the low-dimensional subspace based on the Mahalanobis rather than the Euclidean distance, since it is argued that locally correlated clusters are elliptical shaped. The Mahalanobis distance uses different coefficients according to the dimension [8].

# 3.4 STEPS IN BUILDING AN INDEX FOR k-NN QUERIES

The following steps were followed combining SVD and clustering in References 3 and 14 for building the data structures to carry out k-NN queries.

+   1. Selecting an objective function in step 1
+   2. Selecting the number of clusters in step 2
+   3. Partitioning the data set of points in step 3
+   4. Rotating each partition into an uncorrelated frame of reference in step 4
+   5. Reducing the dimensionality of the partitions in step 5
+   6. Constructing the within-cluster index in step 6