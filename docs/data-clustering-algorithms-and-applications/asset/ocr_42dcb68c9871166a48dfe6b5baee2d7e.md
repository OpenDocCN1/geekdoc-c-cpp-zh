# Data Clustering: Algorithms and Applications

While parameterized divergences give the additional flexibility of rotating/or scaling the feature space appropriately in order to match the given pairwise semisension, without proper regularization, such formulations can yield degenerate solutions. For example, setting A=0, the zero matrix makes all distances zero, and minimizes the objective function, but is not meaningful. To avoid such degenerate solutions, one considers regularizers R(A) on A or putting constraints on A, e.g., making A positive semidefinite, which is commonly in metric learning [41].

**Constraint violation functions:** The second choice involves the constraint violation functions $f_{ML}(i,j)$ and $f_{CL}(i,j)$. For the must-link constraints, one considers penalty functions proportional to the distance, $f_{ML}(i,j)=d_A(X_i,X_j)$. For points which are far according to the distance function, a must-link constraint provides valuable information regarding the structure of the clusters. As a result, the penalty increases if a constraint is violated. i.e., $f_{CL}(i,j)=d_{ij}^{max}-d_A(X_i,X_j)$, where $d_{ij}^{max}$ is a upper bound on the pairwise distances between points in the dataset. Thus, non-link constraints between points which are nearly given more weight as they suggest that the cluster may be substantially different from the one suggested by the distance measure. One can consider alternative of the functions as appropriate for the given partition domain.

With the two generators, the objective function for PCC can be written as

```
$J_{PCC}(M,Y,A) = \frac{1}{2}\sum_{i\neq j} d_A(X_i,X_j) + R(A) \n + \sum_{(i,j) \in M} w_{ML}f_{ML}(i,j)\mathbb{I}(Y_i \neq Y_j) + \sum_{(i,j) \in C} w_{CL}f_{CL}(i,j)\mathbb{I}(Y_i \neq Y_j).$
```

Such a formulation can be interpreted as the log-likelihood of a probabilistic graphical model known as the Markov random field (MRF). The HMR model consists of the following sets of variables and parameters: (i) an observable set $X=(X_1,\dots,X_n)$ corresponding to the given data points $X$; (ii) an unobservable (hidden) set $Y=(Y_1,\dots,Y_n)$ corresponding to cluster assignments of points, where each hidden variable $Y_i$ encodes the label of point $i$, and takes values from the set of cluster indices $(1,\dots,K)$; (iii) a set of model parameters $\Theta=\{A,M\}$, which consists of divergence parameters $A$ and cluster representations $M=(\mu_1,\dots,\mu_k)$; and (iv) an observable set of constraint variables $C=\{c_{12},c_{13},\dots,c_{n-1,n}\}$, where each $c_{ij}$ is a binary variable taking a value from the set $(-1,0)$, where $c_{ij}=1$ indicates that $(X_i,X_j) \in M$, is the set of must-link constraints, and $c_{ij}=-1$ indicates that $(X_i,X_j) \in C$, the set of non-link constraints.

Consider the posterior distribution $P(Y|\Theta,C)$, which by Bayes rule is proportional to

```
$P(X,Y|\Theta,C) = P(X|Y,\Theta,C)P(Y|\Theta,C).
```

We assume the model parameters $\Theta=(M,A)$ to be independent of the constraints $C$, so that $P(\Theta|C)=P(\Theta)=P(M,A)=P(M)P(A)$, where we assume $M$ and $A$ to be independent.

The latent variables $Y$ are assumed to form a pairwise Markov random field (MRF) with only pair-wise potentials [39,40], so that

```
$P(Y|\Theta
```

where $Z$ is the partition function, and the pairwise potentials are given by

```
$f(i,j) = \begin{cases} w_{ij}f_{ML}(i,j) , & c_{ij}=1\text{ and } y_i \neq y_j \ w_{ij}f_{CL}(i,j) , & c_{ij}=-1\text{ and } y_i = y_j \ 0 , & \text{otherwise}. \end{cases}$
```