# Algorithm 20.3 Manifold Regularization

Input : l labeled examples {(x_i, y_i)}_{i=1}^l, u unlabeled examples {x_j}_{j=l+1}^{l+u}. Output : Estimated function f^* : X → R.

+   1. Construct data adjacency graph with l + u nodes using, for example, k-nearest neighbors. Choose edge weights W_{ij}, for example, binary weights or heat kernel weights W_{ij} = e^{-||x_i - x_j||^2 / t}.
+   2. Choose kernel function K(x, y). Compute the Gram matrix K_{ij} = K(x_i, x_j).
+   3. Compute the Graph Laplacian matrix: L = D - W where D is a diagonal matrix given by D_{ii} = sum_{j=1}^{l+u} W_{ij}.
+   4. Choose γ_A and γ_I.
+   5. Compute α^* using Equation 20.8 for squared loss (Laplacian RLS) or using Equation 20.9 and 20.10 for hinge loss (Laplacian SVM).
+   6. Output f^*(x) = sum_{i=1}^{l+u} α_i^* K(x_i, x).

# 20.4.3 Theoretical Justification and Relevant Results

Even though various graph-based semi-supervised learning methods are quite popular and successful in practice, their theoretical justification is not quite well understood. Note that various semi-supervised learning algorithms involving graph Laplacian have a common structure as in equation 20.5, involving graph Laplacian (according to Equation 20.3). Although this formulation intuitively makes sense and these methods have enjoyed reasonable empirical success, Nadler et al. ([43]) pointed out that with a proper scaling of λ → 0, the solution of 20.4 degenerates to constants on unlabeled examples and “spikes” at labeled examples, in the limit, when for a fixed number of labeled examples the number of unlabeled examples increases to infinity. This shows that there is no generalization in the limit and the resulting solution is unstable in the finite labeled example case. Zhou et al. ([70]) resolve this problem by using higher order Sobolev semi-norm ||f||_m of order m such that 2m > d, where d is the intrinsic dimension of the submanifold. The Sobolev embedding theorem guarantees that this method gives continuous solutions of a certain order in the limit of infinite unlabeled examples while keeping the number of labeled examples fixed. Zhou et al. ([70]) clarify that the manifold regularization method ([8]), however, is guaranteed to provide continuous solutions due to a different formulation of the optimization problem.

In another direction, Zhang et al. ([63]) propose and study the theoretical properties of a transductive formulation of kernel learning on graphs, which is equivalent to supervised kernel learning and includes some of the previous graph-based semi-supervised learning methods as special cases. The general form of this formulation is

```
f̂ = arg min_{f ∈ R^{l+u}} (1/l) sum_{i=1}^l V(f_i, y_i) + λ f^T K^{-1} f   (20.11)
```

where V(·,·) is a convex loss function and K ∈ R^{(l+u)×(l+u)} is the kernel gram matrix whose (i,j)^{th} entry is the kernel function k(x_i, x_j). Some of the graph Laplacian-based algorithms fall under this category when K^{-1} is replaced by graph Laplacian L. Note that kernel gram matrix is always positive semi-definite but it may be singular. In that case the correct interpretation of f^T K^{-1} f is lim_{μ→0+} f^T (K + μ I_{(l+u)×(l+u)})^{-1} f where I_{(l+u)×(l+u)} is (l+u)×(l+u) identity matrix. Zhang et al. ([63]) show that the estimator f̂ in Equation 20.11 converges to its limit almost surely when the number of unlabeled examples u → 0. However, it is unclear what this particular limit estimator is and in case it is quite different from the true underlying function then the analysis may be uninformative. Zhang et al. ([63]) also study the generalization behavior of Equation 20.11 in the