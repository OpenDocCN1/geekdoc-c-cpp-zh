
- 1. Distance defined as \((D_{\max} - D_{\min})/D_{\min}\), where \(D_{\max}\) and \(D_{\min}\) are the points with the farthest and least distance from a target point, decreases with increasing dimensionality. Setting \(0 \le p \le 1\) has been proposed in References 37 and 38 to provide more meaningful distance measures.
- 2. Clusters are intended to group objects based on attribute values, but some of the large number of attributes may not be meaningful for a given cluster. This is known as the local feature relevance problem: Different clusters might be found in different subspaces.
- 3. Subsets of attributes might be correlated; hence, clusters might exist in arbitrarily oriented affine subspaces (in affine geometry, the coordinates are not necessarily orthonormal).
- 4. Problem 4 is similar to problem 3 in that there may be some correlations among subsets of attributes.

\[
D(u, v) = \left( \sum_{i=1}^{n} |u_i - v_i|^p \right)^{1/p}. \tag{3.6}
\]

\(p = 1\) yields the Manhattan distance and \(p = 2\) the Euclidean distance.

Given \(n\) points and \(k\) clusters, the number of possible clusters is a Stirling number of the second kind defined as follows:

\[
S(n, k) = {n \brace k} = \frac{1}{k!} \sum_{t=0}^{k} (-1)^t \binom{k}{t} (k - t)^n.
\]

\(S(n, 1) = S(n, n) = 1\), \(S(4, 2) = 7\) because there are seven ways to partition four objects, \(a, b, c, d\), into two groups: \((a)(bcd)\), \((b)(acd)\), \((c)(abd)\), \((d)(abc)\), \((ab)(cd)\), \((ac)(bd)\), \((ad)(bc)\).

Recursion can be used to compute \(S(n, k) = k S(n - 1, k) + S(n - 1, k - 1)\), \(1 \le k < n\), and to show that \(S(n, k)\) increases rapidly, for example, \(S(10, 5) = 42525\). Cluster analysis can be classified into the following methods.

### 3.3.1 Partitioning Methods

Partition \(n\) data points based on their distances from each other into \(k\) clusters. Each cluster has at least one point, and each point belongs to one cluster, unless a fuzzy clustering algorithm is considered, in which case the allocation of data points to clusters is not all or nothing [39]. In fact, the *expectation maximization (EM)* method provides soft assignment of points to clusters, such that each point has a probability of belonging to each cluster.

\(k\)-means is a good example of partitioning-based clustering methods, which can be specified succinctly as follows [40]:

- 1. Randomly select \(H\) points from the data set to serve as preliminary centroids for clusters. Centroid spacing is improved by using the method in Reference 41.
- 2. Assign points to the closest centroid based on the Euclidean distance to form \(H\) clusters.
- 3. Recompute the centroid for each cluster.
- 4. Go back to step 2, unless there is no new reassignment.

The quality of the clusters varies significantly from run to run, so that the clustering experiment is repeated and the one yielding the smallest *sum of squares (SSQ)* distances to the centroids of all clusters is selected:

\[
SSQ = \sum_{h=1}^{H} \sum_{i \in C^{(h)}} \sum_{j=1}^{N} \left(x_{i,j} - c_j^{(h)}\right)^2. \tag{3.7}
\]

\(C^{(h)}\) denotes the \(h\)th cluster, with centroid \(C_h\) with coordinates given by \(c^{(h)}\) and radius \(R^h\), which is the distance of the farthest point in the cluster from \(C_h\). SSQ decreases with increasing \(H\), but a point of diminishing returns is soon reached. The \(k\)-means clustering method does not scale well to large high-dimensional data sets [42].

Clustering Large Applications Based on Randomized Search (CLARANS) [43] extends Clustering Large Applications (CLARA), described in Reference 33. Clustering is carried out with respect to representative points referred to as medoids. This method, also known as \(k\)-medoids, is computationally expensive because (1) each iteration requires trying out new partitioning representatives through an exchange process and (2) a large number of passes over the data set may be required. CLARANS improves efficiency by performing iterative hill climbing over a smaller sample.

### 3.3.2 Hierarchical Clustering

This is also called connectivity-based clustering since it connects objects to form clusters based on their distance. Hierarchical clustering methods fall into two categories:

- 1. Agglomerative or bottom up, where at first, each point is its own cluster, and pairs of clusters are merged as one moves up the hierarchy.
- 2. Divisive or top down, where all observations start in one cluster, and splits are performed recursively as one moves down the hierarchy.

Agglomerative clustering is \(O(N^3)\), although faster implementations are known, while divisive clustering is \(O(2^N)\).

Balanced Iterative Reducing and Clustering Using Hierarchies (BIRCH) can find a good clustering with a single scan of data with a limited amount of main memory available [44]. It improves the quality further with a few additional scans. A hierarchical data structure called CF-tree, which is a height-balanced tree, is used to store the clustering features (CFs). It is an order-sensitive clustering algorithm, which may detect different clusters for different input orders of the same data. BIRCH can only generate spherically shaped clusters.

Consider a cluster of \(n\) \(d\)-dimensional data objects or points. The CF, \((CF) = (m, LS, SS)\), where \(LS\) and \(SS\) are the vectors for the \(N\) dimensions of linear sums and square sums of the \(m\) points, is as follows:

\[
LS\text{ vector} = \sum_{i=1}^{m} x_{i,j}, \qquad SS\text{ vector} = \sum_{i=1}^{m} x_{i,j}^2.
\]

In the first phase, BIRCH scans the database to build an initial in-memory CF-tree, which can be viewed as a multilevel compression of the data that tries to preserve the inherent clustering structure of data. In the second phase, BIRCH applies a clustering algorithm to cluster the leaf nodes of the CF-tree, which removes sparse clusters as outliers and groups dense clusters into larger ones. Using CF, we can easily derive many useful statistics of a cluster: the cluster's centroid, radius, and diameter. To merge two clusters \(C1\) and \(C2\), we simply have the following:

\[
CF = (CF1 + CF2) = (m1 + m2, LS1 + LS2, SS1 + SS2).
\]

For two dimensions \(X\) and \(Y\), we have the following:

\[
LS\text{ vector} = (LS_X, LS_Y) = \left(\sum_{i=1}^{m} x_i, \sum_{i=1}^{m} y_i\right), \qquad SS\text{ vector} = (SS_X, SS_Y) = \left(\sum_{i=1}^{m} x_i^2, \sum_{i=1}^{m} y_i^2\right).
\]

The centroid is \((x_0, y_0) = (LS_X/m, LS_Y/m)\), and the radius is as follows:

\[
R = \frac{1}{m}\sqrt{SS_X + SS_Y + \left(\frac{1}{m} - 2\right)(LS_X^2 + LS_Y^2)}.
\]

Generalizing to \(N\) dimensions with subscript \(1 \le n \le N\),

\[
R = \frac{1}{m}\sqrt{\sum_{n=1}^{N} SS_n + \left(\frac{1}{m} - 2\right)\sum_{n=1}^{N} LS_n^2}.
\]

An algorithm similar to BIRCH is described in Reference 45.

Chameleon is a hierarchical clustering algorithm that uses dynamic modeling to determine the similarity between pairs of clusters [46]. Cluster similarity is assessed based on (1) how well connected objects are within a cluster and (2) the proximity of clusters. Two clusters are merged if their interconnectivity is high and they are close together. A \(k\)-NN graph approach constructs a sparse graph, where each vertex of the graph represents a data object, and there is an edge between two vertices if one object is among the \(k\) most similar objects to the other. The edges are weighted to reflect the similarity between objects. A graph-partitioning algorithm partitions the \(k\)-NN graph into a large number of relatively small subclusters such that it minimizes the cost of cutting edges [47]. Chameleon is more capable of discovering arbitrarily shaped clusters of high quality than several well-known algorithms such as BIRCH and density-based spatial clustering of applications with noise (DBSCAN) (see also FastMap [FM] in Reference 8).

Clustering Using Representatives (CURE) uses multiple representations to denote each cluster, so that clusters with nonspherical shapes can be discovered and there is less sensitivity to outliers [48]. The representatives are generated by selecting well-scattered points in the cluster and then shrinking them toward the center of the cluster by a specified fraction. At each iteration, the process merges two clusters until the number of clusters reaches the specified value. CURE uses a minimum heap to keep track of distances between one cluster and its closest cluster and one \(k\)-d-tree [49] to keep track of the representatives in all clusters. A heap extracts the cluster with the minimum distance by searching the nearest neighbors for all representatives in a cluster. CURE tends to be slow due to its dependence on the \(k\)-d-tree when handling large high-dimensional data sets.

BUBBLE-FM is an extension of BIRCH to distance spaces. The only operation possible on data objects is the computation of distance between them, while all scalable algorithms in the literature assume a \(k\)-dimensional vector space, which allows vector operations on objects [50]. The distance function associated with a distance space can be computationally expensive. For example, the distance between two strings is the edit distance, which, for strings of lengths \(N\), requires \(O(N^2)\) comparisons. BUBBLE-FM improves upon BUBBLE by reducing the number of calls to the distance function, which tends to be computationally expensive.

### 3.3.3 Density-Based Methods

Most partitioning methods for cluster objects based on the distance between objects can find only spherical-shaped clusters and encounter difficulty in discovering clusters of arbitrary shapes. The general idea behind density-based clustering methods is to continue growing a given cluster as long as the neighborhood density exceeds some threshold, so that clusters are defined as areas of higher density than the remainder of the data set. Objects in the sparse areas are usually considered to be noise and border points. Density-based methods can divide a set of objects into multiple exclusive clusters or a hierarchy of clusters.

DBSCAN is so called because it finds a number of clusters starting from the estimated density distribution of corresponding nodes [51]. DBSCAN's definition of a cluster is based on the notion of density reachability, that is, a point \(q\) is directly density-reachable from a point \(p\) if it is not farther away than a given distance \(\varepsilon\).
