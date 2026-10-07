# Big Data Clustering

![](bbox=[0.209, 0.093, 0.792, 0.173])

FIGURE 11.3: The flowchart of BIRCH algorithm.

The empirical evaluation in [47] indicates that BIRCH consistently outperforms the previous CLARANS in terms of time and space efficiency. It also more robust to the ordering of the input data sequence. BIRCH offers some additional advantages, e.g., being robust to outliers and being more parallelized.

# 11.2.3 CURE: Fighting with the Irregular Clusters

In both CLARANS and BIRCH, we use one single data point to represent a cluster. Conceptually, we assume each cluster has a spherical shape, which may not be the case in real applications where the clusters can exhibit more complicated shapes. At the other extreme, we can keep all the data points within each cluster, which computational as well as space cost might be too high for large data sets. To address this issue, clustering using CURE [22] proposes to use a set of well-characterized data points to represent a cluster.

CURE is essentially a hierarchical clustering algorithm. By treating each data point as a single cluster and recursively merging existing clusters into one until we have only k clusters. In order to decide which clusters to be merged at each iteration, it computes the minimum distance between all the possible representatives of the two clusters. CURE uses two major data structures to enable the efficient search. First, it uses a heap to track the distance of each existing cluster to its closest cluster. Additionally, it uses k-d tree to store all the representative points for each cluster.

In order to speed the computation, CURE first draws a sample of the input data and analyze the above procedure on the sampled data. The authors use Chernoff bound to analyze the necessary sample size. When the original data is large, the different clusters overlap each other, which in turn requires a large sample size. To alleviate this issue, CURE uses partitions to speed up. By specify, it first partitions the n' sampled data points into p partitions. With each partition, it runs a partial hierarchical clustering until either a predefined number of clusters is reached or exceeds some threshold. After that, it runs clustering on all the clusters from the p partitions (“global clustering”). Finally, each nonsampled point is assigned to a cluster based on its distance to the representative point ("labeling”). Figure 11.4 summarizes the flowchart of the CURE algorithm.

The empirical evaluation in [22] shows that CURE achieves lower execution time compared to BIRCH. In addition, with BIRCH, CURE is robust to outliers by shrinking the representative points to the center of the cluster with a constant factor.

# 11.3 Randomized Techniques for Clustering Algorithms

In the previous section, we have already seen how sampling can be used to speed up the clustering algorithms, e.g., to reduce the search space as in CLARA and CLARANS and to pre-