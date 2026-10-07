# Semisupervised Clustering

two clustering objectives in Equation 20.1 and Equation 20.2. The combined objective is given by

```
$J_{PCCC}(M,Y,\mathcal{A}) = \sum_{\mathbf{x}_i \in \mathcal{X}} \{(\mathbf{x}_i - oldsymbol{\mu}_{y_i})^T A_{y_i}(\mathbf{x}_i - oldsymbol{\mu}_{y_i}) + \log(\det(A_{y_i}))\}\n + \sum_{\mathbf{x}_i,\mathbf{x}_j \in M} w_{ij}f_m(\mathbf{x}_i,\mathbf{x}_j)[y_i \neq y_j] + \sum w_{ij}f_c(\mathbf{x}_i,\mathbf{x}_j)[y_i = y_j] \; $
```

where $fm$ and $fc$ are the constraint functions defined on $(\mathbf{x}_i, \mathbf{x}_j)$. The function $fm$ is defined such that the penalty for violation of must-link constraints between points that are distant should be higher. Such a constraint makes sense since two distant points need to be must-linked, then the metric used must-link needs a major update, and a high penalty will be to accomplish that a violated must-link involves two clusters, the penalty is defined in terms of both:

```
$f_M(\mathbf{x}_i,\mathbf{x}_j) = \frac{1}{2}(\mathbf{x}_i - oldsymbol{\mu}_{y_i})^T A_{y_i}(\mathbf{x}_i - oldsymbol{\mu}_{y_i}) + \frac{1}{2}(\mathbf{x}_j - oldsymbol{\mu}_{y_j})^T A_{y_j}(\mathbf{x}_j - oldsymbol{\mu}_{y_j}) . $
```

In the case of cannot-link violations, the penalty for nearby points should be higher. The following penalty term is considered:

```
$f_C(\mathbf{x}_i,\mathbf{x}_j) = \frac{1}{2}(\mathbf{x}_i - oldsymbol{\mu}_{y_i})^T A_{y_i}(\mathbf{x}_i - oldsymbol{\mu}_{y_i}) - \frac{1}{2}(\mathbf{x}_j - oldsymbol{\mu}_{y_j})^T A_{y_j}(\mathbf{x}_j - oldsymbol{\mu}_{y_j}) . $
```

where $(\mathbf{x}_i, \mathbf{x}_j)$ are the maximally separated sets of points in the data according to $A_l$. These weight functions are introduced in order to produce more relevant to the constraints. The objective function is optimized by the EM algorithm, which alternates between updating the cluster assignments, and updating the cluster means $\mu_0$ and $A_0$ until convergence. For scalability and stability, [9] suggests using metrics with simpler structures, such as diagonal matrices, for high-dimensional problems.

Global Metric Learning: A generalization of the PCMeans setting was considered in the literature [9, 5, 4], where the distance metric to measure the within-cluster distortion is global and parameters are learned as part of the SSC. In particular, if A is a positive definite matrix, one considers the following:

```
$J_{GL}(M,Y,\mathcal{A}) = \frac{1}{2}\sum_{\mathbf{x}_i \in \mathcal{X}} (\mathbf{x}_i - \boldsymbol{\mu}_{y_i})^T A_{y_i}(\mathbf{x}_i - \boldsymbol{\mu}_{y_i}) + \sum_{\mathbf{x}_i,\mathbf{x}_j \in M} w_{ij}[y_i \neq y_j] + \sum_{\mathbf{x}_i,\mathbf{x}_j \in \mathcal{X}} w_{ij}[y_i = y_j] . $
```

Although the above focuses on the K-means clustering, the formulation can be generalized to several other settings such as information theoretic and spherical clustering. The two main choices in each setting are (i) a parameterized distance $d_l(\mathbf{x}_i,oldsymbol{\mu}_{y_i})$, which measures the divergence of each data point from its corresponding cluster mean, and (ii) suitable penalty functions $f_L(i,j)$ and $f_C(i,j)$, which measure the cost of violating a must-link and a cannot-link constraint. In Equation 20.6, we have $d_l(\mathbf{x}_i,oldsymbol{\mu}_{y_i}) = $(\mathbf{x}_i - oldsymbol{\mu}_{y_i})^T A_{y_i}(\mathbf{x}_i - oldsymbol{\mu}_{y_i})$, and $f_L(i,j) = 1$, and $f_C(i,j) = 1$.

Parameterized divergence functions: One can consider more general divergence functions, including parameterized and directional divergences. In particular, information theoretic clusters use the following divergence function [22, 4]: $d_l(\mathbf{x}_i,\boldsymbol{\mu}_{y_i}) = \sum_{k=1}^d x_{ik} \log \frac{x_{ik}}{\mu_{y_i,k}}$, where $\mu_{y_i,k}$ are assumed to be positive or probability distributions. In the latter case, the divergence converges to the KL-divergence [19]. The parameterized version of I-divergence uses a diagonal matrix $A = diag(a_j)$ with nonnegative weight $a_j$ corresponding to each dimension $j$ to $d_{L,A}(\mathbf{x}_i,\boldsymbol{\mu}_{y_i}) = \sum_{j=1}^d a_{ij} x_{ij} \log \frac{x_{ij}}{\mu_{y_i,j}} - \sum_{j=1}^d a_{ij}(x_{ij} - \mu_{y_i,j})$. One can similarly define a parameterized version of directional divergence based on the cosine similarity $d_A(\mathbf{x}_i,\boldsymbol{\mu}_{y_i}) = 1 - \frac{\mathbf{x}_i^Toldsymbol{\mu}_{y_i}}{\|\mathbf{x}_i\|\\boldsymbol{\mu}_{y_i}\|}$, where $\|\mathbf{x}_i\| = \sqrt{\mathbf{x}_i^T\mathbf{x}_i}$.

© 2014 by Taylor & Francis Group, LLC