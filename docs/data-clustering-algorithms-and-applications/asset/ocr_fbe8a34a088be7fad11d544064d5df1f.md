# Feature Selection for Clustering: A

$\Psi(P,t)$ for each $j$th dimension is given by $\sum_{i=1}^n f(t-T_i)^2$ and $\sum_{i=1}^n f(t-T_i) \cdot \chi(j)$, respectively, and $\Psi(t)$ is the sum of all the weights of the data points at time $t$, $\sum_{i=1}^n f(t-T_i)$.

Algorithm 9 systematically describes clustering using $k$-means to cluster the data $D_t$ using full dimension. Then, the least spread dimensions within each cluster are chosen to form the initial cluster structure. Then, using the selected features until convergence. After initialization, incoming data stream $X$ is temporarily added to each cluster with the corresponding selected features for cluster deformation of a new set of selected features. Final assignment of $X$ will be the closest cluster. After, the limiting radius of each cluster is calculated. Any data point that lies outside the limiting radii will form a cluster by itself. If the number of generated clusters exceeds the predetermined number of clusters $K$, the oldest cluster(s) are removed, so that the number of clusters equals $K$.

```
Algorithm 9 High-Dimensional Projected Stream Clustering (HPStream)
Input:
D: training data set
K: number of clusters
L: number of selected features
Output:
$\Omega$:
Initialize:
Perform clustering on $D_t$
$F = \{F_1, \dots, F_K\}$: sets of bit vectors
$\Omega$: fading cluster structure
1: while $X \leftarrow$ We have incoming stream do
2: for each cluster $C_i$
3: Add the new stream point $X$ into $C_i$
4: Update $\Omega(C_i,t)$
5: for each dimension $d$ do
6: Compute the radius of $\Omega(C_i,t)$
7: end for
8: Pick the dimensions in $\Omega(C_i,t)$ with minimum radii
9: Create selected features $F_i$ for $C_i$
10: end for
11: for each cluster $C_i$
12: for each selected feature $F_j$
13: $dis_j \leftarrow$ Distance between $X$ and the center of $C_i$
14: end for
15: $index = argmin\{dis_j\}$$
16: $s \leftarrow$ The radius of $C_{index}$
17: if $index > s$ then
18: Add new cluster $C_{K+1}$
19: else
20: Add $X$ to $C_{index}$
21: end if
22: Remove clusters with zero dimensions from $\Omega$
23: if Number of current clusters $> K$ then
24: Delete the least recently added cluster from $\Omega$
25: end if
26: end for
27: end while
```