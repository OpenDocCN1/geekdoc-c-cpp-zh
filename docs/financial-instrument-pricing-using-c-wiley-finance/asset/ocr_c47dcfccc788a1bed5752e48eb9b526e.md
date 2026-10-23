where:

k₁ = f(t, y)
k₂ = f(t + h/2, y + ½ h k₁)
k₃ = f(t + h/2, y + ½ h k₂)
k₄ = f(x + h, y + h k₃).

Other methods are:

# Second-order Ralston method:

yₙ₊₁ = yₙ + ¼(k₁ + 3k₂)
k₁ = h f(tₙ, yₙ)    (24.34)
k₂ = h f(tₙ + 2h/3, yₙ + 2k₁/3).

# Heun’s (improved Euler) method:

ỹₙ₊₁ = yₙ + h f(tₙ, yₙ)
yₙ₊₁ = yₙ + h/2 [f(tₙ, yₙ) + f(tₙ₊₁, ỹₙ₊₁)].    (24.35)

This is a predictor–corrector method that also has applications to stochastic differential equations.

In general, explicit Runge–Kutta methods are unsuitable for stiff ODEs.

# 24.6.3 Richardson Extrapolation Methods

Extrapolation procedures are usually applied to partial differential equations but they can also be applied to Runge–Kutta methods for ODE systems. Let us assume that we are using a Runge–Kutta method to approximate the solution of system (24.24). Then on meshes of size h and h/2 we have the following error estimates:

yʰ = y + M hᵖ⁺¹ + O(hᵖ⁺²)
yʰ/² = y + M (h/2)ᵖ⁺¹ + O(hᵖ⁺²).    (24.36)

In (24.36) the constant M is independent of h but depends on y.

Some basic mathematics allows us to improve the accuracy. We define the mesh function wʰ/² by:

wʰ/² = [2ᵖ⁺¹ uʰ/² − uʰ] / [2ᵖ⁺¹ − 1] = u + O(hᵖ⁺²).    (24.37)

For example, extrapolation can be applied to the Ralston method (24.34) in the case ρ = 1.