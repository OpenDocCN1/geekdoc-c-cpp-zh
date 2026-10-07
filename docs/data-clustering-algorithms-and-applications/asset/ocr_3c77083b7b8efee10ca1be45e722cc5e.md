# Alternative Clustering Analysis: A Review

tinction between two clusterings) is minimized. The objective function of CAMI is when

```
$L(\\Theta, D) = L(\\Theta^1; D) + L(\\Theta^2; D) - \eta \sum_{i,j} p(C_i, C_j) \log \frac{p(C_i, C_j)}{p(C_i)p(C_j)}$
```

The first two terms correspond to the likelihood of each of the two clusterings will be simultaneously discovered and $\Theta^1$ and $\Theta^2$ are their parameters. The third term corresponds to the dissimilarity between the clusterings $C_1$ and $C_2$ as measured by mutual information. The $\eta$ is a regularization parameter used to trade off similarity and quality (which can be specified by the user). Using Gaussian mixture models, an EM approach can be used to optimize the objective function.

# 21.3.3 Guided Generation with Constraints

The next class of techniques uses constraints to guide the generation of one or more alternative clusterings. The type of constraints and the way they are used distinguishes each of the methods.

# 21.3.3.1 COALA

COALA method takes into account a similarity matrix and a single clustering as background knowledge. Using the existing clustering, a set of "cannot-link" constraints is generated, for each pair of objects in the same cluster. Intuitively, it is less desirable for these pairs to be together in the same cluster of the alternative. A hierarchical clustering algorithm is used. At each iteration, COALA finds two pairs of clusters for a possible merge, denoted as $(q_1, q_2)$, called a qualitative pair, and $(o_1, o_2)$, called a dissimilar pair. The qualitative pair is the one with the minimum distance over all the pairs of clusters. The dissimilar pair has the minimum distance over all the pairs of clusters that also satisfy the cannot-link constraints. Given a tradeoff parameter $\omega$, if $d(q_1, q_2) \geq \omega$, then the pair $(o_1, o_2)$ is merged. Otherwise, the pair $(q_1, q_2)$ is merged. By varying the value of $\omega$, different behaviors can be achieved.

COALA is a simple technique and has been used as a baseline method for comparison in range of papers. A limitation of COALA is that it is specifically tied to a hierarchical clustering algorithm. It was not formulated for the case of generating multiple alternative clusterings. However, it is easy to make generalizations where multiple clusterings are used as background knowledge, yielding a larger set of cannot-link constraints for generating the alternative clustering.

# 21.3.3.2 Constrained Optimization Approach

The approach of Qi and Davidson in [32] uses constraints in a different way. It takes the original dataset $X = \{x_1, \dots, x_n\}$ and transforms it into a new dataset $Y = \{y_1, \dots, y_n\}$, where $Y = DX$ and $D$ is a transformation matrix representing a distance metric. Any clustering algorithm can then be used to generate the new dataset as an alternative to the original clustering as a constrained optimization task

The objective function is

```
$min_{B \geq 0} D_{KL}(p(y_i) || p(x_i)) = \sum_{i=1}^n \sum_{j=1, x_i \in C_j} ||x_i - \mu_j||_B^2 \leq \beta$
```

where $B = D^T D, ||\cdot||_B$ is the Mahalanobis distance using matrix $B$, and $B \geq 0$ signifies that $B$ is required to be positive semidefinite.