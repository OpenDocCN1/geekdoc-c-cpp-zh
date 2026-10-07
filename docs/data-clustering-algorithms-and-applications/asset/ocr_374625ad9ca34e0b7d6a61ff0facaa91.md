# Data Clustering: Algorithms and Applications

where $x_i$ and $x_j$ are connected samples in the k-Nearest-Neighbors graph and $\sigma$ is used as a predefined parameter. From $W$ a dense matrix is constructed as explained earlier in this chapter. Then, a graph Laplacian matrix $L = D - W$ is constructed. After that, MCFS follows the following equation:

```
$Ly = \lambda Dy$ (2.6)
```

Given $Y = [y_1, \dots, y_K]$, the eigenvectors of Equation (2.6), we can represent a subset of features by minimizing the objective function:

```
$$\min_{a_k} ||y_k - X^T a_k||^2\ns.t. \ ||a_k||_0 = 1$
```

Where $a_k$ is an $m$-dimensional vector and $||a_k||_0$ is the number of nonzero elements in $a_k$. Then, $K$ sparse coefficient vectors will be chosen to represent each cluster. For each feature $f_j$, the weight $a_k$ to $f_j$ will be chosen. Finally, MCFS will choose the top $l$ features. MCFS shows improvement over other methods such as LS like [9].

# 2.2.1.6 Weighting K-means

k-means is one of the most popular clustering techniques. It has been extensively used in data mining and machine learning problems. A large number of k-means variations have been proposed to handle feature selection [7, 68, 28, 25, 46]. Most of these variations by clustering the data into clusters. Then, weight is assigned to each feature. The feature that minimizes within-cluster distance and maximizes between-cluster difference is preferred and hence, gets higher weight. In [28], an entropy weighting k-means (EKWM) is proposed for subspace clustering. It simultaneously minimizes the within-cluster dispersion and maximizes the negative entropy in the clustering process. EKWM calculates the weight of each feature in each cluster by weighting the subset of features corresponding to each cluster, then, selected based on that weight.

In addition, [46] proposes feature weighting k-means clustering using generalized Fisher ratio that minimizes the ratio of average-within distortion over average-between distortion. In algorithm, several candidate clusters are generated and the one with the minimal Fisher ratio is deemed the final cluster.

Similarly, [25] proposes another variation of feature weighting k-means (W-k-means) that measures the weight of each feature based on its variance of the within-cluster distance. Algorithm 4 illustrates the process of W-k-means. It, iteratively, minimizes Equation (2.7) by fixing two parameters at each step and solving $\Psi$ until the third one. If there is no change in $\Psi$ after the minimization, the algorithm is said to converge.

```
$$\Psi(C, Z) = \sum_{i=1}^n \sum_{j=1}^m c_{ij} d(x_i, z_j)$ (2.7)
```

Where $C$ is a n-by-k partition matrix that contains binary values, $c_{il} = 1$ indicates that $x_i$ belongs to cluster $l$. $Z$ is the centroids and $d(\cdot, \cdot)$ is the distance metric. The weight vector and $eta$ is the parameter of the attribute weight. Minimizing $\Psi$ with respect to $C$ and $Z$ is straightforward. However, minimizing $\Psi$ with respect to $w$ depends on the value of $eta$. We refer to [25] for more about minimizing weight with respect to $w$.