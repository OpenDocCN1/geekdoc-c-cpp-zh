# Data Clustering: Algorithms and Applications

Subsequently, for each incoming record, we will update the counts of the cluster-specific hash tables. In order to determine the assignments of data points to clusters, the d-dimensional records to the frequency statistics of the values in the different clusters are computed. It is not possible to do it all precisely, since the frequency statistics are not maintained. Let $q_j(x^j)$ be the frequency of the value $x^j$ in the $j$th cluster. Let $m_j$ be the number of data points assigned to the $j$th cluster, the d-dimensional statistics of the record $(x^1...x^d)$ for the $j$th cluster are given by $(q_j(x^1)...q_j(x^d))$. Then, the frequency-based dot product $D^j(X)$ of the incoming record with cluster statistics of j is the product of the frequencies $(q_j(x^1)/m_j)...q_j(x^d)/m_j)$ of the attribute values $(x^1...x^d)$ with the frequencies of these same values within record $(1,...,d)$. Therefore, the dot product is

```
$D^j(\mathbf{X}) = \sum_{r=1}^{d} \frac{q_j(x^r)}{m_j}$
```

The incoming record is assigned to the cluster for which the estimated dot product is the largest. We note that the value of $q_j(x^j)$ cannot be known, but can only be estimated approximately due to the massive-domain constraint. There are two key steps which use the sketch table during the clustering process:

+   * Updating the sketch table and other required statistics for the corresponding cluster for each incoming record.
* Comparing the similarity of the incoming record to the different clusters with the use of the corresponding sketch tables.

First, we discuss the process of updating the sketch table, a particular cluster has been identified for assignment. For each record, the sketch-table entries correspond to the attribute values on the different dimensions. For each incoming record $\mathbf{X}$, the w hash functions are applied to the strings to represent the attribute values in it. Let $m$ be the number of clusters to which the data point is assigned. Then, exactly $d$ entries in the sketch table for cluster are updated by applying the w hash functions to each of the $d$ strings which are denoted by $x^1...x^d@$. In order to pick a cluster, the approximate dot product across different clusters need to be computed. The record is compared to its sketch representation by applying the w hash functions to each of the different attributes. We retain the corresponding d-sketch table for the sketch cluster $j$, the $d$ counts are simple estimates of the value of $q_j(x^1)...q_j(x^d)$ of the dimension of record $\mathbf{X}_i$. Specifically, let the count of $\mathbf{X}_i$ in the sketch table for cluster $j$ be given by $c_{ijr}$. Then, we estimate the dot product $D_{ij}$ between the record $\mathbf{X}_i$ and the frequency statistics for cluster $j$ as:

```
$D_{ij} = \min \sum_{r=1}^{d} c_{ijr}/m_j$
```

The value of $D_{ij}$ is computed over all clusters $j$, and the cluster with the largest dot product to the record $\mathbf{X}_i$ is picked for assignment.

It has been shown in [2] that this assignment process approximates an infinite space clustering algorithm quite well. This is characterized by being kept in mind that in many cases an assignment errors of the approximation process. An important point is that an incoming data point may match with many of the clusters. Since similarity functions as the dot product are heuristically defined, small errors in ordering (when $b_j$ are not very significant for