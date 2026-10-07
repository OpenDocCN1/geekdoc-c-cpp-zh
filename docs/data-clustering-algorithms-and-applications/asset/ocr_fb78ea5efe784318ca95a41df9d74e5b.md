# An Introduction to Cluster Analysis

onto distant points in this line. We would like to determine values of $y_i$ which minimize the objective function O:

```
$O = \sum_{i=1}^{n} \sum_{j=1}^{n} W_{ij} \cdot (y_i - y_j)^2 \quad (1.4)$
```

The objective function O can be rewritten in terms of the Laplacian matrix $W$. The Laplacian matrix is defined as $D - W$, where $D$ is a diagonal matrix satisfying $D_{ii} = \sum_{j=1}^{n} W_{ij}$. Let $\mathfrak{y} = (y_1, \dots, y_n)$. The objective function can be rewritten as:

```
$O = 2 \cdot \mathfrak{y}^T \cdot D \cdot \mathfrak{y} \quad (1.5)$
```

We need to consider a scaling constraint in order to ensure the trivial value of $y_i = 0$ for all $i$ is not selected by the problem. A possible scaling constraint is as follows:

```
$\mathfrak{y}^T \cdot D \cdot \mathfrak{y} = 1 \quad (1.66)$
```

Note that the matrix $D$ provides different weights to the data items, because it is assumed that nodes with greater similarity to different data items are more involved in the clustering process. This optimization formula is in generalized eigenvector format, and the value of $\mathfrak{y}$ is optimized by selecting the smallest eigenvalue for which the generalized eigenvector relationship $L\cdot\mathfrak{y} = \lambda\cdot D\cdot\mathfrak{y}$ is satisfied. In practice, the smallest eigenvalue corresponds to the trivial solution, where $\mathfrak{y}$ is the (normalized) unit vector. This trivial eigenvector is noninformative. Therefore, it can be discarded, and it is not used in the analysis. The second-smallest eigenvalue provides an optimal solution, which is more informative.

This model can be generalized to determining all the eigenvectors in ascending order of value. Such directions correspond to directions in the data space, which result in the best mapping. The set of $n$ eigenvectors $\lambda_1, \lambda_2, \dots, \lambda_n$ (of which the first is trivial), with corresponding eigenvectors representing the vector representation of the data points along each eigenvector denoted by $v^1, \dots, v^n$. What do the large and small magnitude eigenvectors intuitively represent in the transformed space? By using the order of the data items along a small magnitude eigenvector to create a cut, the weight of the edges across the cut is likely to be small. Thus, this represents a cluster of the data items. At the same time, if $k$ largest eigenvectors are picked, the then representations $v^1, \dots, v^k$ preserve the maximum amount of information. Thus, spectral methods can be used to simultaneously perform clustering and dimensionality reduction (possibly nonlinear) shape of the data, which arguably at a rather high cost [78]. The specific locality reduction technique of this section is discussed in detail in [19]. An excellent survey on spectral clustering methods may be found in [35, 63]. These methods are also discussed in Chapter 8 of this book.

# 1.2.6 The High Dimensional Scenario

The high dimensional scenario is particularly challenging for clustering because of the large variations in the behavior of the data attributes over different parts of the data. This leads to numerous challenges in data mining problems such as clustering, nearest neighbor search, and outlier analysis. It should be noted that many of the algorithms for these problems are dependent upon the use of distances as an important subroutine. However, with increasing dimensionality, the distances seem to increasingly lose their effectiveness and statistical significance because irrelevant attributes. The problem is that a smaller fraction of the attributes remains relevant with increasing dimensionality, which leads to the blurring of the data and increasing