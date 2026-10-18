Equation (2.27) assumes that the feature graph is unsigned, and encourages positive correlation between the values of coefficients for the features connected by an edge in the unsigned graph. However, two features might be negatively correlated. In this situation, the feature graph is signed, with both positive and negative edges. To perform feature selection with a signed feature graph, GFlasso employs a different ℓ₁ regularization over a graph [32],

penalty(w, G) = λ‖w‖₁ + (1 − λ) Σ_{i,j} A_{ij} ‖w_i − sign(r_{ij}) w_j‖,    (2.28)

where r_{ij} is the correlation between two features. When f_i and f_j are positively connected, r_{ij} > 0, i.e., with a positive edge, penalty(w, G) forces the coefficients w_i and w_j to be similar; while f_i and f_j are negatively connected, r_{ij} < 0, i.e., with a negative edge, the penalty forces w_i and w_j to be dissimilar. Due to possible graph misspecification, GFlasso may introduce additional estimation bias in the learning process. For example, additional bias may occur when the sign of the edge between f_i and f_j is inaccurately estimated.

In [72], the authors introduced several alternative formulations for graph Lasso. One of the formulations is defined as

penalty(w, G) = λ‖w‖₁ + (1 − λ) Σ_{i,j} A_{ij} max(|w_i|, |w_j|),    (2.29)

where a pairwise ℓ_∞ regularization is used to force the coefficients to be equal and the grouping constraints are only put on connected nodes with A_{ij} = 1. The ℓ₁-norm of w encourages sparseness, and max(|w_i|, |w_j|) will penalize the larger coefficients, which can be decomposed as

max(|w_i|, |w_j|) = ½(|w_i + w_j| + |w_i − w_j|),    (2.30)

which can be further represented as

max(|w_i|, |w_j|) = |uᵀ w| + |vᵀ w|,    (2.31)

where u and v are two vectors with only two non-zero entities, i.e., u_i = u_j = ½ and v_i = −v_j = ½.

The GOSCAR formulation is closely related to OSCAR in [4]. However, OSCAR assumes that all features form a complete graph, which means that the feature graph is complete. OSCAR works for A whose entities are all 1, while GOSCAR can work with an arbitrary undirected graph where A is any symmetric matrix. In this sense, GOSCAR is more general. Meanwhile, the formulation for GOSCAR is much more challenging to solve than that of OSCAR.

The limitation of the Laplacian Lasso — that the different signs of coefficients can introduce additional penalty — can be overcome by the grouping penalty of GOSCAR. However, GOSCAR can easily overpenalize the coefficient w_i or w_j due to the property of the max operator. The additional penalty would result in biased estimation, especially for large coefficients. As mentioned above, GFlasso will introduce estimation bias when the sign between w_i and w_j is wrongly estimated. This motivates the following non-convex formulation for graph features,

penalty(w, G) = λ‖w‖₁ + (1 − λ) Σ_{i,j} A_{ij} ‖|w_i| − |w_j|‖,    (2.32)

where the grouping penalty Σ_{i,j} A_{ij} ‖|w_i| − |w_j|‖ controls only magnitudes of differences of coefficients while ignoring their signs over the graph. Via the ℓ₁ regularization and grouping penalty, feature grouping and selection are performed simultaneously where only large coefficients as well as pairwise difference are shrunk [72].

For features with graph structure, a subset of highly connected features in the graph is likely to be selected or not selected as a whole. For example, in Figure 2.8, {f₅, f₆, f₇} are selected, while {f₁, f₂, f₃, f₄} are not selected.