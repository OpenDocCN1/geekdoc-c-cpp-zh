
positions of the original $K$-dimensional points. For this, the projection function $P$ should respect several constraints. The most common such constraints are

- Distance preservation: Given two points $p_1$ and $p_2$ in $D$, the distance between their projections $\|P(p_1) - P(p_2)\|$ in $\mathbb{R}^K$ should, ideally, be proportional with the distance $\|p_1 - p_2\|$ between the original points in $A^K$. If this happens, then when we find visually close projections, we can infer that these correspond to *similar* points in $A^K$. This effectively supports the so-called *query by example* task [Faloutsos and Lin 95].

- Neighborhood preservation: Given a point $p$ in $D$, the neighbors $P(p_k)$ of $P(p)$ in $\mathbb{R}^K$ should be, ideally, the same as the neighbors $p_i$ of $p$ in $A^K$. If this happens, then when we find a group of close projections, we can infer that they correspond to a group of similar points in $A^K$.

To better quantify the above preservation conditions, we define a so-called *stress function*

$$\sigma = \sqrt{\frac{\sum_{i,j} (\|p_i - p_j\| - \|P(p_i) - P(p_j)\|)^2}{\sum_{i,j} \|p_i - p_j\|^2}}$$ (11.9)

over all point-pairs $1 \le i \le N, 1 \le j \le N$ in our dataset $D$. $\sigma$ is a global value that measures how well the placement of the projections preserves distances on the average. Lower stress values indicate that $P$ has successfully preserved the relative distances from the high-dimensional space. Higher stress values indicate that distances are preserved less well. However, note that $\sigma$ is only a *global* indication of this preservation: Depending on the actual algorithm used, distances may be preserved better for certain point pairs than for others.

Techniques that compute a projection $P$ in order to minimize the stress function $\sigma$ are known under the global name of *dimensionality reduction methods*. Such methods differ in their implementation based on what type of information they use to compute $P$, as follows.

### 11.5.3 Multidimensional Scaling

A first type of dimensionality reduction method does not assume that we know the actual coordinates of the points $p_i$ in $A^K$. Rather, we only know the $N \times N$ square matrix $M = \{d_{ij}\}_{1 \le i \le N, 1 \le j \le N}$ of distances between these points. Here, $d_{ij} \in \mathbb{R}_+$ gives the distance, or dissimilarity, between the $K$-dimensional points $p_i$ and $p_j$. Of course, if we have access to the actual point coordinates, we can immediately compute such distances as

\( d_{ij} = \|p_i - p_j\| = \sqrt{\sum_{i=1}^K \delta(a'_i, a'_j)^2.} \) (11.10)

Here, the function \(\delta: A \times A \rightarrow \mathbb{R}_+\) gives the (one-dimensional) distance between two attribute values. For numerical attributes, \(\delta\) is the difference and \(d\) becomes the Euclidean distance in \(\mathbb{R}^K\). For non-numerical attributes, we must design a distance \(\delta\) that reflects the similarities of interest for the problem at hand. For instance, if the attributes are categorical, then we can use the distance

\(\delta(a \in A, a' \in A) = \left\{ \begin{array}{ll} 0 & \text{if } a = a' \\ 1 & \text{otherwise.} \end{array} \right.\) (11.11)

However, there are cases when we only know the interpoint distances \(d_{ij}\) but not the actual point coordinates. In the extreme case, we may not even know the space \(A^K\) or even its dimension \(K\). In such cases, the stress \(\sigma\) (Equation 11.9) becomes

\(\sigma = \sqrt{\frac{\sum_{i,j} (d_{ij} - \|P(p_i) - P(p_j)\|)^2}{\sum_{i,j} d_{ij}^2}},\) (11.12)

Methods that compute the projection \(P\) by directly minimizing \(\sigma\) given by Equation 11.12 are known under the name of *multidimensional scaling* (MDS) methods [Borg and Groenen 97, Cox and Cox 01, Mead 92]. The process of assigning \(k\)-dimensional coordinates to points in an unknown \(K\)-dimensional space, based only on the distances \(d_{ij}\), is also known under the name of *embedding*, since we "embed" points from an unknown space \(A^K\) into a known \(k\)-dimensional space. The MDS name reflects an important property of the computation: Distances between data points in the low-dimension \(k\) should be "scaled" versions of the distances between the same points in the original (unknown) high dimension. In the ideal case, we would like the two distances to be proportional to each other. MDS methods are useful also if they do not enforce a strict proportionality relation between the distances in the two spaces, as long as the distances are highly correlated.

Multidimensional scaling can be computed in a variety of ways. A simple, though not very computationally efficient way, is to use force-directed layouts. Consider a graph in which every data point \(i\) is a node, and every distance relation \(d_{ij}\) is an edge between the corresponding nodes \(i\) and \(j\). The edge stiffness is set to be inversely proportional to the distance \(d_{ij}\) between its nodes. Performing a force-directed layout on this graph (Section 11.4.2) will bring points

![](img/1274306e378c42ed8a0ad5669902d2a1_525_0.png)

Figure 11.31. Computation of projection coordinates in FastMap using only point-wise distances.

that are highly similar in the high-dimensional space close to each other in the \(k\)-dimensional layout space. In practice, several refinements must be applied to this basic idea to make it usable. Edges corresponding to very high distance values are not created, as these have a negligible impact on the layout. Reducing the number of edges from the theoretical maximum of \(N^2\), or in other words approximating the distance matrix \(M\) by a sparse matrix, also considerably accelerates the layout process. Furthermore, more sophisticated layouts than the basic force-directed method and more complex distance functions can be used to obtain a better reflection of the high-dimensional distances in the computed \(k\)-dimensional layout [Williams and Munzner 04].

A different approach is taken by FastMap [Faloutsos and Lin 95]: This simple, but effective, algorithm constructs a \(k\)-dimensional point set using the \(N \times N\) distance matrix \(M\) only. The main idea of FastMap is simple:

- 1. Choose the points \(p_i\) and \(p_j\) which maximize \(d_{ij}\).
- 2. Project all points \(p_l\) on the line \(\mathbf{v} = p_j - p_i\) to find one coordinate in the \(k\)-dimensional space.
- 3. Recursively apply FastMap on the projections of \(p_i\) on a plane orthogonal to \(\mathbf{v}\), to find the remaining \(k-1\) coordinates.

The key to FastMap is the observation that, to find the coordinate \(x_l\) of \(p_l\) along the line \(\mathbf{v}\), we only need to know the distances between the points \(p_i, p_j\), and \(p_l\) (Figure 11.31), using the well-known 'cosine law' theorem

\(x_l = \frac{d_{il}^2 + d_{ij}^2 - d_{lj}^2}{2d_{ij}}.\) (11.13)

FastMap is simple to implement and computationally efficient: For \(N K\)-dimensional points to be projected in \(k\) dimensions, its complexity is \(O(kN)\). However, compared to other more recent MDS methods mentioned at the end of this section, FastMap achieves a less well-minimized stress cost. For more details, we refer to the highly readable paper of Faloutsos and Lin [Faloutsos and Lin 95]. An implementation of FastMap is also readily available.

Besides force-directed layouts and FastMap, many other MDS algorithms exist. Spectral decomposition techniques project points along the eigenvectors having the largest eigenvalues of the distance matrix [Torgerson 65]. Efficient methods such as LLE [Roweis and Saul 00] and Isomap [Tenenbaum et al. 00, de Silva and Tenenbaum 03] have been devised, using numerical methods tailored to solve sparse eigenproblems. Isomap is an interesting extension of the conventional MDS techniques that aims to capture nonlinear relationships in the dataset. For this, Isomap replaces the input point-to-point distances by an approximation of the geodesic distance between points given by the shortest path on a graph created connecting neighbor points in the K-dimensional space with the original distance as weight. The k-dimensional coordinates are computed via conventional MDS methods, with calculations of eigenvalues over the distance relations of the previous step. Landmark MDS [de Silva and Tenenbaum 03] and Pivot MDS [Brandes and Pich 07] book further speed-ups by applying classical MDS to a small subset of representative points and projecting the remaining ones by local interpolation. MetricMap improves upon FastMap by attempting to perform the entire projection in one step [Wang et al. 99]. We refer the more mathematically inclined reader to the paper of Platt which shows how FastMap, MetricMap, and Landmark MDS can be unified in a single mathematical framework [Platt 05].

### 11.5.4 Projection-Based Dimensionality Reduction

As discussed in the introduction of dimensionality reduction methods, apart from using the point-wise distance matrix, we can use the original high-dimensional point coordinates (if available). Compared to MDS methods, the key difference is that we now assume that we know all K-dimensional coordinates p_i = (a_i^1, ..., a_i^K) of our points. We call the methods using this type of information projection-based dimensionality reduction methods.

One such method uses the so-called Karhunen-Loève transform [Fukunaga 90], which works as follows:

- 1. Compute the covariance matrix C of the N K-dimensional points p_i (for the definition thereof, see Section 8.3.2).
