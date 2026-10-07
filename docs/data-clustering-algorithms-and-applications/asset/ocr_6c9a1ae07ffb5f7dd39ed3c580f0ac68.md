# Spectral Clustering

Data Symmetric KNN Spectral Clustering

![](bbox=[0.125, 0.11, 0.875, 0.2])

**FIGURE 8.2:** Example illustrating three steps of spectral clustering. (From Tenenbaum, de Silva, and Langford, *Science*, 290(5550):2319–2323, 2000.)

# 8.2 Similarity Graph

Let the set of data points, which we wish to partition into $k$ subsets, be denoted by $X = \{x_1, ..., x_n\}$ in $\mathbb{R}^m$. In order to perform spectral clustering, we first need to represent this data in the form of an undirected "similarity graph” $G = (V, E)$. Each data point $x_i$ is represented by a vertex $v_i$ and $E$ refers to the edges between vertices. Note that $x_i$ is a vector which denotes the data point $v_i$ is a vertex without any attributes. Then we can use a nonnegative weighted $n$ by $n$ adjacency matrix (or affinity matrix) to describe $G$, where $W = \{W_{ij}\}_{i,j=1}^n$. Note that $W_{ij}$ equals 0 when vertices $v_i$ and $v_j$ are not connected. Since spectral clustering algorithms aim at partitioning the vertices to leaves in the same cluster have high similarity and in different clusters have low similarity, it becomes critical to choose an effective method to construct such an adjacency matrix.

Recent studies in graph theory [8] and manifold learning [50] have demonstrated that the adjacency matrix models the local geometric structure of the data points. This issue will be discussed in more detail in Section 8.7. Based on this rule, we introduce three ways to construct $W$ [2, 31]:

+   **1. K-nearest neighbor graph:** The idea is that $v_i$ is connected with $v_j$ when $v_j$ is among the $K$-nearest neighbors of $v_i$ or $v_i$ is among the $K$-nearest neighbors of $v_j$. The distance is computed based on the original orientation of the data points $x_i$ and $x_j$. Some examples include $\ell_1$-norm, $\ell_2$-norm, and cosine distance. The graph structure is usually the $k$-nearest neighbor graph. The algorithm is to connect $v_i$ and $v_j$ when they are mutual in the neighborhood of each other. This is referred to as the mutual $K$-nearest neighbor graph or symmetric $K$-nearest neighbor graph. In both cases, after adding the edges according to the similarity of their endpoints or endpoints, we can assign weights to the edges or adopt a 0–1 weight

+   **2. ε-neighborhood graph:** In this kind of graph, vertices are connected only when the pairwise distance $\|x_i - x_j\|$ is smaller than $\varepsilon$. However, this method often leads to graphs with disconnected components if $\varepsilon$ is not carefully chosen.

+   **3. Fully connected graph:** In this case, we connect all vertices with positive similarity. Since the adjacency matrix models the local neighborhood, the selection of the similarity function itself becomes tricky. An example is the heat kernel function:

```
$W_{ij} = e^{-\frac{\|x_i-x_j\|^2}{\sigma^2}}$
```

where $\sigma$ controls the width of the neighborhoods. It is suggested in [60] that $\sigma$ could be tuned with respect to the pair of vertices. Besides the problem of choosing an appropriate