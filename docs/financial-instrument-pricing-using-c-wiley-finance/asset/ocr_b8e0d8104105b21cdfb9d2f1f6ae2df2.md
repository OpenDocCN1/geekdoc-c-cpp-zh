(20.9) represents Neumann boundary conditions. Finally, the solution of the Cauchy problem for equation (20.1) in the infinite region ℝⁿ × (0, T) is given by the initial condition:

u|ₜ=ₙ = φ(x)  (20.10)

where φ(x) is a given continuous function and u(x, t) satisfies equation (20.1) in ℝⁿ × (0, T) and the initial condition (20.10). This problem allows negative values of the components of the independent variable x = (x₁, ..., xₙ). A special case of the Cauchy problem can be seen when modelling one-factor European and American options where x plays the role of the underlying asset S. Boundary conditions are given by values at S = 0 and at S = ∞. For European call options these conditions are:

C(0, t) = 0
C(S, t) → S as S → ∞.  (20.11)

Here C (the role played by u in equation (20.1)) is the price of the call option. For European put options the boundary conditions are:

P(0, t) = K e⁻ʳᵗ
P(S, t) → 0 as S → ∞.  (20.12)

Here P (the role played by u in equation (20.1)) is the variable representing the price of the put option, K is the strike price, r is the risk-free interest rate, T is the expiration and t is the current time.

We sometimes assume the following ‘canonical’ form for the operator L in equation (20.1) in the one-factor case:

Lu ≡ −∂u/∂t + σ(s, t) ∂²u/∂x² + μ(x, t) ∂u/∂x + b(x, t)u = f(x, t)  (20.13)

where σ, μ, b and f are known functions of x and t.

For completeness, we formulate the one-factor initial boundary value problem whose solution we wish to approximate using the finite difference method. To this end, we define the interval Ω = (A, B) where A and B are two real numbers with A < B. Further, let T > 0 and D = Ω × (0, T). The statement is:

Find a function u : D → ℝ¹ such that:

Lu = −∂u/∂t + σ(x, t) ∂²u/∂x² + μ(x, t) ∂u/∂x + b(x, t)u = f(x, t) in D  (20.14)
u(x, 0) = φ(x), x ∈ Ω  (20.15)
u(A, t) = g₀(t), u(B, t) = g₁(t), t ∈ (0, T).  (20.16)

The initial boundary value problem (20.14)–(20.16) subsumes many specific cases (in particular it is a generalisation of the Black–Scholes equation).

In general, the coefficients σ(x, t) and u(x, t) represent volatility (diffusivity) and drift (convection), respectively. Equation (20.14) is called a convection–diffusion–reaction equation. It serves as a model for many kinds of problems. Much research has been carried out in this