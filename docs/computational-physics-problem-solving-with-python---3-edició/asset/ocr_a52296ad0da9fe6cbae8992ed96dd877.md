where α = Δt/2(Δx)². In the discrete form with Rₓ=iΔxᵗ=nΔt, we have

```
Rᵢⁿ⁺¹ = Rᵢⁿ − 2 { α [ Iᵢ₊₁ⁿ + Iᵢ₋₁ⁿ ] − 2 [ α + VᵢΔt ] Iᵢⁿ } , (22.9)
Iᵢⁿ⁺¹ = Iᵢⁿ + 2 { α [ Rᵢ₊₁ⁿ + Rᵢ₋₁ⁿ ] − 2 [ α + VᵢΔt ] Rᵢⁿ } , (22.10)
```

where the superscript n indicates the time and the subscript i the position.

The probability density ρ is defined in terms of the wave function evaluated at three different times:

```
ρ(t) = { R²(t) + I(t + Δt/2) I(t − Δt/2) , for integer t , I²(t) + R(t + Δt/2) R(t − Δt/2) , for half-integer t . } (22.11)
```

Although probability is not conserved exactly with this algorithm, the error is two orders higher than that in the wave function, and this is usually quite satisfactory. If it is not, then we need to use smaller steps. While this definition of ρ may seem strange, it reduces to the usual one for Δt → 0 and so can be viewed as part of the art of numerical analysis. We will ask you to investigate just how well probability is conserved. We refer the reader to Koonin (1986) and Visscher (1991) for details on the stability of the algorithm.

# 22.2.2

# Wave Packet Implementation, Animation

In Listing 22.1, you will find the program HarmosAnimate.py that solves for the motion of the wave packet (22.1) inside a harmonic oscillator potential. The program Slit.py on the instructor’s site solves for the motion of a Gaussian wave packet as it passes through a slit (Figure 22.3). You should solve for a wave packet confined to the square well:

```
V(x) = { ∞ , x < 0 , or x > 15 , 0 , 0 ≤ x ≤ 15 . }
```

+   1. Define arrays psr[751,2] and psi[751,2] for the real and imaginary parts of ψ, and Rho[751] for the probability. The first subscript refers to the x position on the grid, and the second to the present and future times.
+   2. Use the values σ₀ = 0.5, Δx = 0.02, k₀ = 17π, and Δt = 1/2Δx².

![](bbox=[0.18, 0.78, 0.82, 0.88])

Figure 22.3 The probability density as a function of position and time for an electron incident upon and passing through a slit. Significant reflection is seen to occur.