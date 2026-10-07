
# Nonnegative Matrix Factorizations for Clustering: A Survey

It has also been shown that symmetric matrix factorization, a special case of nonnegative matrix factorization, is equivalent to sophisticated normalized cut clustering [100]. Given the adjacent matrix W of a graph, it can be easily seen that the following matrix factorization

```
$$\min_{H:H\ge0} ||\tilde{W} - HH^T||^2, \quad (7.8)
```

where

```
$\tilde{W} = D^{-1/2}WD^{-1/2}, D = \text{diag}(d_1, \cdots, d_n), d_i = \sum_{j} w_{ij},
```

is equivalent to Normalized Cut spectral clustering [35, 118].

## 7.2.4 NMF Boundedness Theorem

NMF differs from SVD (Singular Value Decomposition) due to the absence of cancellation of plus and minus signs. What is the fundamental significance of this absence of cancellation? The Boundedness Property offers the theoretical foundation for the normalization of F and G in $X = FG^T$. A matrix $A$ is bounded, if $0 \le A_{ij} \le 1$. Note that for any input matrix, we can rescue it into the bound.

The boundedness property of NMF states: if $X$ is bounded, then the factors F, G must also be bounded. More precisely:

**Theorem 4 (Bounded Theorem)** Let $0 \le X \le 1$. There exists a diagonal matrix $D$ such that we rescale $X = FG = (FD)(GD)^T$, the matrices satisfy $0 \le F'_{ij}G'_{ij} \le 1$. $D$ is constructed this way: $D_{jj}=F_j^{-1/2}, D=\text{diag}(f_1, \cdots, f_k), f_j=\max_i F_{ij}$ and $G=\text{diag}(g_1, \cdots, g_k), g_k=\max_i G_{ik}$,

This theorem assures the existence of an appropriate scale such that both W and H are bounded, i.e., their elements cannot exceed the magnitude of the input data. Note that SVD decomposition does not have the boundedness property. In this case, even if the input data are in the range of $0 \le X_{ij} \le 1$, we cannot guarantee that for $|F_{ij}| \le 1$ and $|V_{ij}| \le 1$.

## 7.3 NMF Clustering Capabilities

### 7.3.1 Examples

We demonstrate the clustering capabilities of NMF using several examples. Figures 7.1 and 7.2 present the computed $F$ factors (images) on two datasets: ORL image dataset and Digits image dataset. Here each image is represented as a vector of gray pixel values. Note that by Theorem 1, $F$ factors are cluster centroids (representatives of clusters). Intuitively, the images are *representatives* of the original images. The examples show that NMF provides a holistic view of the datasets.

### 7.3.2 Analysis

In general, the advantages of NMF over the existing unsupervised learning methods can be summarized as follows. NMF can model widely varying distributions due to the flexibility of matrix factorization compared to the rigid spherical clusters that the $K$-means clustering objective attempts to capture.

![](img/b94d85a2e934001944bcc21abd9a9943_180_0.png)

**FIGURE 7.1:** Left: ORL face image dataset, containing 100 images of 10 persons. Middle/Right: Computed NMF factors $F=(f_1, \dots, f_{16})$ for 2 runs with random initialization.

When the data distribution is far from a spherical clustering, NMF can have advantages. Another advantage of NMF is that NMF can do both hard and soft clustering simultaneously.

Figure 7.3 gives an example. The 2-D dataset in the left consists of 38 data points and the $G$ values are in the right figure. As seen in the figure, $G$ values for $\{C, D, E\}$ indicate they are fractionally assigned to different clusters. As a result, NMF is able to perform soft clustering.

The third advantage is that NMF is able to perform simultaneously clustering of the rows (features) and the columns (data points) of an input data matrix. Consider the following NMF objective with orthonormal constraints on the factor matrices.

> $J_{orth} = \|X - FG^T\|^2, \text{ s.t. } F \ge 0, G \ge 0, F^TF = I, G^TG = I.$

The orthonormal constraints and the nonnegative constraints in Equation (7.9) make the resulted $F$ and $G$ approximate the $K$-means clustering results on both features and data points [35]. The fourth advantage is that many other data mining and machine learning problems can be reformulated as NMF problems.

![](img/b94d85a2e934001944bcc21abd9a9943_180_1.png)

**FIGURE 7.2:** Left: Digits image dataset. Middle/Right: Computed NMF factors $F=(f_1, \dots, f_{16})$ for 2 runs with random initialization.

![](img/b94d85a2e934001944bcc21abd9a9943_181_0.png)

**FIGURE 7.3:** Left: A 2D dataset of 38 data points. Right: The $G=(g_1,g_2)$ values are shown as blue and red colors. Points in regions $\{A,B\}$ are numbered 1–30, where $g_1$ and $g_2$ values differ significantly, indicating that these points are uniquely clustered either cluster A or cluster B (hard clustering). Points in regions $\{C,D,E\}$ are numbered 31–38, where $g_1$ and $g_2$ values are close, indicating that these points are fractionally clustered into clusters A and B (soft clustering).

## 7.4 NMF Algorithms

### 7.4.1 Introduction

The algorithms for matrix factorizations are generally iterative updating procedures: updating one factor while fixing the others. Existing algorithms for NMF include multiplicative updates of Lee and Seung [68, 67], alternating least squares (ANLS) [88, 7], alternating nonnegative least squares [59, 60], gradient descent methods [56, 98], projected gradient methods [79], and Newton-type algorithms [134, 58]. More details on NMF algorithms can be found in [105, 7, 24]. In this section, we provide an outline of the algorithm development for orthogonal NMF and also discuss several practical issues when applying NMF for clustering.

### 7.4.2 Algorithm Development

Here we provide an outline of the algorithm development for orthogonal NMF. We wish to solve the optimization problem

```
$min J(F) = ||X - FG^T||^2, \quad s.t. \quad F^TF = I,\quad (7.10)$
```

where $X, G \ge 0$ are fixed. We show that given an initial $F$, the updating algorithm

```
$F_{ik} \leftarrow F_{ik} \frac{(XG)_{ik}}{(F^TXF)_{ik}},\quad (7.11)$
```

correctly identifies a local minimum of this problem.

We can use the gradient-descent method, the current approach, to update $F$ on the Stiefel manifold. Note that in Equation (7.11) we use the orthogonality $F^TF = I$

```
(-2G + A)_{ik} = 0. (7.12)
```

### 7.4.3 Practical Issues in NMF Algorithms

In the following we discuss several practical issues when applying NMF for clustering.

#### 7.4.3.1 Initialization

Similar to K-means, initialization also plays an important role when applying NMF for clustering since the objective function has many local minima [109, 53]. The intrinsic alternating minimization in NMF algorithms is nonconvex.

A random initialization, where the factor matrices are initialized as random matrices, is generally not effective as it often leads to slow convergence to a local minimum. Many different techniques have been developed for improving the random initialization:

- Multiple initializations: The core idea is to perform multiple runs using different initializations and select the best estimates from multiple runs. This method needs to perform NMF multiple times and is computationally expensive.
- Factorization-based initialization: Note that NMF is a constrained low rank matrix factorization; hence, we use the results from low rank factorization methods as the initialization [10]. Typical examples include SVD-based initialization [10] and CUR decomposition-based initialization [66].
- Clustering-based initialization: If we think of NMF as a clustering process, then the initialization strategy based on the results from other clustering algorithms (e.g., spherical k-means [127, 41], divergence-based k-means [131], and fuzzy clustering [142]).

A comparison of different initialization methods can be found in [66]. Note that both factorization-based and clustering-based initialization methods are able to lead to rapid error reduction and faster convergence.

#### 7.4.3.2 Stopping Criteria

Beyond a predefined number of iterations or a fixed running time, there are simple heuristics that be the stopping criteria for the iterative algorithms of NMF: (1) the objective function
