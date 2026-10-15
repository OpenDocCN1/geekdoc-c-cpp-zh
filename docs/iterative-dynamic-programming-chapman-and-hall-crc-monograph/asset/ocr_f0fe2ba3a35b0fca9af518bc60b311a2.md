![](bbox=[0.28, 0.06, 0.64, 0.42])

Figure 1.3: Convergence profile for Example 1, where the equations are arranged so that there are two difficult equalities, showing the effect of the starting conditions

x₄ = (4 − 0.5(x₆ + x₇)) / (1 + 0.193 x₂ / x₁₀)  (1.98)
x₅ = 0.193 x₂ x₄ / x₁₀  (1.99)
x₁₂ = 40  (1.100)
x₃ = 2 x₁₂ − 0.5 x₅  (1.101)
x₈ = (1.799 x₄ x₁) / (3.846 x₂)  (1.102)
x₉ = (2.155 × 10⁻⁴ x₁₀ √(x₃ x₁₁)) / x₂  (1.103)
f₁ = 2(x₁ + x₁₀) + x₂ + x₄ + x₇ + x₈ + x₉ − x₁₂ = 0  (1.104)
f₂ = Σᵢ₌₁¹⁰ xᵢ − x₁₁ = 0.  (1.105)

Here we have two difficult equality constraints. The free variables are x₁ and x₂. Two sets of initial values for these variables were taken, namely (0.1, 0.1) and (0.5, 0.5). The only precaution required was to keep x₁ and x₂ positive so that the square root could be calculated. Thus, if x₁ or x₂ were calculated to be less than 10⁻⁴, then 10⁻⁴ was arbitrarily assigned. This precaution eliminates any possibility of numerical