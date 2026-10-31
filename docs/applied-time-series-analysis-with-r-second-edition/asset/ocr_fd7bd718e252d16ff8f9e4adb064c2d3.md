As noted above, for an AR(p) process, it follows from Equation 3.47 that ρ_k → 0 (and equivalently γ_k → 0) as k → ∞. From Theorem 1.1, it then follows that Γ_k and ρ_k defined in Equations 1.2 and 1.3, respectively, are positive definite for each integer k > 0 in the case of an AR process.

# EXAMPLE 3.5: AUTOCORRELATIONS OF AN AR(1) MODEL

For the case of the AR(1) model X_t - φ₁ X_{t-1} = a_t, the autocorrelation ρ_k satisfies the difference equation

ρ_k - φ₁ ρ_{k-1} = 0,   k > 0. (3.50)

Since there is only one root (and thus no repeated roots), we use Equation 3.49, and ρ_k satisfies. ρ_k = C₁ r₁^{-k}, k > 0 Also, for an AR(1) model, r₁ = 1 / φ₁, so this can be rewritten

ρ_k = C₁ φ₁^{k},   k > 0. (3.51)

Since ρ₀ = 1, it follows from Equation 3.50 that ρ₁ - φ₁ ρ₀ = 0. Thus, ρ₁ = φ₁, and thus C₁ = 1. Notice that ρ₀ = 1 = φ₁⁰, so

ρ_k = φ₁^{k},   k ≥ 0. (3.52)

Since ρ_k = ρ_{-k}, the autocorrelation function for an AR(1) process satisfies ρ_k = φ₁^{|k|} which is the result given earlier in Equation 3.32.

NOTE: In general, for the mth-order difference equation with no repeated roots, the values C₁, ..., C_m are chosen in such a way that the starting values, g_j, g_{j-1}, ..., g_{j+1-m} also satisfy Equation 3.46 although they do not satisfy Equation 3.44.

NOTE: In Equation 3.77, we will give an expression for Equation 3.49 that provides better insight into the behavior of the autocorrelation function of an AR(p) model.

# 3.2.6 Spectral Density of an AR(p) Model