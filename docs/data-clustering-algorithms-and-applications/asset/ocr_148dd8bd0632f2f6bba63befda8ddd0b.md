# Data Clustering: Algorithms and Applications

Since $f_i = y_i$ due to the constraints,$2$ the above system can be simplified to get a closed form for $f_u$ given by

```
$f_u = (D_{uu} - W_{uu})^{-1}W_{ul}y_l .$
```

We can interpret the objective function in GF as a special case of the GLP problem in (20,38). In particular, using the identity in Equation 20.22 and noting that the constraints on the labeled points are binding, GF can be seen as a special case of GLP with $L=L_u$ and $\varepsilon=0$, i.e.,

```
$\min_{f_u \in \mathbb{R}^u} f_u^T L_u f_u, \text{s.t.} } \sum_{i=1} (f_i - y_i)^2 \le 0 .$
```

# 20.43 Tikhonov Regularization (TIKREG)

Given a partially labeled data set, TIKREG [7] is an algorithm for regularized regression on graphs, where the objective is to infer a function $f$ over graphs. The objective for TIKREG is given by

```
$\min_{f \in \mathbb{R}^n} \sum_{i,j=1}^n w_{ij}(f_i - f_j)^2 + \frac{1}{\gamma} \sum_{i=1}^n (f_i - y_i)^2$
```

with the constraint that $\dot{f} \perp \mathbf{1}$, i.e., for in the orthogonal subspace of $\mathbf{1}$, all ones vector. The parameter $\gamma$ is chosen (positive) real. A closed form for the problem problem is obtained [7]

```
$f = (\gamma L_u + I_k)^{-1}(\gamma y_l).$
```

where $\hat{y} = (y_1, y_2, ..., y_k, 0, ..., 0)$, $I_k = diag(1, ..., 1, 0, ..., 0)$ with the number of ones equal to the labeled points. The constraint on $f$ is enforced by the Lagrange multiplier $\mu$, which is computed as

```
$\mu = \frac{\mathbf{1}^T(\gamma L_u + I_k)^{-1}\gamma y_l}{\mathbf{1}^T(\gamma L_u + I_k)^{-1}\mathbf{1}}$
```

The objective in Equation 20.42 can be viewed as a special case of the GLP objective in (20,38). As previously, the first term is $f_u^T L_u f_u$, where $L_u$ is the unnormalized Laplacian. The second term corresponds to the constraint $\sum_{i}(f_i - y_i)^2 \le \varepsilon$, in (20,38) where $1/\gamma$ is the optimal Lagrange multiplier corresponding to the constraint. In other words, if $\varepsilon(1/\gamma)$ is the constraint value that leads to the optimal Lagrange multiplier $1/\gamma$, the TIKREG problem can be seen as a special case of GLP:

```
$\min_{f_u \in \mathbb{R}^u} f_u^T L_u f_u, \text{s.t.} } \sum_{i=1} (f_i - y_i)^2 \le \varepsilon(1/\gamma).$
```

# 20.44 Local and Global Consistency

The Local Global Consistency (LGC) approach [45] gives an graph-based regularization framework for semisvised learning. In particular, the LGC is formulated based on the following objective:

```
$\min_{f \in \mathbb{R}^n} \frac{1}{2} (\sum_{i,j=1}^n w_{ij}(\frac{f_i}{\sqrt{D_{ii}}} - \frac{f_j}{\sqrt{D_{jj}}})^2 + \mu \sum_{i=1}^n (f_i - y_i)^2)$
```

> 2We use notation and denote $[f_1, ..., f_l]^T$ by $f_l$ similarly for $[f_{(1)}, ..., f_{(u)}]^T$ by $f_u$ in the sequel.