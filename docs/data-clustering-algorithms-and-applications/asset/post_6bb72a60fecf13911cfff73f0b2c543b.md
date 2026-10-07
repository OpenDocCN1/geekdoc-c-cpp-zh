
# Data Clustering: Algorithms and Applications

![](img/b94d85a2e934001944bcc21abd9a9943_292_0.png)

**Figure 11.5:** The flowchart of clustering ensemble based on Random Projection and EM algorithm.

## 11.3.2 Global Projection

In the locality-preserving projection, for any two data points, we want their pair-wise distance approximately unchanged before and after the projection. In global projection, for each data point, we want project it to as close as possible to the original data point. If we use the Euclidean distance, it is equivalent to saying that we want to minimize the Frobenius norm of $(\hat{A}-A)$, where $A$ is the original data matrix and $\hat{A}$ is the projection of the original data matrix.

We can represent a global projection using the notation $\hat{A}$; a low-rank approximation. For example, a rank-$k$ approximation of $A$ is a matrix $\hat{A} = L \cdot M \cdot R$ where $L, M,$ and $R$ are of rank-$k$; and $\|\hat{A}-A\|$ is small. Such low-rank approximation provides a powerful tool for clustering. For example, for the spatial data, the right matrix $R$ provides the description of cluster-membership; and for the bipartite graph data, we represent it by its adjacency matrix $A$; then the left and right matrices are good indicators for row and column memberships; and the middle $M$ indicates the interaction between the row and the columns. We refer the readers to Chapter 7 for more details on the clustering algorithms based on matrix-rank approximation. Here, we introduce how to use such low-rank approximation efficiently so that the overall clustering procedure is efficient and stable.

Depending on the properties of these matrices $(L, M,$ and $R)$, different approaches have been proposed in the literature. For example, in singular value decomposition (SVD) [21], $L$ and $R$ are orthogonal matrices containing singular vectors and $M$ is a diagonal matrix whose diagonal entries are singular values. Among all possible rank-$k$ approximations, SVD gives the best approximation in terms of squared error. Furthermore, SVD is usually dense, even if the original matrix is sparse. The singular vectors are abstract notions of best orthonormal behavior, which is not intuitive for the interpretation.

To address the computational challenges in SVD, sparsification has been proposed in [1]. The basic idea is to randomly sample the entries in $A$ as zeros and rescale the remaining entries; and to run SVD on the resulting sparse matrix once. Instead, with uniform sampling, each entry $A(i,j)$ is set to zero with the probability of $1-1/s(s>1)$ and is scaled as $sA(i,j)$ with the probability of $1/s$. The resulting sparse matrix $\hat{A}$ can be viewed as a perturbed version of the

> $^3The authors in [1] also proposed a non-uniform sampling procedure.

original matrix A adding a random matrix $E$ to it. From the random matrix theory [20], it is well known that the norm of a random matrix is well-bounded. As a result, the SVD on this sparse matrix $A$ Provides a *near-optimal* low-rank approximation of the original data matrix $A$, at the benefit of significantly speeding up the computation.

Notice that the sparse SVD provides computational gain compared to the exact SVD, but does not address the issue of space cost or the interpretability of the resulting low-rank approximation. For example, as shown in [44], these methods often need a huge amount of space. More-recently, the so-called example-based low-rank approximations have started to appear, such as CX/CUR [15], CMD [44] and Colibri [45], which use the actual columns and rows of the matrix A to form $L$ and $R$. The benefit is that they provide an intuitive as well as a representation, since $L$ and $R$ are sampled from the original data. However, the approximation is often sub-optimal compared to SVD and the matrix $M$ is no longer diagonal, which means a more complicated interaction.

In decomposition, we first randomly sample a set of columns $C$ from the original data matrix A, and then project the A into the column space of $C$, i.e., $A = CC'$, where $C'$ is the Moore-Penrose inverse of $C$. In CUR decomposition, we also allow sampling on the row side to further reduce the space cost. One drawback of the original CX/CUR is the repeated sampling, i.e., some sampled columns/rows are repeated. Based on this observation, CMD tries to remove duplicate columns and rows before performing the projection. In [45], the authors further propose removing all the linearly correlated sampled columns. Since it does not affect the column/row space if we remove the linearly correlated columns/rows, these methods (CMD and Colibri) lead to the same approximation accuracy as CX/CUR, but require much less space and cost. Figure 11.6 provides an illustrative comparison of these different projection methods.

# Big Data Clustering

![](img/b94d85a2e934001944bcc21abd9a9943_293_0.png)

**FIGURE 11.6:** An illustrative comparison of SVD, CX/CUR, CMD, and Colibri. Each dot is a data point in 2-D space. SVD (a) uses all the available data points to generate optimal projection directions. CX/CUR (b) uses actual sampled data points (dark dots) as projection directions and there are a lot of duplicates. CMD (c) removes duplicate sampled data points. Colibri (d) removes all the linearly correlated data points from sampling.

## 11.4 Parallel and Distributed Clustering Algorithms

In this section, we survey parallel and distributed clustering algorithms to handle big data. In contrast to the typical single machine clustering, parallel and distributed algorithms use multiple machines to speed up the computation and increase the scalability. The parallel and distributed algorithms are divided into two groups: traditional memory-based algorithms [13, 19, 5, 6, 41] and disk-based algorithms [11, 9, 22, 26].

The traditional memory-based algorithms assume that the data fit in the memory of multiple machines, and each machine loads the data into memory.

Many of the disk-based algorithms use MapReduce [11], or its open-source counterpart Hadoop, to process resident data. MapReduce is a programming framework for processing huge amounts of data in a massively way. MapReduce has two major advantages: (a) the programming is obvious of the data distribution, replication, load balancing, etc., and (b) the programming concept is familiar, i.e., the concept of functional programming. Briefly, the programmer needs to provide only two functions, a map and a reduce. The framework follows as follows: (a) the map stage sequentially passes over the input file and outputs (key, value) pairs; (b) the reduce stage processes the values with the same key and outputs. Optionally, combiners can be used to aggregate the outputs from local mappers. MapReduce has been used widely for scale data mining [29, 26].

We describe both the traditional and modern parallel and distributed clustering algorithms. We first describe the general principle of parallel and distributed algorithms including DBDC and ParMetrics. Finally we survey modern, disk-based MapReduce algorithms including PKMeans, DisCo, and BOW.

### 11.4.1 General Framework

Most parallel and distributed clustering algorithms follow the general framework depicted in Figure 11.7.

- 1. Partition. Data are partitioned and distributed over machines.
- 2. Local Clustering. Each machine performs local clustering on its partition of the data.
- 3. Global Clustering. The cluster information from the previous step is aggregated globally to produce clusters.
- 4. Refinement of Local Clusters. Optionally, the local clusters are sent back to each machine to refine the local clusters.

Some algorithms (e.g. PKMeans in Section 11.4.4 and DisCo in Section 11.4.5) iteratively perform steps 3 and 4 until the quality of clusters becomes reasonably good. One of the main challenges of parallel and distributed clustering is to minimize data traffic between the steps 2 and 3. Minimizing the traffic is important because the advantage of a parallel and distributed clustering comes from the fact that the output from the local clustering step is much smaller than the raw data. We will see how different algorithms use strategies to minimize the data traffic.

Another issue in parallel and distributed clustering is the lower accuracy compared to the serial counterpart. There are two main reasons for the lower accuracy. First, each machine performing the local clustering might use a different algorithm than the serial counterpart due to heavy communication costs. Second, even though the same algorithm is used for the local clustering step
