# Semi-implicit Euler:

X_{n+1} = X_n + [α μ_{n+1} + (1 − α) μ_n] Δt + σ_n ΔW_n
with special cases:
α = 1/2 (Trapezoidal), α = 1 (Backward Euler). (14.3)

# Heun:

X_{n+1} = X_n + 1/2 [F_1 + F_2] Δt + 1/2 [G_1 + G_2] ΔW_n
where:
F(x) ≡ μ(x) − 1/2 σ'(x) σ(x) where σ'(x) ≡ dσ/dx
F_1 = F(X_n), G_1 = σ(X_n)
F_2 = F(X_n + F_1 Δt + G_1 ΔW_n)
G_2 = σ(X_n + F_1 Δt + G_1 ΔW_n). (14.4)

# Milstein:

X_{n+1} = X_n + μ_n Δt + σ_n ΔW_n + 1/2 [σ' σ]_n ((ΔW_n)^2 − Δt). (14.5)

# Derivative free

X_{n+1} = X_n + F_1 Δt + G_1 ΔW_n + [G_2 − G_1] Δt^{−1/2} ( (ΔW_n)^2 − Δt ) / 2
where:
F_1 = μ(X_n), G_1 = σ(X_n) G_2 = σ(X_n + G_1 Δt^{1/2}). (14.6)

# First-order Runge–Kutta with Ito coefficient (FRKI):

X_{n+1} = X_n + F_1 Δt + G_2 ΔW_n + [G_2 − G_1] Δt^{1/2}
where:
F_1 = μ(X_n), G_1 = σ(X_n) G_2 = σ( X_n + G_1 (ΔW_n − Δt^{1/2}) / 2 ). (14.7)

In this section we extend the C++ code of Section 6.8 in Chapter 6 that models SDEs. In particular, we simulate the paths of SDEs using the above finite difference methods. We design part of the system context diagram of Figure 7.1 (and related topics in Chapter 9).

The main systems are:

+   - S1: The option (derivative) input data.
+   - S2: Modelling one-factor SDEs.
+   - S3: Modelling finite difference schemes.
+   - S4: Presenting SDE paths in Excel.
+   - S5: A Builder/Factory system to configure and initialise the systems S1 to S4.