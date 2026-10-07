classifier weights $w \in \mathbb{R}^{D 	imes Q}$ need to be determined. $P_{qk} = 1$ if label $k$ appears in child $q$ and $P_{ql} = 0$ otherwise. To measure the accuracy, the loss function is defined as follows:

```
$L(w,x,y,P) = 1 - P(\hat{q},y)$ (14.11)
```

implies that label clustering should keep a higher classification accuracy. In the meantime, the partition for each label set within the cluster will also contribute to the overall efficiency measure which is formulated as follows:

```
$A(w,x,P) = \frac{1}{K} \sum_{k=1}^{K} P(\hat{q},k)$ (14.12)
```

Therefore, the joint balance of efficiency and accuracy trade-off for label sets and enhancing the classification performance leads to the following optimization problem:

```
$\min_{w,P} \frac{1}{m} \sum_{i=1}^{m} A(w,x_i,P)$ (14.13)\ns.t. \quad \frac{1}{m} \sum_{i=1}^{m} L(w,x_i,y_i,P) \le \varepsilon$ (14.14)\n$\varepsilon \ge 0$ (14.15)\n$P \in \{0,1\}^{O \times K}$ (14.16)
```

However, directly optimizing the optimization problem is difficult. With proper relaxation, alternatively optimizing over $w$ and $P$ can be formulated as a convex programming problem:

```
$\hat{L}(w,x,y,P) = \max {0, 1 + \max_{q \in A_i \cup B_i} w_q^T x_i - w_q^T y_i}$ (14.17)
```

Here, $A_i$ is the set of children that contains label $x_i$, and $B_i$ is the rest of the children. Therefore, optimizing with a fixed $P$ can be done as follows:

```
$\min_{P} A(P) = \sum_{q,k} \frac{P_{qk}}{mK} \sum_{i=1}^{m} I(\hat{q}_i = q)$ (14.19)\ns.t. \quad 1 - \sum_{q,k} \frac{P_{qk}}{mK} \sum_{i=1}^{m} I(\hat{q}_i = q \wedge y_i = y_k) \le \varepsilon$ (14.20)\n$\varepsilon \ge 0$ (14.21)\n$P_{qk} \in \{0,1\ \forall q,k$ (14.22)
```

Furthermore, if we fix $w$ and optimize $P$, the terms can be rearranged as follows:

In such a way, clustering for each label set and the associated classifier are iteratively learned, yielding a local optimal solution.

# 14.3 Clustering with Video and Audio Data

In the previous section, we have discussed several examples of clustering algorithms with image data. It is known that videos consist of image sequences. However, clustering algorithms with video data