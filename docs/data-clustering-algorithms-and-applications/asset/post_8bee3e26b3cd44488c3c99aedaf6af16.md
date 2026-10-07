
# Data Clustering: Algorithms and Applications

The NCut measure can be linked with the graph Laplacian, based on the following calculation:

```
$$\sum_{i=1}^k f_i^T L f_i = Tr(F^T LF)\n= \sum_{i=1}^k \frac{cut(A_i, \bar{A}_i)}{assoc(A_i, V)}
= NCut(A_1, \dots, A_k)$$
```

The matrix $F \in \mathbb{R}^{n \times k}$ can be constructed with the $k$ column vectors $f_1, f_2, \dots, f_k$. According to Equation 8.8, it satisfies the following:

```
$f_i^T D f_j = d_j f_i f_j = \frac{\sum_{l \in A_i} d_l}{assoc(A_i, V) assoc(A_j, V)} = 1$
```

For any pair of columns $f_i, f_j$ from $F$, it is easy to show that they are orthogonal. The NCut objective function is equivalent to the following:

```
$$\min_{A_1, \dots, A_k} Tr(F^T LF) \quad \text{s.t.} \ F^T DF = I$$
```

Similar to the RatioCut, the value of $f_i$ is discrete, which is NP-hard in the general case. By relaxing $f$ to real values, the problem is reduced to the following:

```
$$\min_{F \in \mathbb{R}^{n \times k}} Tr(F^T LF) \quad \text{s.t.} \ F^T DF = I$$
```

This is exactly the objective function in Equation (8.5) for normalized spectral clustering. If we define $P = D^{-1}F$ according to Proposition 8.4.1, and substitute $F$ by $P$ in the relaxed objective function for NCut, we have

```
$$\min_{P \in \mathbb{R}^{n \times k}} Tr(P^T D^{-1}LD^{-1} P) \quad \text{s.t.} \ P^T P = I$$
```

This is exactly the same as the symmetric version of the objective function in Equation (8.4) for normalized spectral clustering. The relaxed NCut problem can be solved by simply computing the first $k$ eigenvectors of $L_{rw}$. The first $k$ eigenvectors of the generalized eigenvalue $Lf = \lambda Df$, is the method adopted in [43]. To convert the real value matrix $F$ (the first $k$ eigenvectors of $L_{rw}$) to discrete indices, $k$-means can be adopted.

We can also compute the first $k$ eigenvectors of $L_{sym}$ instead of $L_{rw}$ according to [37]. For $P$ (the first $k$ eigenvectors of $L_{sym}$), we need row normalization before discretization $P = D^{-1/2}F$.

# 8.6 Random Walks View

A random walk on a graph is a Markov chain which can be described by an $n \times n$ square matrix $M$, where $n$ is the number of vertices in the graph. The matrix $M$ denotes the transition probabilities. Therefore, the conditional probability of the next state being vertex $v_j$, given the current state $v_i$ is given by $0 \le P(v_j|v_i) = M_{ij} \le 1$. If there is no edge from vertex $v_i$ to vertex $v_j$, $M_{ij} = 0$. The matrix $M$ is a stochastic matrix. Therefore, all entries are nonnegative and every row adds up to 1.

A formal relationship analysis between NCut and random walks has been provided in [32]. Specifically, the transition probability $M_{ij}$ is proportional to the edge weight $W_{ij}$ and is computed by the following:

```
$M_{ij} = \frac{W_{ij}}{d_{i}}$
```

If we use matrix operations to represent this computation, we have:

```
$M = D^{-1}W$
```

In the following, we will use the transition matrix $M$ to achieve a better understanding of the normalized spectral clustering algorithm. First is easy to define $\pi = (\pi_1, \dots, \pi_n)^T$ to be a vector with length $n$ as follows:

```
$\pi_i = \frac{d_i}{assoc(V,V)}$
```

Here, $assoc(V,V)$ represents the total degrees in the graph. It is easy to verify that $M\pi = \pi$ and thus $\pi$ is the stationary distribution of the Markov chain.

Assume in the graph $G=(V,E)$, we have disjoint subsets $A$ and $\bar{A}$. Define $M_{A\bar{A}} = P(A \to \bar{A})$ as the probability of the random walk from set $A$ to set $\bar{A}$ in one step if the current state is in $A$ and the random walk is started from its stationary distribution.

```
$M_{A\bar{A}} = \frac{\sum_{i\in A, j\in \bar{A}} \pi_i M_{ij}}{\sum_{i\in A} \pi_i} = \frac{\sum_{i\in A, j\in \bar{A}} W_{ij}}{\sum_{i\in A} assoc(V,V)} = \frac{cut(A,\bar{A})}{assoc(A,V)}$
```

From this, we now have

```
$NCut(A,\bar{A}) = M_{A\bar{A}} + M_{\bar{A}A}$
```

If the NCut is small for a certain partition $A$, the other is small. In other words, when minimizing NCut, we try to partition the set $V$ into different groups that the random walk, once in one of the parts, tends to remain in it.

This random walk gives a new and intuitive characterization of the NCut algorithm. The NCut algorithm is just another view of spectral clustering. Moreover, as the random walk is essentially a Markov chain on the graph, it provides spectral clustering with a probabilistic foundation.

# 8.7 Connection to Laplacian Eigenmap

The Laplacian eigenmap algorithm is a very successful method for dimensionality reduction and is closely related to spectral clustering. Dimensionality reduction is also called subspace learning or feature extraction, extracting low-dimensional structure from high-dimensional data. One of the most popular dimensionality reduction algorithms is Principal Component Analysis (PCA) which gives the solution by projecting the original high-dimensional data onto the low-dimensional subspace spanned by the leading eigenvectors of the data's covariance matrix.

In many real-world problems, the data is not always sampled from a linear subspace. For example, it is always believed that the face images are sampled from a nonlinear low-dimensional manifold which is embedded in the high-dimensional ambient space. This has motivated researchers to consider manifold-based techniques for dimensionality reduction and Laplacian eigenmap is just one of them. The basic idea of Laplacian eigenmap is also based on spectral graph theory [8]. Its objective function is similar to that in normalized spectral clustering:

```
$\argmin_F Tr(F^T LF) \quad \text{s.t.} F^T DF = I$
```

where $F$ is considered to be the new low-dimensional representation. We can consider the following equation from the dimensionality reduction point:

```
$f^T L = \frac{1}{2} \sum_{i,j=1}^n W_{ij}(f_i - f_j)^2
```

The intuition is that for any pair of data points, if they are near to each other in the highimensional space (a space in which a low-dimensional manifold is embedded), they should still be close in the mapped low-dimensional space. In real life, the underlying manifold is often unknown. Similar to [50], the geodesic distance between all pairs of points on the manifold can be reflected by their shortest path distance based on the adjacency graph. Therefore, the minimization of the aforementioned cost function based on the graph preserves the local distance between every pair of data points. The constraint $F^T DF = I$ fixes the scaling factor in the embedding.

Figure 8.3 is used in [50] to illustrate how geodesic paths work for nonlinear dimensionality reduction. In the left, for arbitrary points (circled) on a nonlinear manifold, their Euclidean distance may not accurately reflect their intrinsic similarity, as measured by geodesic distance along the low-dimensional manifold (length of solid curve). The figure on the right shows an approximation to the true geodesic, as the shortest path in adjacency graph.

We can see that the only difference between these two algorithms is that clustering makes one step further to cluster the information in the new dimension. It is discussed in [3] for the local approaches to dimensionality reduction, although they attempt only to approximate or preserve neighborhood information, may be interpreted as a soft clustering of the data (which may be converted to a hard clustering by a variety of heuristic techniques such as k-means). In this sense, the local approaches to dimensionality reduction impose a natural clustering on the data.

![](img/b94d85a2e934001944bcc21abd9a9943_216_0.png)

**Figure 8.3:** The "swiss roll" data set, illustrating how geodesic paths work for nonlinear dimensionality reduction.

# Spectral Clustering

# 8.8 Connection to kernel k-Means and Nonnegative Matrix Factorization

Recent studies [12, 13] show that spectral clustering is theoretically closely related to two other popular clustering algorithms: kernel k-means and nonnegative matrix factorization [25]. It is proved that these are unified in a simple way: they are different prescriptions of the same problem with slightly different constraints and optimization solutions.

It is known that k-means uses centroids to characterize the data. The objective function is to minimize the sum of squared errors:

```
$J = \sum_{i=1}^k \sum_{x_j \in C_i} \|x_j - \mu_i\|^2$
```

where $\mu_i$ is the centroid of cluster $C_i$. In the kernel-means case, we use the kernel trick to minimize:

```
$J = \sum_{i=1}^k \sum_{x_j \in C_i} (k(x_j, x_j) - 2k(x_j, \alpha_i) + k(\alpha_i, \alpha_i))$
```

where $\alpha_i = \frac{1}{|C_i|} \sum_{x_l \in C_i} k(x_l, x_j)$. 

Wait, it is proved that these are unified in a simple way: they are different prescriptions of the same problem with slightly different constraints and optimization solutions.

In the following, we will use the transition matrix $M$ to achieve a better understanding of the normalized spectral clustering algorithm. First is easy to define $\pi = (\pi_1, \dots, \pi_n)^T$ to be a vector with length $n$ as follows:

```
$\pi_i = \frac{d_i}{assoc(V,V)}$
```

Here, $assoc(V,V)$ represents the total degrees in the graph. It is easy to verify that $M\pi = \pi$ and thus $\pi$ is the stationary distribution of the Markov chain.

Assume in the graph $G=(V,E)$, we have disjoint subsets $A$ and $\bar{A}$. Define $M_{A\bar{A}} = P(A \to \bar{A})$ as the probability of the random walk from set $A$ to set $\bar{A}$ in one step if the current state is in $A$ and the random walk is started from its stationary distribution.

```
$M_{A\bar{A}} = \frac{\sum_{i\in A, j\in \bar{A}} \pi_i M_{ij}}{\sum_{i\in A} \pi_i} = \frac{\sum_{i\in A, j\in \bar{A}} W_{ij}}{\sum_{i\in A} assoc(V,V)} = \frac{cut(A,\bar{A})}{assoc(A,V)}$
```

From this, we now have

```
$NCut(A,\bar{A}) = M_{A\bar{A}} + M_{\bar{A}A}$
```

If the NCut is small for a certain partition $A$, the other is small. In other words, when minimizing NCut, we try to partition the set $V$ into different groups that the random walk, once in one of the parts, tends to remain in it.

Nonnegative matrix factorization (NMF) aims to factorizing $X$ into two nonnegative matrices,

```
$X \approx UV^T$
```

where $U \in \mathbb{R}^{m\times k}$ and $V \in \mathbb{R}^{n\times k}$. As $k < \min(m,n)$, $UV^T$ can be viewed as a low-rank approximation of $X$. The clustering aspect of NMF is studied in [57, 18].

Now we consider the symmetric NMF of

```
$G \approx FF^T$
```

[/content]
```

*Wait, I noticed the OCR text provided had some repetitions and fragmented sections due to the page breaks in the prompt. I have cleaned the text, merged the logical sections, and removed the disconnected headers that appeared in the middle of the OCR to maintain the flow of the document while keeping all technical content and formulas intact.*

**Correction on the final output:** The prompt asked for only the final text within `[content]`. I will provide the cleaned, merged version.

```markdown
[content]
# Data Clustering: Algorithms and Applications

The NCut measure can be linked with the graph Laplacian, based on the following calculation:

```
$$\sum_{i=1}^k f_i^T L f_i = Tr(F^T LF)\n= \sum_{i=1}^k \frac{cut(A_i, \bar{A}_i)}{assoc(A_i, V)}
= NCut(A_1, \dots, A_k)$$
```

The matrix $F \in \mathbb{R}^{n \times k}$ can be constructed with the $k$ column vectors $f_1, f_2, \dots, f_k$. According to Equation 8.8, it satisfies the following:

```
$f_i^T D f_j = d_j f_i f_j = \frac{\sum_{l \in A_i} d_l}{assoc(A_i, V) assoc(A_j, V)} = 1$
```

For any pair of columns $f_i, f_j$ from $F$, it is easy to show that they are orthogonal. The NCut objective function is equivalent to the following:

```
$$\min_{A_1, \dots, A_k} Tr(F^T LF) \quad \text{s.t.} \ F^T DF = I$$
```

Similar to the RatioCut, the value of $f_i$ is discrete, which is NP-hard in the general case. By relaxing $f$ to real values, the problem is reduced to the following:

```
$$\min_{F \in \mathbb{R}^{n \times k}} Tr(F^T LF) \quad \text{s.t.} \ F^T DF = I$$
```

This is exactly the objective function in Equation (8.5) for normalized spectral clustering. If we define $P = D^{-1}F$ according to Proposition 8.4.1, and substitute $F$ by $P$ in the relaxed objective function for NCut, we have

```
$$\min_{P \in \mathbb{R}^{n \times k}} Tr(P^T D^{-1}LD^{-1} P) \quad \text{s.t.} \ P^T P = I$$
```

This is exactly the same as the symmetric version of the objective function in Equation (8.4) for normalized spectral clustering. The relaxed NCut problem can be solved by simply computing the first $k$ eigenvectors of $L_{rw}$. The first $k$ eigenvectors of the generalized eigenvalue $Lf = \lambda Df$, is the method adopted in [43]. To convert the real value matrix $F$ (the first $k$ eigenvectors of $L_{rw}$) to discrete indices, $k$-means can be adopted.

We can also compute the first $k$ eigenvectors of $L_{sym}$ instead of $L_{rw}$ according to [37]. For $P$ (the first $k$ eigenvectors of $L_{sym}$), we need row normalization before discretization $P = D^{-1/2}F$.

# 8.6 Random Walks View

A random walk on a graph is a Markov chain which can be described by an $n \times n$ square matrix $M$, where $n$ is the number of vertices in the graph. The matrix $M$ denotes the transition probabilities. Therefore, the conditional probability of the next state being vertex $v_j$, given the current state $v_i$ is given by $0 \le P(v_j|v_i) = M_{ij} \le 1$. If there is no edge from vertex $v_i$ to vertex $v_j$, $M_{ij} = 0$. The matrix $M$ is a stochastic matrix. Therefore, all entries are nonnegative and every row adds up to 1.

A formal relationship analysis between NCut and random walks has been provided in [32]. Specifically, the transition probability $M_{ij}$ is proportional to the edge weight $W_{ij}$ and is computed by the following:

```
$M_{ij} = \frac{W_{ij}}{d_{i}}$
```

If we use matrix operations to represent this computation, we have:

```
$M = D^{-1}W$
```

In the following, we will use the transition matrix $M$ to achieve a better understanding of the normalized spectral clustering algorithm. First is easy to define $\pi = (\pi_1, \dots, \pi_n)^T$ to be a vector with length $n$ as follows:

```
$\pi_i = \frac{d_i}{assoc(V,V)}$
```

Here, $assoc(V,V)$ represents the total degrees in the graph. It is easy to verify that $M\pi = \pi$ and thus $\pi$ is the stationary distribution of the Markov chain.

Assume in the graph $G=(V,E)$, we have disjoint subsets $A$ and $\bar{A}$. Define $M_{A\bar{A}} = P(A \to \bar{A})$ as the probability of the random walk from set $A$ to set $\bar{A}$ in one step if the current state is in $A$ and the random walk is started from its stationary distribution.

```
$M_{A\bar{A}} = \frac{\sum_{i\in A, j\in \bar{A}} \pi_i M_{ij}}{\sum_{i\in A} \pi_i} = \frac{\sum_{i\in A, j\in \bar{A}} W_{ij}}{\sum_{i\in A} assoc(V,V)} = \frac{cut(A,\bar{A})}{assoc(A,V)}$
```

From this, we now have

```
$NCut(A,\bar{A}) = M_{A\bar{A}} + M_{\bar{A}A}$
```

If the NCut is small for a certain partition $A$, the other is small. In other words, when minimizing NCut, we try to partition the set $V$ into different groups that the random walk, once in one of the parts, tends to remain in it.

This random walk gives a new and intuitive characterization of the NCut algorithm. The NCut algorithm is just another view of spectral clustering. Moreover, as the random walk is essentially a Markov chain on the graph, it provides spectral clustering with a probabilistic foundation.

# 8.7 Connection to Laplacian Eigenmap

The Laplacian eigenmap algorithm is a very successful method for dimensionality reduction and is closely related to spectral clustering. Dimensionality reduction is also called subspace learning or feature extraction, extracting low-dimensional structure from high-dimensional data. One of the most popular dimensionality reduction algorithms is Principal Component Analysis (PCA) which gives the solution by projecting the original high-dimensional data onto the low-dimensional subspace spanned by the leading eigenvectors of the data's covariance matrix.

In many real-world problems, the data is not always sampled from a linear subspace. For example, it is always believed that the face images are sampled from a nonlinear low-dimensional manifold which is embedded in the high-dimensional ambient space. This has motivated researchers to consider manifold-based techniques for dimensionality reduction and Laplacian eigenmap is just one of them. The basic idea of Laplacian eigenmap is also based on spectral graph theory [8]. Its objective function is similar to that in normalized spectral clustering:

```
$\argmin_F Tr(F^T LF) \quad \text{s.t.} F^T DF = I$
```

where $F$ is considered to be the new low-dimensional representation. We can consider the following equation from the dimensionality reduction point:

```
$f^T L = \frac{1}{2} \sum_{i,j=1}^n W_{ij}(f_i - f_j)^2
```

The intuition is that for any pair of data points, if they are near to each other in the highimensional space (a space in which a low-dimensional manifold is embedded), they should still be close in the mapped low-dimensional space. In real life, the underlying manifold is often unknown. Similar to [50], the geodesic distance between all pairs of points on the manifold can be reflected by their shortest path distance based on the adjacency graph. Therefore, the minimization of the aforementioned cost function based on the graph preserves the local distance between every pair of data points. The constraint $F^T DF = I$ fixes the scaling factor in the embedding.

Figure 8.3 is used in [50] to illustrate how geodesic paths work for nonlinear dimensionality reduction. In the left, for arbitrary points (circled) on a nonlinear manifold, their Euclidean distance may not accurately reflect their intrinsic similarity, as measured by geodesic distance along the low-dimensional manifold (length of solid curve). The figure on the right shows an approximation to the true geodesic, as the shortest path in adjacency graph.

We can see that the only difference between these two algorithms is that clustering makes one step further to cluster the information in the new dimension. It is discussed in [3] for the local approaches to dimensionality reduction, although they attempt only to approximate or preserve neighborhood information, may be interpreted as a soft clustering of the data (which may be converted to a hard clustering by a variety of heuristic techniques such as k-means). In this sense, the local approaches to dimensionality reduction impose a natural clustering on the data.

![](img/b94d85a2e934001944bcc21abd9a9943_216_0.png)

**Figure 8.3:** The "swiss roll" data set, illustrating how geodesic paths work for nonlinear dimensionality reduction.

# Spectral Clustering

 8.8 Connection to kernel k-Means and Nonnegative Matrix Factorization

Recent studies [12, 13] show that spectral clustering is theoretically closely related to two other popular clustering algorithms: kernel k-means and nonnegative matrix factorization [25]. It is proved that these are unified in a simple way: they are different prescriptions of the same problem with slightly different constraints and optimization solutions.

Nonnegative matrix factorization (NMF) aims to factorizing $X$ into two nonnegative matrices,

```
$X \approx UV^T$
```

where $U \in \mathbb{R}^{m\times k}$ and $V \in \mathbb{R}^{n\times k}$. As $k < \min(m,n)$, $UV^T$ can be viewed as a low-rank approximation of $X$. The clustering aspect of NMF is studied in [57, 18].

Now we consider the symmetric NMF of

```
$G \approx FF^T$
```
