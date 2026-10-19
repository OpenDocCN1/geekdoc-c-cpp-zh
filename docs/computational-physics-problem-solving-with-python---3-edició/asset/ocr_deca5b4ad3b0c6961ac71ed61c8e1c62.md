# 22.4.1

# Algorithm

The algorithm for the solution of the two-particle Schrödinger equation (22.26) in one dimension x, is similar to the one we outlined for the solution for a single particle in the two dimensions x and y, only now with x → x₁ and y → x₂. As usual, we assume discrete space and time

x₁ = l Δx₁ ,   x₂ = m Δx₂ ,   t = n Δt . (22.32)

We employ the improved algorithm for the time derivative introduced by Askar and Cakmak (1977), which uses a central difference algorithm applied to the formal solution (22.16)

ψₗ,ₘⁿ⁺¹ − ψₗ,ₘⁿ⁻¹ = (e⁻ⁱΔtH − eⁱΔtH) ψₗ,ₘⁿ ≃ −2i Δt H ψₗ,ₘⁿ , (22.33)

⇒ ψₗ,ₘⁿ⁺¹ ≃ ψₗ,ₘⁿ⁻¹ − 2i [ { (1/m₁ + 1/m₂) 4λ + Δx Vₗ,ₘ } ψₗ,ₘⁿ − λ { 1/m₁ (ψₗ₊₁,ₘⁿ + ψₗ₋₁,ₘⁿ) + 1/m₂ (ψₗ,ₘ₊₁ⁿ + ψₗ,ₘ₋₁ⁿ) } ] , (22.34)

where we have assumed Δx₁ = Δx₂ = Δx and formed the ratio λ = Δt / Δx². Again we will take advantage of the extra degree of freedom provided by the complexity of the wavefunction

ψₗ,ₘⁿ⁺¹ = Rₗ,ₘⁿ⁺¹ + i Iₗ,ₘⁿ⁺¹ , (22.35)

and staggered times to preserve probability better (Visscher, 1991). The algorithm (22.34) then separates into the pair of coupled equations

Rₗ,ₘⁿ⁺¹ = Rₗ,ₘⁿ⁻¹ + 2 [ { (1/m₁ + 1/m₂) 4λ + Δt Vₗ,ₘ } Iₗ,ₘⁿ − λ { 1/m₁ (Iₗ₊₁,ₘⁿ + Iₗ₋₁,ₘⁿ) + 1/m₂ (Iₗ,ₘ₊₁ⁿ + Iₗ,ₘ₋₁ⁿ) } ] , (22.36)

Iₗ,ₘⁿ⁺¹ = Iₗ,ₘⁿ⁻¹ − 2 [ { (1/m₁ + 1/m₂) 4λ + Δt Vₗ,ₘ } Rₗ,ₘⁿ − λ { 1/m₁ (Rₗ₊₁,ₘⁿ + Rₗ₋₁,ₘⁿ) 1/m₂ (Rₗ,ₘ₊₁ⁿ + Rₗ,ₘ₋₁ⁿ) } ] . (22.37)

# 22.4.2

# Implementation

We assume that the particle–particle potential is central and depends only on the relative distance between particles 1 and 2 (the method can handle any x₁ and