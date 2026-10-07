# Data Clustering: Algorithms and Applications

We can also show that the fixed point of the iteration in Equation (7.11) is in fact the KKT ((Karush-Kuhn-Tucker) condition in the theory of constrained optimization. We utilize the Lagrange multipliers $\Lambda \in \mathbb{R}^{K \times K}$ and minimize the Lagrangian function $L(F) = \|X - FG^T\|^2 + Tr[A(F^T - I)]$. The KKT complementarity condition for the nonnegativity of $F_{ik}$ gives

```
(-2ZG + 2FG^T + 2FA)_{ik} = 0. (7.13)
```

This is the fixed point that any local $F^*$ must satisfy. From Equation (7.13) we can obtain the Lagrange multiplier $\Lambda = G^TX^T - G^TG$. Now, we can easily check that the converged solution of the update Rule (7.11) also satisfies the fixed point relation Equation (7.13) with A substituted. This shows that the converged solution of the update Rule (7.11) is a local minimum of the optimization problem.

The convergence of Equation (7.11) is guaranteed by the monotonicity theorem which may be using the auxiliary function approach [67, 41].

**Theorem 5** *The Lagrangian L is nonincreasing (monotonically decreasing) under the update Rule (7.11).*

# 7.4.3 Practical Issues in NMF Algorithms

In the following we discuss several practical issues when applying NMF for clustering.

# 7.4.3.1 Initialization

Similar to K-means clustering, initialization also plays an important role when applying NMF for clustering since the objective function has many local minima [109, 53]. The intrinsic alternating minimization in NMF algorithms is nonconvex, even though the objective function is convex with respect to one set of variables.

A random initialization, where the factor matrices are initialized as random matrices, is generally not effective as it often leads to slow convergence to a local minimum. Many different techniques have been developed for improving the random initialization:

+   * Multiple initializations: The core idea is to perform multiple runs using different initializations and select the best estimates from multiple runs. This method needs to perform NMF multiple times and is computationally expensive.

+   * Factorization-based initialization: Note that NMF is a constrained low rank matrix factorization; hence, we use the results from low rank factorization methods as the initialization [10]. Typical examples include SVD-based initialization [10] and CUR decomposition-based initialization [66].

+   * Clustering-based initialization: If we think of NMF as a clustering process, then the initialization strategy based on the results from other clustering algorithms (e.g., spherical k-means [127, 41], divergence-based k-means [131], and fuzzy clustering [142]).

A comparison of different initialization methods can be found in [66]. Note that both factorization-based and clustering-based initialization methods are able to lead to rapid error reduction and faster convergence.

# 7.4.3.2 Stopping Criteria

Beyond a predefined number of iterations or a fixed running time, there are simple heuristics that be the stopping criteria for the iterative algorithms of NMF: (1) the objective function