![](bbox=[0.22, 0.12, 0.78, 0.35])

# FIGURE 8.20

Examples of 2-maps and their Euler-Poincaré characteristics.

+   (a) M₁ describes a sphere: χ(M₁) = 2.
+   (b) M₂ describes a torus: χ(M₂) = 0.

characteristic χ(M) is the alternated sum:

χ(M) = (-1)^(n-1)(n - 1)|D| + Σ_{i=2}^n (-1)^(n-i) Σ_{0<k₁<...<k_{i-1}≤n} #⟨β_{k₁},...,β_{k_{i-1}}⟩ + Σ_{i=2}^n (-1)^(n-i) Σ_{0<k₀<...<k_{i-1}≤n} #⟨β_{k₁}∘β_{k₀},...,β_{k_{i-1}}∘β_{k₀}⟩.

Note that it is possible to extend this formula to consider n-maps with boundary, but the definition becomes more complex since the case of free darts has to be taken into account.

For 1D, the previous definition becomes χ(M) = 0. Any 1-map M without boundary (i.e. closed polygonal curves) has the Euler-Poincaré characteristic of a circle.

For 2D, the previous definition becomes χ(M) = -|D| + #⟨β₁⟩ + #⟨β₂⟩ + #⟨β₂∘β₁⟩. Figure 8.20 shows two examples of 2-maps and their corresponding Euler-Poincaré characteristics. For M₁ given in Fig. 8.20(a), |D| = 6, #⟨β₁⟩ = 3, #⟨β₂⟩ = 3, #⟨β₂∘β₁⟩ = 2: thus χ(M₁) = -6 + 3 + 3 + 2 = 2: this is the Euler-Poincaré characteristic of a sphere. For M₂ given in Fig. 8.20(b), |D| = 4, #⟨β₁⟩ = 1, #⟨β₂⟩ = 2, #⟨β₂∘β₁⟩ = 1: thus χ(M₂) = -4 + 1 + 2 + 1 = 0: this is the Euler-Poincaré characteristic of a torus.

For 3D, the previous definition becomes χ(M) = 2|D| - #⟨β₁⟩ - #⟨β₂⟩ - #⟨β₃⟩ + #⟨β₁,β₂⟩ + #⟨β₁,β₃⟩ + #⟨β₂,β₃⟩ - #⟨β₂∘β₁⟩ - #⟨β₃∘β₁⟩ - #⟨β₃∘β₂⟩ + #⟨β₂∘β₁,β₃∘β₁⟩.

In 2D, the Euler-Poincaré characteristics of a 2-map without 1-boundary