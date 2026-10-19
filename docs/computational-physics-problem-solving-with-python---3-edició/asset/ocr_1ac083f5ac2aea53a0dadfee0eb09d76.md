![](bbox=[0.17, 0.11, 0.82, 0.28])

Figure 26.3 (a) A projectile (dark particle at r) scattering from a dense medium. (b) The same process viewed in the CM system where the projectile and target always have equal and opposite momenta.

# 26.4

# Lippmann–Schwinger Equation (Theory)

Because experiments measure scattering amplitudes and not wave functions, it is more direct to have a theory dealing with amplitudes rather than wave functions.³) An integral form of the Schrödinger equation dealing with the scattering amplitude R is the Lippmann–Schwinger equation:

```
R(k′, k) = V(k′, k) + (2/π) P ∫₀^∞ dp [p² V(k′, p) R(p, k) / ((k₀² − p²)/2μ)] , (26.20)
```

where the symbol P in (26.20) indicates the Cauchy principal-value prescription for avoiding the singularity arising from the zero of the denominator (we discuss how to do that next). As for the bound-state problem, this equation is for partial wave l = 0 and ħ = 1. In (26.20), the momentum k₀ is related to the energy E and the reduced mass μ by

```
E = k₀² / (2μ) , μ = (m₁ m₂)/(m₁ + m₂) . (26.21)
```

The initial and final COM momenta k and k′ are the momentum–space variables. The experimental observable that results from a solution of (26.20) is the diagonal matrix element R(k₀, k₀), which is related to the scattering phase shift δ₀ and thus the cross section:

```
R(k₀, k₀) = − tan δₗ / ρ , ρ = 2μ k₀ . (26.22)
```

Note that (26.20) is not just the evaluation of an integral, it is an integral equation in which R(p, k) is integrated over all p. Yet because R(p, k) is unknown, the integral cannot be evaluated until after the equation is solved!

> 3) To make the presentation simpler, but still perfectly valid, we solve for the reaction matrix R, but call it the scattering amplitude.