where C is constant independent of the initial data p₀ⁱ.

Let us define the attraction set of qᵢ as K(qᵢ) = {x : (8) with x as the initial state converges to a point in B(qᵢ, γ)}.

Since the Hessian matrix of g(x) has negative eigenvalues near of qᵢ, we find B(qᵢ, γ) ⊆ K(qᵢ) provided γ is small enough. Thus, for any given α ∈ (0,1) there exists σ₀ such that for σᵢ < σ₀, (13) implies ∫_U p̄σᵢ(x)dx > α + (1 − α)/2. (16)

Also, there exists a τ(α) such as for Tᵢ − Sᵢ > τ(α), (15) gives us ‖pσᵢ(Tᵢ − Sᵢ, x) − p̄σᵢ(x)‖_{L¹} < (1 − α)/2. (17)

Therefore, by (16) and (17), we have ∫_U pσᵢ(Tᵢ − Sᵢ, x)dx ≥ ∫_U p̄σᵢ(x)dx − ∫_U |pσᵢ(Tᵢ − Sᵢ, x) − p̄σᵢ(x)| dx > α. (18)

This implies that P(x(Sᵢ₊₁) ∈ U | x(Sᵢ) ∈ B(qᵢ, γᵢ)) = P(x(Tᵢ) ∈ K(x*) | x(Sᵢ) ∈ B(qᵢ, γᵢ)) > α, (19) due to the fact that the ID method is deterministic on [Tᵢ, Sᵢ₊₁].

Let Θ be the set consisting of local minimizers of g, then P(x(Sᵢ₊₁) ∈ Uᶜ) = Σ_{qᵢ∈Θ} P(x(Sᵢ₊₁) ∈ Uᶜ | x(Sᵢ) ∈ B(qᵢ, γᵢ)) × P(x(Sᵢ) ∈ B(qᵢ, γᵢ)), (20) where Uᶜ is the complement of U. By estimate (19), we have P(x(Sᵢ₊₁) ∈ Uᶜ | x(Sᵢ) ∈ B(qᵢ, γᵢ)) < (1 − α) for all qᵢ ∈ Θ, (21) provided (Tᵢ − Sᵢ) > τ and σᵢ < σ₀. This implies P(x(Sᵢ₊₁) ∈ Uᶜ) < (1 − α) Σ_{qᵢ∈Θ} P(x(Sᵢ) ∈ B(qᵢ, γᵢ)) < (1 − α). (22)

The estimate (22) can be made for all segments i = 1,2,…,N uniformly. We remark that the estimate (22) is independent of which neighborhood

B(qᵢ, γᵢ) the x(Sᵢ) will lie in. Since x(Sᵢ) must lie in some B(qᵢ, γᵢ), if we repeat it for all intervals [Sⱼ, Sⱼ₊₁], j = 1,…,N, with the same fixed α, then the probability that the solution X_opt of the ID method does not belong to U satisfies, P(X_opt ∈ Uᶜ) = P(⋂_{i=0}^N {x(Sᵢ) ∈ Uᶜ}) < (1 − α)^N.

For any given ε ∈ (0,1), there exists N₀ > 0, such as for N ≥ N₀, P(X_opt ∈ Uᶜ) < (1 − α)^N < ε, which is equivalent to (9).

It it easy to obtain the following statement from the proof.

# Corollary 37.1. Assume the probability of attaining an approximation in U, a small neighborhood of the global minimizer x*, in one segment of the ID process is α ∈ (0,1), and there are N segments, then the best approximation X_opt obtained by the ID method satisfies P(X_opt ∈ U) ≥ 1 − (1 − α)^N. (23)

Furthermore, if we pick α ≥ 1/2 in the proof, it implies that x(Sᵢ₊₁) has larger probability in U than in the neighborhoods of other local minimizers.

We summarize this extension in the following theorem.

# Theorem 2. Consider the ID process for the gradient flow stated in Theorem 1. If 0 < γ ≪ 1, then P(x(Sᵢ₊₁, ω) ∈ U) ≥ P(x(Sᵢ₊₁, ω) ∈ B(qⱼ, γ)), where qⱼ is any local minimizer, provided Tᵢ − Sᵢ is large and σᵢ small enough.

We remark that the ID method indicates the convergence is monotone with respect to the number of segments N. And the convergence rate is a geometric series based on the factor α. The following theorem reveals more properties of the ID method.

# Theorem 3. Consider the ID method for the randomly perturbed gradient flow (2) and suppose that g ∈ C² satisfies (H2) and the following conditions: (H3) lim_{|x|→∞} g(x) = ∞. (H4) ∇g has a Lipschitz constant L on ℝⁿ. Given 0 < ε, T > 0 and any finite sequence {pᵢ}_{i=1…N} of local minimizers of g, there exist a