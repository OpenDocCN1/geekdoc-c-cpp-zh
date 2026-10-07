# Data Clustering: Algorithms and Applications

In [19] the authors perform an evaluation of clustering methods applied on a long time series of medical data and implement agglomerative hierarchical clustering. Their experimental results show that complete-linkage selection produces more reasonable clusters and better dendrograms, when the input sequences are more uniformly distributed in the output clusters. However, the superiority of complete-linkage selection over others is not proven to be held on all datasets and clustering applications.

In [18] the authors propose a hierarchical clustering method followed by a k-means fine-tuning process using DWI distance, where the objective function that is minimized is a sum of DWI distances from each object to a prototype of the cluster to which it belongs. The cluster prototype can be the DWI average of the objects belonging to the cluster, which has been proven to be inaccurate [42], the cluster method, or a locally optimal prototype that has been computed with a warping path based local search.

# 15.5.3 Density-Based Clustering

In [13] Ester et al. propose DBSCAN as a way to identify clusters of points utilizing the fact that intercluster density is higher than among points to different clusters. The intuition behind their approach is that objects belonging to a cluster must be surrounded by a minimum number of objects at a small distance, thus defining the notion of neighborhood density. The DBSCAN algorithm, points that are located in a neighborhood of high density are defined as core points, whereas points that do not have a core in their neighborhood are defined as noise points, and are discarded. Clusters are formed around core points, and clusters that are in the same neighborhood are merged.

Ertöz et al. argue that traditional DBSCAN cannot be used effectively in high-dimensional data as such time series, because the notion of Euclidean distance is meaningless as the number of dimensions increases [12]. Instead, they propose the k-nearest neighbor approach to multivariate density estimation, where a point is considered to be in a region with high probability density it has a lot of highly similar neighbors. Using this notion, they eliminate noise and outliers, identifying dense clusters in the data.

# 15.5.4 Trajectory Clustering

While multidimensional time series can be used to represent trajectories¹ another commonly accepted interpretation is that trajectory is a data type representing the movement of an object. In the past couple of decades, Moving Objects Databases have brought a trend of their own, and various representation methods, storage, and indexing techniques, with spatiotemporal querying methodologies, have been introduced [17, 60]. Clustering and mining of spatiotemporal trajectories are of interest in various applications such as traffic management, transportation optimizations, and ecological studies of animals/migrations.

Vlachos et al. define a trajectory as the set of positional information of a moving object ordered by time [51]. Lin and Su [35] disagree the time information in trajectories and focus on the shape information. They point out that continuous representation of trajectories is usually costly and difficult to compute, so represent trajectories in terms of line sequences. Specifically, each trajectory is defined as an ordered sequence of points $T=[p_1, p_2, ..., p_n]$ that are connected with straight lines. Alternatively, Chen et al. represent a trajectory $S$ in the two-dimensional plane is defined as a sequence of triples $S=\{(t_1; s_1), ..., (t_n; s_n)\}$. [11].

textnA fair amount of work has been devoted to trajectory clustering, where not only shape but speed and direction are important. Some methods [44] also discuss the online correlation aspect

> ¹For matter, a trajectory can be perceived as a special case of multidimensional time series.