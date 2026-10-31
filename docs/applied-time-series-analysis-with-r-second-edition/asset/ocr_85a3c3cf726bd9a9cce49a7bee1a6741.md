once, m_i = 2, and if r_i is not repeated, then m_i = 1), ∑_{i=1}^ν m_i = m, and C_{ij} are uniquely determined by the initial conditions

g_1 = h_1
g_2 = h_2
⋮
g_m = h_m

where the h_j are constants. When there are no repeated roots, Equation 3.45 simplifies to

g_k = C_1 r_1^{-k} + C_2 r_2^{-k} + ... + C_m r_m^{-k}. (3.46)

From Equations 3.38 and 3.45, it follows that for an AR(p) model,

ρ_k = ∑_{i=1}^ν ∑_{j=0}^{m_i -1} C_{ij} k^j r_i^{-k}, (3.47)

where

∑_{i=1}^ν m_i = p,

and the initial conditions are given by

ρ_k = φ_1 ρ_{k-1} + ... + φ_p ρ_{k-p}, (3.48)

k = 1, 2, ..., p. Note that ρ_k → 0 as k → ∞ in Equation 3.47 if and only if |r_i| > 1, i = 1, ..., p, and thus it follows from Theorem 3.2 and the comments following it that ρ_k → 0 as k → ∞ is a necessary and sufficient condition for the model in Equation 3.17 to be a causal and stationary AR(p) process. In addition, note that if none of the roots are repeated, it follows from Equation 3.46 that for k > 0

ρ_k = C_1 r_1^{-k} + C_2 r_2^{-k} + ... + C_p r_p^{-k}. (3.49)