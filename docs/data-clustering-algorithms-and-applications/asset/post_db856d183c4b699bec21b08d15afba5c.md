
# Network Clustering

clustering does not use geometric information of the graph. It does not operate on but a mathematical representation of the graph. An advantageous feature of spectral clustering is that the decision about each vertex is taken based on a more global view of the problem. In the following sections we discuss spectral clustering in detail.

## 17.8.1 Similarity Graphs

Given a set of data points $x_1, x_2, \dots, x_n$ and some notion of similarity $s_{i,j} \ge 0$ between $x_i$ and $x_j$, a simple and nice way of representing data is in the form of similarity graph $G = (\mathcal{V}, \mathcal{E})$. Each data point $x_i$ is represented by a vertex $v_i$ in the graph and two vertices $v_i$ and $v_j$ are connected if the similarity $s_{i,j}$ between corresponding data points $x_i$ and $x_j$ is greater than some threshold value. The edge is weighted by $s_{i,j}$. The clustering problem can be reformulated as the problem of partitioning the similarity graph so that the edges between different groups have very low values.

Let $\mathcal{G} = (\mathcal{V}, \mathcal{E})$ be a weighted undirected graph, the weighted *adjacency matrix* of the graph is matrix $W = w_{i,j}$ for $i, j = 1, \dots, n$. The degree of vertex $v_i$ is defined as

```
$d_i = \sum_{j=1}^{n} w_{i,j}$
```

Because $w_{i,j} = 0$ if $v_i$ and $v_j$ are not connected, this sum runs over vertices adjacent to $v_i$. The degree matrix $D$ is defined as diagonal matrix with $d_1, \dots, d_n$ on the diagonal. Let $F = (f_1, \dots, f_n)^T \in \mathbb{R}^n$ as the vector with $f_i = 1$ if $v_i \in A$ and $f_i = 0$. A few more notices are as follows:

```
$W(A, B) := \sum_{i\in A, j\in B} w_{ij}$
```

Given a subset $A \subset \mathcal{V}$, the "size" of $A$ is as follows:

```
$|A| := Number \text{ of vertices in A}$
$vol(A) := \sum_{i\in A} d_i$
```

Subset $A \subset \mathcal{V}$ of a graph is *connected* if there is a path between each pair of vertices in $A$ and no intermediate vertices from $\mathcal{V} \setminus A$. Subset $\bar{A}$ is called a *connected component* if it is connected and there are no connections between vertices in $A$ and $\bar{A}$. The nonempty sets $A_1, \dots, A_k$ form a partition of the graph if $A_i \cap A_j = \mathbf{0}$ and $\bigcup_{i=1}^{k} A_i = \mathcal{V}$.

## 17.8.2 Types of Similarity Graphs

Given a set of data points $x_1, x_2, \dots, x_n$ and a pairwise similarity $s_{i,j}$ (or dissimilarity $d_{i,j}$) measure, there are several methods to convert these points into a similarity graph [105]. In this section we discuss several well-known methods for constructing a similarity graph from a set of points and the pairwise similarity/dissimilarity function.

$\epsilon$-neighborhood graph: In this method, all points with pairwise distance smaller than $\epsilon$ are connected. Since the distance is smaller than for all connected pairs, weighting the edges does not convey more information. Hence, these graphs are typically undirected.

$k$-nearest neighbor graph: In this approach, vertex $v_i$ is connected with $v_j$ if $v_j$ is among $k$-nearest neighbors of $v_i$. However, since the neighborhood relationship is not symmetric, this definition leads to a directed graph. There are two standard ways to deal with this issue:

- The simplest solution is to ignore the directions of the edges. In this method $v_i$ and $v_j$ are connected if $v_i$ is among $k$-nearest neighbors of $v_j$ or if $v_j$ is among $k$-nearest neighbors of $v_i$. Resulting graph is called k-nearest neighbor graph.
- The second way is to connect $v_i$ and $v_j$ only if $v_j$ is in $k$-nearest neighbors of $v_i$ and $v_i$ is in $k$-nearest neighbors of $v_j$. The resulting graph is called *mutual k-nearest neighbor graph*.

After connecting the vertices, the edges are weighted by the similarity of endpoints.

**Fully connected**: in this case all points are connected with each other and the edges are weighted by the similarity function $x_i,_j$. An important issue is that if all are connected, it is important that the similarity function reflects the local neighborhoods. A popular similarity function is the Gaussian similarity $f(x_i, x_j) = \exp(-\|x_i - x_j\|^2/(2\sigma^2))$. The parameter $\sigma$ controls the width of the neighborhood and provides a role similar to that of $\epsilon$ in the $\epsilon$-neighborhood graph. The paper [105] provides a discussion on choice of similarity graph construction and the resultant cluster based on type.

## 17.8.3 Graph Laplacians

Graph Laplacian matrices are the principal tool for spectral clustering and there is dedicated area of study for those matrices [36]. There are variants of graph Laplacians, and unfortunately, is no unique definition of a matrix that is exactly "graph Laplacian". Let $G = (\mathcal{V}, \mathcal{E})$ be an undirected graph with weight matrix $\mathcal{W}$ with $w_{i,j} \geq 0$. Using eigenvectors of matrix, do not assume them to be normalized, i.e., constant vector $\vec{f}$ and for some $a$ the same. Eigenvalues will be ordered in ascending order.

### 17.8.3.1 Unnormalized Graph Laplacian

The unnormalized graph Laplacian $L$ is defined as $L = D - W$. Some of properties of graph Laplacian that are critical for spectral clustering are given below. For more detail see overview in [116, 117].

**Properties of graph Laplacian**: Matrix $L$ has the following properties:

- for every vector $f \in \mathbb{R}^n$, $f^T L f = \sum_{i,j} w_{ij}(f_i - f_j)^2$
- $L$ is symmetric and positive semi-definite.
- The smallest eigenvalue of $L$ is 0 with the corresponding eigenvector $\vec{f}$ (constant vector).
- $L$ has nonnegative real-valued eigenvalues $0 = \lambda_1 \leq \lambda_2 \leq \dots \leq \lambda_n$.

Proof of these properties is available in [105]. It is noticeable that self-edges in a graph do not change properties of graph Laplacians. The unnormalized graph Laplacian, its eigenvectors and eigenvalues can describe many properties of graph [116, 117]. One such property important for spectral clustering is follows:

**Number of connected components and spectrum of L**: For an undirected graph $\mathcal{G}$ with non-negative weights, the multiplicity $k$ of the eigenvalue 0 of $L$ equals the number of connected components. Proof of this property can be found in [105].

### 17.8.3.2 Normalized Graph Laplacians

The following matrices are known as normalized graph Laplacians [36]:

```
L_s := D^{-1/2}LD^{-1/2} = I - D^{-1/2}WD^{-1/2}
L_rw := D^{-1}L = I - D^{-1}W
```

$L_s$ is a symmetric matrix with $L_{rw}$ related to random walk. Some of properties of normalized Laplacians are as follows:

- for every $f \in \mathbb{R}^n$, $f^T L_s f = \sum_{i,j} w_{ij}(\frac{f_i}{\sqrt{d_i}} - \frac{f_j}{\sqrt{d_j}})^2$
- $\lambda$ is an eigenvalue of $L_{rw}$ with eigenvector $u$ iff $\lambda$ is an eigenvalue of $L_s$ with eigenvector $w = D^{1/2}u$.
- $\lambda$ is an eigenvalue of $L_{rw}$ with eigenvector $u$ iff the generalized eigenproblem $Lu = \lambda Du$ is solved by $\lambda$ and $u$.
- 0 is an eigenvalue of $L_{rw}$ with constant eigenvector and an eigenvalue of $L_s$ with eigenvector $D^{-1/2}u$.
- $L_s$ and $L_{rw}$ are positive semidefinite with $n$ nonnegative real-valued eigenvalues $0 = \lambda_1 \le \lambda_2 \le \dots \le \lambda_n$.

For proofs of these properties, please see [105].

**Number of connected components and spectra of $L_s$ and $L_{rw}$**: Similar to unnormalized Laplacians, for (non-negative) weighted undirected graph $\mathcal{G}$ the multiplicity $k$ of the eigenvalue 0 of both $L_s$ and $L_{rw}$ equals the number of connected components in the graph.

## 17.8.4 Spectral Clustering Algorithms

Let $x_1, x_2, \dots, x_n$ be $n$ data points and $s_{ij} = s(x_i, x_j)$ be a pairwise similarity function between points. We assume $s_{ij}$ is symmetric and nonnegative. Let $S = (s_{ij})_{i,j=1,\dots,n}$ be the similarity matrix. The following algorithm describes the unnormalized spectral clustering.

**Algorithm 39 Unnormalized Spectral Clustering [105]**
**Input:** Similarity Matrix $S \in \mathbb{R}^{n \times n}$, number $k$ of clusters
- Construct Similarity Graph (using a method from 17.8.2)
- Let $W$ be the adjacency matrix
- Calculate unnormalized Laplacian $L$
- Compute first $k$ eigenvectors $l_1, l_2, \dots, l_k$ of $L$
- Let $U \in \mathbb{R}^{n \times k}$ be the matrix containing $l_1, l_2, \dots, l_k$ as columns
- Let $y_i \in \mathbb{R}^k$ be the $i$-th row of $U$ for $i=1, 2, \dots, n$
- Cluster points $y_i$ for $i=1, 2, \dots, n$ into $k$ clusters $C_1, C_2, \dots, C_k$ using $k$-means algorithm
**Output** $A_1, A_2, \dots, A_k$ with $A_l = \{y_j | y_j \in C_l\}$

For normalized graph Laplacians, there are two versions of normalized spectral clustering. Shi and Malik [151] proposed the following normalized spectral clustering algorithm [105]. Since the
