where φ: R^N → R^{d_h} is the mapping to a high-dimensional feature space of dimension d_h; b_l are the bias terms; and l = 1, ..., maxk − 1. However, for large-scale networks, we can utilize the explicit expression of the underlying feature map and d_h = N. Since the KSC formulation is valid for any positive definite kernel, we use a normalized linear kernel function to avoid any kernel parameter. The projections e_i^{(l)} represent the latent variables of a set of maxk − 1 binary cluster indicators given by sign(e_i^{(l)}), which can be combined with the final groups using an encoding/decoding scheme. The dual problem corresponding to this primal formulation is

D^{-1} M_D α^{(l)} = λ_l α^{(l)} (9.5)

where M_D = I_{N_r} − (1/N_r 1_{N_r} 1_{N_r}^T D^{-1}) / (1_{N_r}^T D^{-1} 1_{N_r}). The α^{(l)} are the dual variables, and the kernel function K: R^N × R^N → R plays the role of similarity function.

# 9.2.3.2 Model Selection

KSC-net provides the user with the option to select one of the two model selection techniques, that is, the BAF criterion [1] or the self-tuned procedure [3].

# Algorithm 1: BAF Model Selection Criterion

Data: Given codebook Cβ, maxk, and P = e_valid1,..., e_valid_Nv.
Result: Maximum BAF value and optimal k.

+   1. foreach k ∈ {2, maxk} do
+   2. Calculate the cluster memberships of training nodes using codebook Cβ.
+   3. Get the clustering Δ = {C1,...,Ck} and calculate cluster mean u_j for each C_j.
+   4. For each validation node valid_d, obtain max_j cos(θ_{j,valid_d}), where cos(θ_{j,valid_d}) = ||e_valid_d|| / ||e_valid_d||, j = 1,...,k.
+   5. Maintain dictionary MaxSim(valid_i) = max_j cos(θ_{j,valid_i}), j = 1,...,k.
+   6. Obtain clustering Δ_valid = {C_valid1,...,C_validk} for the validation nodes.
+   7. Define BAF as BAF(k) = Σ_{i=1}^k Σ_{valid_i ∈ C_i} 1/k * MaxSim(valid_i) / |C_i|.
+   8. end
+   9. Save the maximum BAF value along with the corresponding k.

# 9.2.3.3 Out-of-Sample Extension

Ideally, when the communities are nonoverlapping, we will obtain k well-separated communities, and the normalized Laplacian has k piecewise constant eigenvectors. This is because the multiplicity of the largest eigenvalue, that is, 1, is k as depicted in Reference 23.