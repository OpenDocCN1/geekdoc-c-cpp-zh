# Clustering Validation Measures

![](bbox=[0.175, 0.093, 0.477, 0.263])

![](bbox=[0.533, 0.093, 0.836, 0.263])

(a) Clustering by K-means

(b) Clustering by Agglo

![](bbox=[0.175, 0.337, 0.477, 0.507])

![](bbox=[0.533, 0.337, 0.836, 0.507])

(c) Clustering by DBSCAN

(d) Clustering by Chameleon

**FIGURE 23.14:** Clustering results on data set T4.k.modified by different algorithms where NC = 6.

the representative for cluster when evaluating the intercluster separation. In addition, $S$ uses the average pairwise distance between objects in each cluster as the separation measurement, which can be viewed as equivalent to the minimum pairwise distance between cluster centers in a sense. Since it is meaningful to use the center to represent the entire cluster only for the sphere-shaped cluster, this implies that these indices can work only in the hypersphere condition. Figure 23.15 shows clusters $A$ and $B$ have an entire structure, and the cluster centers are not even in the clusters. If one moves cluster $B$ from the real-line baseline $B'$, $A$ and $B$ are getting closer while the distance between their centers becomes larger. In this case, it is meaningless and incorrect to make cluster center representative for the entire cluster.

The above measures use either the average (minimum) pairwise distance between objects in clusters or one object (the cluster center) as the representative of the entire cluster when calculating the intercluster separation. These measures consider only the positions of the objects and fail to take into account the object distributions which form the geometrical information of the cluster. On the other hand, $CVNN$ evaluates the intercluster separation based on objects that carry the geometrical information of each cluster. Sharing the same idea with knn, $CVNN$ uses multiple objects as representatives for different clusters in different