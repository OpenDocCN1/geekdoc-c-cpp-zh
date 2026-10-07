# Semisupervised Clustering

The conditional distribution $P(X|Y,\Theta) = \prod p(x_i|y_i,\Theta)$ is determined by a mixture model, where the mixture component is determined by $y_i$, and $\Theta$ contains the parameters of the mixture model. The literature has a variety of components, including von M-Fischer, and multinomial [4]. More generally, one can consider a functional form of the conditional distribution distribution $p(x|y,\Theta) = \exp(-d_\Theta(x,\mu_y))$, where $Z_\Theta$ is the partition function. The negative-likelihood of the posterior, is given by

```
-log P(Y,\Theta,C) = \sum_{i} d_Theta(x_i,\mu_{y_i}) + \sum_{j} f(i,j) - \log P(\Theta) + n\log Z_\Theta + n\log P(C). (20.11)
```

Since log $P(C)$ is constant, $R(\Theta) = n\log Z_\Theta - \log P(C)$, Equation 20.11 is equivalent to the objective function in Equation 20.

Given a dataset, some clusters can be learned using a version of the EM algorithm. In particular, for the objective function in 20.11, one has the parameters $\Theta = (M,A)$ and the cluster members $Y = \{y_1, ..., y_n\}$ for every data. The EM algorithm is initialized with some value $\Theta^{(0)}$ for the parameters and then proceeds with the following updates until convergence:

+   **E-step** Update $\Theta = (M',A)$, update clusters $Y^{j+1}$ to minimize the objective

+   **M-step** Update $(A', Y^{j+1})$, update cluster means $M^{j+1}$ to minimize the objective

+   **A-step** Update $(M^{j+1}, Y^{j+1})$, update distortion parameter $A^{j+1}$ to minimize the objective

For a variety of semisupervised clustering, the above SSC approach has been shown to perform well and has, evolved, as one of the standards SSC to SSC with pairwise constraints [5, 4, 6].

# 20.2.3 Active Learning for Semisupervised Clustering

Since SSC works with a few (pointwise) labels, active learning is a natural framework to work in this setting. Given a fixed number of queries on pairwise labels, the goal is to decide which queries in order to get must-link and cannot-link information. In [3], a two-stage method is outlined for active learning for SSC with pairwise labels. In the first stage, called *explore*, the focus is on getting one point from each cluster with a small number of queries. The first point is chosen at random and assigned to a cluster. Subsequent points are chosen by farthest traversal, i.e., by picking the point which is farthest from all existing points, distance to a set is measured by the distance to the nearest point in the existing clusters. Once a set is obtained, pairwise queries are made with any point from each of the existing clusters. If a must-link constraint is found with any of the existing clusters, the point is assigned to that cluster, and if no must-link constraint is found with any of the existing clusters, a new cluster is initialized with this point as the member. The explore explore process continues until at least one point from each cluster is found or the budget of queries is exhausted. In the second stage, called *consolidate*, additional data points are selected and assigned to the correct clusters by pairwise querying. Given a data point, all clusters are first sorted in order of distance to the corresponding clusters. Pairwise queries are made with any point from each of the clusters in sorted order until a point/cluster with a must-link constraint is found. In that case, the new point is assigned to that cluster, and the process continues by another point at random. The querying is expected to be efficient, i.e., for a $k$-clustering problem, much fewer than $k$ queries will usually be needed. Empirically, [3] show the active learning strategy is shown effective in practice, leading to better-test performance with fewer queries as compared to the queries at random.

![](bbox=[0.433, 0.523, 0.566, 0.553])