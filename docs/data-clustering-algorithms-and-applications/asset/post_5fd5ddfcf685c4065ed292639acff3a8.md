
## Data Clustering: Algorithms and Applications

Note that the optimization problem in (22.13) is over the domain of $\hat{S}$. The difference between the matrices $S$ and $\hat{S}$ lies in the optimization problem. If optimization is performed with cluster labels (as illustrated in Section 22.4.3), there is no guarantee of achieving the optimum value $\hat{S} = S$. However, if we are optimizing over the domain of the co-association matrix, we can achieve this optimum value in theory.

## 22.4.2.2 Relating Consensus Clustering to Other Optimization Formulas

The co-association representation of clustering has been used to relate consensus clustering with two other well-known problems.

- 1. Consensus Clustering as Nonnegative Matrix Factorization (NNMF)

Li et al. [43, 42], using the same objective function mentioned in (22.13), show that the problem of consensus clustering can be reduced to an NNMF problem. Using $U_{ij} = \hat{S}_{ij}$ to be a solution to this optimization problem, we can rewrite it (22.13) as

```
$$\arg\min_{i,j=1} (S_{ij} - U_{ij})^2 = \arg\min ||S - U||_F^2$$ (22.14)
```

where matrix is the Frobenius norm. This problem formulation is similar to the NNMF formulation [41] and can be solved using an iterative procedure. In [27], the cost $J$ used in Equation (22.13) was further modified via modification to make it consistent with data sets with different numbers of data points (n) and different numbers of base clusters (k).

- 2. Consensus Clustering as Correlation Clustering

Gionis et al. [26] show that a certain formulation of consensus clustering is a special case of correlation clustering. Suppose we have set $\mathcal{X}$ and some kind of dissimilarity measurement (distance) between every pair of points in $\mathcal{X}$. This dissimilarity is denoted by $d_{ij} \in [0,1] |\mathbf{x}_i, \mathbf{x}_j \in \mathcal{X}$. The objective of correlation clustering [9] is to find a partition $\lambda$ that

```
$$\hat{\lambda} = \arg\min_{\lambda} d(\lambda)$$
```

```
$$\arg\min_{\lambda} \sum_{(i,j) : \lambda(\mathbf{x}_i) = \lambda(\mathbf{x}_j)} d_{ij} + \sum_{(i,j) : \lambda(\mathbf{x}_i) \neq \lambda(\mathbf{x}_j)} (1 - d_{ij})$$ (22.15)
```

In the above equation, $\lambda(\mathbf{x}_i)$ is the cluster label imposed by $\lambda$ on $\mathbf{x}_i$. The co-association value of cluster ensemble problem reduces to correlation clustering if the distance $d_{ij}$ is defined as $d_{ij} = \frac{1}{2}|\lambda(\mathbf{x}_i) \neq \lambda(\mathbf{x}_j)| |\forall i, j$.

## 22.4.3 Direct Approaches Using Cluster Labels

Several consensus mechanisms take the cluster labels provided by the base clusterings as input and try to optimize an objective function such as (22.2), without computing the co-association matrix.

### 22.4.3.1 Graph Partitioning

In addition to CSPA, Strehl and Ghosh [56] propose two approaches to cluster ensembles: Hyper Graph Partitioning Algorithm (HGPA) which clusters the objects based on their cluster memberships, and Meta Clustering Algorithm (MCLA), groups the clusters based on which objects are contained in. HPGA considers a graph with each object being a vertex. A cluster in any base clustering is represented by a hyper-edge connecting the members. The hyper-graph clustering package HMETIS (Karpis et al. [35]) was used to provide quality clusters and is very scalable. With CSPA, employing a graph clustering algorithm ensures a constraint that favors clusterings of comparable size. HPGA is fast with worst case complexity of O(nk), it suffers from an admission problem: if all members of a cluster are not assigned the same cluster in the consensus solution, it incurs a constant penalty; however it cannot distinguish between a situation where one object was clustered differently and one where several objects were allocated to other groups. Due to this issue, HPGA is often not competitive in terms of cluster quality.

MCLA forms a meta-graph with vertices, the edge weights proportional to the similarity between vertices, using the binary Jaccard measure (number of elements common by the total number of distinct elements). Since the base clusters are partial, this results in an r-partite graph. The meta-graph is then partitioned into k meta-clusters. Each meta-cluster, therefore, contains approximately r vertices. Finally, ties are broken randomly. The worst case complexity is O(nk²).

Noting that CSPA and MCLA consider either the similarity of objects or the similarity of clusters, a Hybrid Bipartite Graph Formulation (HBGF) was proposed in [16]. A bipartite graph models both points and clusters as vertices, where an edge exists only between a cluster and a vertex if the latter is a member of the former. Either METIS or other multi-spectral clustering methods are used to partition this bipartite graph. The corresponding versions of CSPA, MCLA, and HBGF have also been developed by Punera and Ghosh [52]. It should be noted that all of CSPA, MCLA, and HBGF were generated using one other than the NI measure in [56].

### 22.4.3.2 Cumulative Voting

The concept of cumulative voting was first introduced in [15] where the authors used bagging to improve the accuracy of clustering procedure. Once clustering is done on a bootstrapped sample, the cluster correspondence is solved using iterative relabeling via Hungarian algorithm. Clustering on each bootstrapped sample gives votes corresponding to each data point and cluster pair which, in aggregate, decide the final consensus.

A similar approach was adopted in [6]. Base clustering in this contribution is of providing a soft or probabilistic vote on which clusters in the consensus solution its data points should. These votes are then gathered across the base solutions and thresholded to determine the membership of each object to the consensus clusters. Again, this requires a mapping from the base clusters to a stochastic one. An information-theoretic criterion based on the information bottleneck was used in [6] for purpose. The mean of all the stochastic yields the consensus partition. This approach is able to capture a range of l in the base clusterings, is fast and avoids the complexity of forming, and has good empirical results as well. Noting that the information bottleneck can be obtained as a special case of Bregman clustering [8], it should be possible to recast this approach as a.

## 22.5 Applications of Consensus Clustering

The motivation for consensus clustering has already been introduced in 22.1. Since cluster ensemble improves the quality of clustering, can be used for any analysis problem, e.g., image segmentation [67], bioinformatics, document retrieval [28], and automatic categorization [70], just to name a few. Gionis et al. [26] show how clustering algorithms can be used to improve the robustness of clustering, for categorical data [29] and heterogeneous data, identifying the correct number of clusters, and detecting outliers. Fisher and Buhmann [20] showed how resampling the data and subsequent aggregation of the clustering from selected sets can improve the quality. [56] is also available at http://strehl.com/soft.html. In this section, we briefly discuss two major application domains.

### 22.5.1 Gene Expression Analysis

Consensus clustering has been applied to microarray data to improve the quality and robustness of the clustering results. A resampling based approach is used by Monti et al. [48], in which the agreement across the results obtained by executing base clustering on several partitions of the original dataset is used to obtain the final clustering. Swift et al. [58] use a variety of clustering algorithms on the same dataset to generate base clustering results and try to find clusters that are consistent across all the base results using simulated annealing. In [19] the consensus clustering problem is treated as a median partition problem, where the aim is to find a partitioning of the data that minimizes the distance to all the other partitions. The authors propose greedy heuristics to find overlapping clusters in microarray data. Deodhar and Ghosh [14] use consensus clustering to identify the clustering solution from the candidate solutions. In this work, two different techniques are used to generate the consensus clustering solution from the candidate solutions. In [12], gene expression time-series data is clustered at different times and the intervals from different timestamps are merged into a single solution using graph partitioning of the ensemble-coassociation matrix.

### 22.5.2 Image Segmentation

Though there exist several segmentation algorithms, depending on the application data, some perform better than the others it is impossible to know beforehand which should be used. The authors in [55] use the cluster ensemble formulation to aggregate the results of multiple segmentation algorithms such as (a) Normalized Cuts, (b) Energy Minimization by Graph Cuts, and (c) Evolution to generate image segmentation. However, they found that the ensemble segmentation outperforms any individual segmentation algorithm. One of such results is shown in Figure 22.4. The first result corresponds to Normalized Cuts, the second one is from Graph
