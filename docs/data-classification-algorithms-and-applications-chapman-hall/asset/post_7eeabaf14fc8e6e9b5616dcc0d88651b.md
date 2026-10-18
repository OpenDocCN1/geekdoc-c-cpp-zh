
where ℒ_i = {j|l_i = l_j}) that is the set of points in the same class as point i.

The objective NCA maximizes is the expected number of points correctly classified under this scheme:

```
ℐ(W) = Σ_i p_i = Σ_i Σ_{j ∈ ℒ_i} p_ij   (18.25)
```

[7] proposed a truncated gradient descent approach to minimize ℐ(W). NCA is a local and linear approach. The learned distance between x_i and x_j is the Euclidean distance between Wᵀ x_i and Wᵀ x_j.

## 18.3.7 Average Neighborhood Margin Maximization (ANMM)

Average Neighborhood Margin Maximization (ANMM) [25] is another local supervised metric learning approach, which aims to find projection directions where the local class discriminability is maximized. To define local discriminability, [25] first defines the following two types of neighborhoods:

Definition 1(Homogeneous Neighborhoods). For a data point x_i, its ξ nearest homogeneous neighborhood N_i^o is the set of ξ most similar⁴ data, which are in the same class with x_i.

Definition 2(Heterogeneous Neighborhoods). For a data point x_i, its ζ nearest heterogeneous neighborhood N_i^e is the set of ζ most similar data, which are not in the same class with x_i.

Then the average neighborhood margin γ_i for x_i is defined as

```
γ_i = Σ_{k:x_k ∈ N_i^e} ||y_i - y_k||² / |N_i^e| - Σ_{j:x_j ∈ N_i^o} ||y_i - y_j||² / |N_i^o|
```

where |·| represents the cardinality of a set. This margin measures the difference between the average distance from x_i to the data points in its heterogeneous neighborhood and the average distance from it to the data points in its homogeneous neighborhood. The maximization of such a margin can push the data points whose labels are different from x_i away from x_i while pulling the data points having the same class label with x_i towards x_i.

Therefore, the total average neighborhood margin can be defined as

```
γ = Σ_i γ_i = Σ_i ( Σ_{k:x_k ∈ N_i^e} ||y_i - y_k||² / |N_i^e| - Σ_{j:x_j ∈ N_i^o} ||y_i - y_j||² / |N_i^o| )   (18.26)
```

and the ANMM criterion is to maximize γ. By replacing y_i = Wᵀ x_i, [25] obtains the optimal W by performing eigenvalue decomposition of some discriminability matrix. Thus ANMM is a local and linear approach. The learned distance between x_i and x_j is the Euclidean distance between Wᵀ x_i and Wᵀ x_j. The authors in [25] also proposed a kernelized version of ANMM to handle nonlinear data called KANMM, thus KANMM is a local and nonlinear approach.

## 18.3.8 Large Margin Nearest Neighbor Classifier (LMNN)

The last local supervised metric learning approach we want to introduce is the Large Margin Nearest Neighbor Classifier (LMNN) [26]. The goal of LMNN is similar to that of ANMM, i.e., to pull the data with the same labels closer while pushing data with different labels far apart. LMNN

deploys a different margin formulation. Specifically, LMNN defines the pull energy term as

$$\varepsilon_{pull}=\sum_{\mathbf{x}_j\in\mathcal{N}_i^\circ}\left\|\mathbf{W}^{\mathsf{T}}(\mathbf{x}_i-\mathbf{x}_j)\right\|^2$$  
(18.27)

which is the sum of pairwise distances between a data point $\mathbf{x}_i$ and the data point in $\mathbf{x}_i$’s homogeneous neighborhood after projection. LMNN defines the push energy as

$$\varepsilon_{push}=\sum_i\sum_{\mathbf{x}_j\in\mathcal{N}_i^\circ}\sum_l(1-\delta_{il})\left[1+\left\|\mathbf{W}^{\mathsf{T}}(\mathbf{x}_i-\mathbf{x}_j)\right\|^2-\left\|\mathbf{W}^{\mathsf{T}}(\mathbf{x}_i-\mathbf{x}_l)\right\|^2\right]_+$$  
(18.28)

where $\delta_{il}=1$ is the labels of $\mathbf{x}_i$ and $\mathbf{x}_l$ are the same, and $\delta_{il}=0$ otherwise. The intuition is to require that the data points from different classes should be at least separated from it by the distance 1. This formulation is very similar to the margin formulation in multiclass SVM [2]. LMNN also pushes the data with different labels to at least distance 1 from its homogeneous neighborhood. The goal of LMNN is to minimize

$$\varepsilon=\mu\varepsilon_{pull}+(1-\mu)\varepsilon_{push}.$$  
(18.29)

The authors in [26] proposed a semi-definite programming technique to solve for $\mathbf{M}=\mathbf{W}\mathbf{W}^{\mathsf{T}}$. Thus LMNN is a local and linear approach. The learned distance between $\mathbf{x}_i$ and $\mathbf{x}_j$ is the Euclidean distance between $\mathbf{W}^{\mathsf{T}}\mathbf{x}_i$ and $\mathbf{W}^{\mathsf{T}}\mathbf{x}_j$.

## 18.4 Advanced Topics

Although supervised metric learning has successfully been applied in many applications, it is human labor intensive and time consuming to get the supervision information. Also most of the above mentioned approaches require eigenvalue decomposition or quadratic optimization. In this section we will briefly review two advanced topics in metric learning: semi-supervised approaches and online learning.

### 18.4.1 Semi-Supervised Metric Learning

Semi-supervised approaches aim to learn a proper distance metric from the data where the supervision information is only available on a small portion of the data. Those algorithms utilize both data with and without supervision information in the learning process. Therefore one straightforward way one can think of to construct a semi-supervised algorithm is to deploy an objective in the form of $\lambda_1\mathcal{L}(\mathcal{D})+\lambda_2\mathcal{U}(\mathcal{D})$, where $\mathcal{U}(\mathcal{D})$ is constructed on the entire data, and $\mathcal{L}(\mathcal{D})$ is constructed on the data with supervision information only. Finally, we put some constraints on the learned distance metric to balance both parts.

#### 18.4.1.1 Laplacian Regularized Metric Learning (LRML)

*Laplacian Regularized Metric Learning (LMRL)* [9] is one semi-supervised distance metric learning approach. LRML adopts data smoothness term as the unsupervised term $\mathcal{U}(\mathcal{D})$; in terms of the supervised term, LRML chooses an ANMM type of objective as $\mathcal{L}(\mathcal{D})$. The optimization

problem that LRML aims to solve is
min_M  t + γ1 t2 - γ2 t3
s.t.   t1 ≤ t
       M ⪰ 0
(18.30)

where the smoothness term is
t1 = Σ_{i,j} ||W^T x_i - W^T x_j||^2 ω_ij = tr(W^T X L X^T W) = tr(X L X^T M)
(18.31)

where M = W W^T. The supervised terms consisting of compactness and scatterness are

t2 = Σ_{(x_i,x_j)∈M} ||W^T x_i - W^T x_j||^2 = tr[ M Σ_{(x_i,x_j)∈M} (x_i - x_j)(x_i - x_j)^T ]
(18.32)

t3 = Σ_{(x_i,x_j)∈C} ||W^T x_i - W^T x_j||^2 = tr[ M Σ_{(x_i,x_j)∈C} (x_i - x_j)(x_i - x_j)^T ]
(18.33)

where M and C are the sets of must-links and cannot-links, respectively.
[9] proposed a semi-definite programming approach for solving problem (18.30). LRML is a mixture of local (its unsupervised part) and global (its supervised part) approach, and it is linear. The learned distance is the Mahalanobis distance with precision matrix M.

#### 18.4.1.2 Constraint Margin Maximization (CMM)

Similarly, Constraint Margin Maximization (CMM) [22] selects the same supervised term as LRML, but a different PCA-type unsupervised term in its objective. Specifically, the optimization problem CMM aims to solve is
max_W  t4 - γ1 t2 - γ2 t3
s.t.   W^T W = I
(18.34)

where the unsupervised term is t4 = tr(W^T X Σ X^T W) is the PCA-like term. Note that before we apply CMM, all data points need to be centered, i.e., their mean should be subtracted from the data matrix. The intuition of CMM is to maximally unfold the data points in the projection space while at the same time satisfying those pairwise constraints. The authors in [22] showed that the optimal W can be obtained by eigenvalue decomposition to some matrix. Therefore CMM is a global and linear approach. Wang et. al. [22] also showed how to derive its kernelized version for handling nonlinear data. The learned distance between x_i and x_j is the Euclidean distance between W^T x_i and W^T x_j.

### 18.4.2 Online Learning

Most of the distance metric learning approaches involve expensive optimization procedures such as eigen-decomposition and semi-definite programming. One way to make those algorithms more efficient is the online learning [16] strategy, which incorporates the data points into the learning process in a sequential manner. More concretely, online learning updates the learned distance metric
