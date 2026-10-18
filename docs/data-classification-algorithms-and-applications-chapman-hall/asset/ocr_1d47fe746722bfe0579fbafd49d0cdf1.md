where ℒ_i = {j|l_i = l_j}) that is the set of points in the same class as point i.

The objective NCA maximizes is the expected number of points correctly classified under this scheme:

```
ℐ(W) = Σ_i p_i = Σ_i Σ_{j ∈ ℒ_i} p_ij   (18.25)
```

[7] proposed a truncated gradient descent approach to minimize ℐ(W). NCA is a local and linear approach. The learned distance between x_i and x_j is the Euclidean distance between Wᵀ x_i and Wᵀ x_j.

# 18.3.7 Average Neighborhood Margin Maximization (ANMM)

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

# 18.3.8 Large Margin Nearest Neighbor Classifier (LMNN)

The last local supervised metric learning approach we want to introduce is the Large Margin Nearest Neighbor Classifier (LMNN) [26]. The goal of LMNN is similar to that of ANMM, i.e., to pull the data with the same labels closer while pushing data with different labels far apart. LMNN