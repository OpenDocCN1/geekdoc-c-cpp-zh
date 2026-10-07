# 21.3.5 Information Theoretic

Another approach to the generation of alternative clusterings is based on the objective functions using information theoretic principles. Such approaches are mathematically attractive and incorporate the use of mutual (or similar) information to measure the strength of correlations between clustering. Several algorithms fall into this category, beginning with the approach of Gonde and Hofmann [16], which was the first (to our knowledge) alternative clustering algorithm to be proposed.

# 21.3.5.1 Conditional Information Bottleneck (CIB)

The conditional bottleneck (CIB) for alternative clustering is described in [15, 16]. This algorithm takes as input an existing clustering $C_1$ as background knowledge and sequentially generates a single alternative clustering $C_2$ by optimizing the objective function

```
$$\max(I(C_2;C_1) - \lambda_1 I(C_2;X) + \lambda_2 I(C_2;F))$
```

Where $F$ is the features, $X$ is the features, and the existing clustering $C_1$. The term $I(C_2;C_1)$ corresponds to the mutual information between the new clustering being discovered and the features, the predefined clustering. The term $I(C_2;X)$ corresponds to the mutual information we desire to be small, avoiding being overly confident about the groupings), and $I(C_2;F)$ corresponds to the mutual information between the alternative clustering and the features (which we wish to be). The symbols $\lambda_1 > 0$ and $\lambda_2 > 0$ are regularization parameters, to trade off the different components of the objective function. The approach of [16] describes an alternating optimization scheme with deterministic annealing, which can be used for generating $C_2$ with this objective function. In practice, this style of approach has been found to behave particularly strongly for document datasets.

# 21.3.5.2 Conditional Ensemble Clustering

The CIB approach of [15, 16] was further extended in [14], which introduced the CondEns (Conditional Ensemble) alternative clustering algorithm.

CondEns operates in three stages. (1) Given the clustering $C_1 = \{c_1, \dots, c_k\}$ as background knowledge, for each cluster $c_i$ a local clustering is generated using any clustering algorithm. It yields $k$ local clusterings. (2) Each of the $k$ local clusterings is extended into a global clustering, by assigning instances not part of a local clustering, to one of its clusters. (3) The $k$ global clusterings are then combined using a combination technique based on the conditional bottleneck, to yield a single alternative clustering.

With the approach of [16], CondEns also performs well for text datasets. A limitation of CondEns is its guarantees about the dissimilarity of the alternative clustering are somewhat unclear, since the clusters in the original clustering $c_1$ may be quite similar among themselves. This means the alternative clustering may turn in similar to the background clustering.

# 21.3.5.3 NACI

The NACI algorithm was proposed by Dang and Bailey in [9] and targets scenarios where the borders between clusters in the alternative clustering may not be linearly separable.

At a high level, its objective function can be expressed as an alternative clustering $C_2$, given a clustering $C_1$ as background knowledge, according to

```
$$C_2 = \text{argmax}\{I(C_2;X) - \eta I(C_1;C_2)\}$
```

where