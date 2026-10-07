# A Survey of Partitional and Hierarchical Clustering Algorithms

# 4.2 Partitional Clustering Algorithms

The first partial clustering algorithm that will be discussed in this section is the K-Means algorithm. It is one of the simplest and most efficient clustering algorithms proposed in the literature of data clustering. After the algorithm is described in detail, some of the major factors that influence the final clustering solution will be highlighted. Finally, some of the widely used variations of K-Means will also be discussed in this section.

# 4.2.1 K-Means Clustering

K-means clustering [33, 32] is the most widely used clustering algorithm. It starts by choosing K representative points as the initial centroids. Each point is then assigned to the closest centroid on a particular proximity measure. Once the clusters are formed, the centroids for each cluster are updated. The algorithm then iteratively repeats until two steps do not change or any other alternative relaxed convergence is met. K-means clustering is a greedy algorithm which is guaranteed to converge to a local minimum but minimization of its score function is known to be NP-Hard [35]. Typically, the convergence is relaxed a weaker condition may be used. In practice, it follows that the iterative procedure must be continued until 1% of the points change their cluster memberships. A detailed proof of the mathematical convergence of K-means can be found in [45].

Algorithm 13 K-Means Clustering
1: Select K points as initial centroids.
2: repeat
3: Form K clusters by assigning each point to its closest centroid.
4: Recompute the centroid of each cluster.
5: until convergence is met.

Algorithm 13 provides an outline of the basic K-Means algorithm. Figure 4.1 provides an illustration of the different stages of the running of 3-means on the Fisher Iris dataset. The first iteration initializes three random points as centroids. In subsequent iterations the centroids change positions until convergence. A wide range of proximity measures can be used within the K-means algorithm while computing the cluster score. The choice can significantly affect the centroid assignment and the quality of the final solution. The different kinds of measures which can be used here are Manhattan distance (L1 norm), Euclidean distance (L2 norm), and Cosine similarity. For the general-means, Euclidean distance metric is the most popular choice. As mentioned above, we can obtain different clusters for different values of K and proximity measures. The objective function employed by K-means is called the Sum of Squared Errors (SSE) or Residual Sum of Squares (RSS). The mathematical formulation for SSE/RSS is provided below.

Given a dataset D={x₁, x², ...,xₙ} consists of n points, let us denote the clustering obtained after applying K-means clustering by C={c₁, c², ...,cₙ}. The SSE for this clustering is provided in the Equation (4.1) where cₖ is the centroid of cluster Cₙ. The objective is to find a clustering that minimizes the SSE score. The iterative assignment and update steps for the K-means algorithm aim to minimize the SSE score for the given set of centroids.

```
SSE(C) = \sum_{x_i \in C_k} \|x_i - c_k\|^²  (4.1)
```

```
c_k = \frac{\sum_{x_i \in C_k} x_i}{|C_k|}  (4.2)
```