
## A Survey of Partitioned and Hierarchical Clustering Algorithms

- 6. Silhouette Coefficient [26]: This is formulated by considering the intra- and inter-cluster distances. For a given point $x_i$, first the average of the distances to all points in the same cluster is calculated. This value is set to $a_i$. For each cluster that does not contain $x_i$, the average distance of $x_i$ to all the data points in each cluster is computed. This value is set to $b_i$. Using these two values the silhouette coefficient of a point is estimated. The average of all the silhouettes in the dataset is the average silhouette widths for all points in the dataset. To evaluate the quality of a clustering one can compute the average silhouette coefficient of all points:
$$S = \sum_{i=1}^{N} \frac{b_i - a_i}{\max(a_i, b_i)}$$

- 7. Newman and Girvan [40]: In this method, the dendrogram is viewed as a graph, and a betweenness score (which will be used as a dissimilarity measure between the edges) is proposed. The procedure starts by calculating the betweenness score of all edges in the graph. Then the edge with the highest betweenness score is removed. This is followed by recomputing the betweenness scores of the remaining edges until the final set of connected components is obtained. The cardinality of the set serves as a good estimate for K.

- 8. ISODATA [2]: Proposed for clustering based on the nearest centroid method. In this method, K-means is run on the dataset to obtain clusters. Clusters are then merged if distance is less than a threshold $\theta$ or split if they have fewer than a certain number of points.

### ### Variations of K-Means

The simple framework of K-means makes it easy to modify and build more efficient algorithms on top of it. Some of the variations of K-means are based on:

(i) Choosing different prototypes for the clusters (K-medoids, K-medians, K-modes),
(ii) choosing better initial estimates (Intelligent K-means, Genetic K-means), and
(iii) applying some feature transformation (Weighted K-means, Kernel K-means). In this section, we will discuss the most prominent variants of K-means that have been proposed in literature.

### ### 4.2.4.1 K-Medoids Clustering

K-medoids is a clustering algorithm which is more resilient to outliers than K-means [38]. Similar to K-means, the goal of K-medoids is to find a clustering solution that minimizes a predefined objective function. The K-medoids algorithm chooses the actual data points as prototypes and is more robust to noise and outliers in the data. The K-medoids algorithm aims to minimize the absolute error relative to SSE. Similar to the K-means algorithm, the K-medoids algorithm proceeds iteratively until each representative object is the medoid of the cluster. The basic K-medoids clustering is given in Algorithm 14.

In K-medoids clustering, specific cases are considered where an arbitrary point $x$ is used to replace a representative point $m$. Following this step, the change in membership of the points originally belonged to $m$ is checked. The change in membership of these points can occur in one of two ways: these points can be closer to $x$ (new representative point) or to any of the other set of representative points. The cost of swapping is calculated as the absolute error correction for K-medoids. For each reassignment operation this cost of swapping is calculated and contributes to the overall cost function.

**Algorithm 14: K-Medoids Clustering**
1. Select K points as the initial representative objects.
2. repeat
3. Assign each point to the cluster with the nearest representative object.
4. Randomly select a nonrepresentative object $x_i$.
5. Compute the total cost $S$ of swapping representative $m$ with $x_i$.
6. If $S < 0$, swap $m$ with $x_i$ to form the new set of K representative objects.
7. until Convergence criterion is met.

To deal with the problem of executing multiple swap operations while obtaining the final representative points for each cluster, a modification of K-medoids clustering called Partitioning Around Medoids (PAM) algorithm is proposed [26]. This algorithm operates on the dissimilarity metric of a dataset. PAM minimizes the objective function by swapping all non-medoid points and iteratively until convergence. K-medoids is more robust than K-means but the computational complexity of K-medoids is higher and not suitable for large datasets. PAM was also combined with a sampling method to propose the CLARA (Clustering Large Application) algorithm. CLARA considers samples and applies PAM on each of them to finally return the set of optimal methods.

### ### 4.2.4.2 K-Medians Clustering

K-medians clustering calculates the median for each cluster as opposed to calculating the mean of the cluster (as in K-means). K-medians algorithm chooses K clusters that aim to minimize the sum of distance between each point and the closest cluster center. The distance used in the K-medians algorithm is the L1-norm as opposed to the square of the L2-norm used in K-means. The criterion for the K-medians algorithm is defined as:
$$S = \sum_{k=1}^{K} \sum_{i \in C_k} |x_{ij} - med_{kj}|$$
where $x_{ij}$ represents the $j$-th instance $i$ of the $k$-th cluster $C_k$ and $med_{kj}$ represents the median for the $j$-th attribute in $C_k$. K-medians are more robust to outliers compared to K-means. The goal of the K-medians clustering is to determine which subsets of points minimize the cost of assignment of the data points to the nearest median. The overall outline of the algorithm is similar to K-means. The two steps are iterated until converge (i) all data points are assigned to their nearest median and (ii) the means are recomputed using the median of each feature.

### ### 4.2.4.3 K-Modes Clustering

One of the major disadvantages of K-means is its inability to deal with categorical data. To handle this, K-modes was proposed. Using transformation methods, categorical data can be transformed into new spaces, and K-means can be applied to obtain the clusters. However, this method proves to be very ineffective. The K-modes algorithm [21] has been proposed to tackle this challenge.

### ### 4.2.4.4 Fuzzy C-Means Clustering

This is popularly known as Fuzzy C-Means. Performing hard assignments of points to clusters is not feasible in complex datasets where there are overlapping clusters. To extract such overlapping structures, a fuzzy clustering algorithm can be used. In fuzzy clustering algorithm (FCM) [12, 4], the membership of points to different clusters can vary from 0 to 1. The SSE function for FCM is presented in Equation (4.12):
$$SSE(C) = \sum_{k=1}^{K} \sum_{x_i \in C_k} w_{sik}^\beta \|x_i - c_k\|^2$$
$$w_{sik} = \frac{1}{\sum_{j=1}^K (\frac{\|x_i - c_k\|}{\|x_i - c_j\|})^\beta}$$
$$c_k = \frac{\sum_{x_i \in C_k} w_{sik}x_i}{\sum_{x_i \in C_k} w_{sik}}$$
Here $w_{sik}$ is the membership weight of point $x_i$ belonging to $C_k$. This weight is estimated during the update step of fuzzy c-means. The weighted centroid according to the fuzzy weights for $C_k$ is calculated ($c_k$). The basic algorithm works similarly to K-means where the algorithm minimizes the SSE iteratively by updating $w_{ijk}$ and $c_k$. This process is continued until the convergence of clusters. As in K-means, the FCM algorithm is sensitive to outliers and the final solutions obtained will correspond to the local minimum of the objective function. There are further extensions of this algorithm in the literature such as Rough C-means [34] and Possibilistic C-means.

### ### 4.2.4.5 X-Means Clustering

X-means [42] is a clustering method used to efficiently estimate the value of K. It uses a method blacklisting to identify those sets of centroids among the current existing ones.

## A Survey of Partitioning and Hierarchical Clustering

K-modes is a nonparametric algorithm suitable for categorical data. It is a special case of the L-p norm where p tends to zero. As opposed to K-means which calculates the distance between data points, the K-modes algorithm is described in detail in Algorithm 15.

**Algorithm 15: K-Modes**
1. Select initial modes.
2. repeat
3. Assign each point to the cluster with the nearest mode.
4. Recompute the modes of the clusters.
5. until Convergence is met.
