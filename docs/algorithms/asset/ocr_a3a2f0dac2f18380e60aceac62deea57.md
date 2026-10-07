# 9.2 Approximation algorithms

# Figure 9.5 Some data points and the optimal $k = 4$ clusters.

![](bbox=[0.215, 0.118, 0.53, 0.276])

+   2. $d(x, y) = 0$ if and only if $x = y$.
3. $d(x, y) = d(y, x)$.
4. (Triangle inequality) $d(x, y) \leq d(x, z) + d(z, y)$.

We would like to partition the data points into groups that are compact in the sense of having small diameter.

# k-Cluster

**Input:** Points $X = \{x_1, \dots, x_n\}$ with underlying distance metric $d(\cdot, \cdot)$; integer $k$.
**Output:** A partition of the points into $k$ clusters $C_1, \dots, C_k$.
**Goal:** Minimize the diameter of the clusters,

> $\max_{x_i, x_j \in C} d(x_i, x_j)$

One way to visualize this is to imagine $n$ points in space, which are to be covered by $k$ spheres of equal size. What is the smallest possible diameter of the spheres? Figure 9.5 shows an example.

This problem is NP-hard, but a very simple approximation algorithm. The algorithm is to pick $k$ points of the data as *centers* and to assign each of the remaining points to the center closest to it, creating $k$ clusters. The centers are picked one at a time, using an intuitive rule: pick the next center to be as far as possible from the centers so far (see Figure 9.6).

```
Pick any point $\mu_1 \in X$ as the first cluster center
for $i=2$ to $k$:
  Let $\mu_i$ be the point in $X$ farthest from $\mu_1, \dots, \mu_{i-1}$
  (i.e., that maximizes $\min_{j<i} d(\cdot, \mu_j))
Create $k$ clusters: $C_i = (all \ x \in X \ whose \ closest \ center \ is \ \mu_i)$
```

It's clear that this algorithm returns a valid partition. What, the resulting diameter is guaranteed to be most optimal.