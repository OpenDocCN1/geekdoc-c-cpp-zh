
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

## 22.2.2
### Wave Packet Implementation, Animation

In Listing 22.1, you will find the program HarmosAnimate.py that solves for the motion of the wave packet (22.1) inside a harmonic oscillator potential. The program Slit.py on the instructor’s site solves for the motion of a Gaussian wave packet as it passes through a slit (Figure 22.3). You should solve for a wave packet confined to the square well:

```
V(x) = { ∞ , x < 0 , or x > 15 , 0 , 0 ≤ x ≤ 15 . }
```

- 1. Define arrays psr[751,2] and psi[751,2] for the real and imaginary parts of ψ, and Rho[751] for the probability. The first subscript refers to the x position on the grid, and the second to the present and future times.
- 2. Use the values σ₀ = 0.5, Δx = 0.02, k₀ = 17π, and Δt = 1/2Δx².

![](img/bccda43674e4a93dee81c749eba8d2f7_537_0.png)

Figure 22.3 The probability density as a function of position and time for an electron incident upon and passing through a slit. Significant reflection is seen to occur.

![](img/bccda43674e4a93dee81c749eba8d2f7_539_0.png)

Figure 22.4 The probability density as a function of x and y at three different times for an electron confined to a 2D parabolic tube (infinite in the y direction). The electron is initially placed in a Gaussian wave packet in both the x and y directions, and it is to be noted how there is spreading of the wave packet in the y direction, but not in the x direction.

## 22.2.3
### Wave Packets in Other Wells (Exploration)

1D Well Now confine the electron to a harmonic oscillator potential:

```
V(x) = 1/2 x^2    (-∞ ≤ x ≤ ∞) .    (22.12)
```

Take the momentum k0 = 3π, the space step Δx = 0.02, and the time step Δt = 1/4 Δx². Note that the wave packet broadens yet returns to its initial shape!

2D Well Now confine the electron to a 2D parabolic tube (Figure 22.4):

```
V(x, y) = 0.9 x² ,    -9.0 ≤ x ≤ 9.0 ,    0 ≤ y ≤ 18.0 .    (22.13)
```

The extra degree of freedom means that we must solve the 2D PDE:

```
i ∂ψ(x, y, t)/∂t = - ( ∂²ψ/∂x² + ∂²ψ/∂y² ) + V(x, y) ψ .    (22.14)
```

Assume that the electron’s initial localization is described by the 2D Gaussian wave packet:

```
ψ(x, y, t = 0) = e^{i k0x x} e^{i k0y y} exp[ -(x - x0)² / (2 σ0²) ] exp[ -(y - y0)² / (2 σ0²) ] .    (22.15)
```

Note that you can solve the 2D equation by extending the method we just used in 1D or you can look at the next section where we develop a special algorithm.

## 22.3
### Algorithm for the 2D Schrödinger Equation

One way to develop an algorithm for solving the time-dependent Schrödinger equation in 2D is to extend the 1D algorithm to another dimension. Rather than that, we apply quantum theory directly to obtain a more powerful algorithm (Maestri et al., 2000). First, we note that Equation 22.14 can be integrated in a formal sense (Landau and Lifshitz, 1976) to obtain the operator solution:

ψ(x, y, t) = U(t) ψ(x, y, t = 0) ,  (22.16)
U(t) = e^{-iĤt} ,  (22.17)
Ĥ = - (∂²/∂x² + ∂²/∂y²) + V(x, y) ,

where U(t) is an operator that translates a wave function by an amount of time t and Ĥ is the Hamiltonian operator. From this formal solution, we deduce that a wave packet can be translated ahead by time Δt via

ψ^{n+1}_{i,j} = U(Δt) ψ^n_{i,j} ,  (22.18)

where the superscripts denote time t = nΔt and the subscripts denote the two spatial variables x = iΔx and y = jΔy. Likewise, the inverse of the time evolution operator moves the solution back one time step:

ψ^{n-1} = U^{-1}(Δt) ψ^n = e^{+iĤΔt} ψ^n .  (22.19)

While it would be nice to have an algorithm based on a direct application of (22.19), the references show that the resulting algorithm would not be stable. That being so, we base our algorithm on an indirect application (Askar and Cakmak, 1977), namely, the relation between the difference in ψ^{n+1} and ψ^{n-1}:

ψ^{n+1} = ψ^{n-1} + [e^{-iĤΔt} - e^{+iĤΔt}] ψ^n ,  (22.20)

where the difference in sign of the exponents is to be noted. The algorithm derives from combining the O(Δx²) expression for the second derivative obtained from the Taylor expansion,

∂²ψ/∂x² ≃ -1/2 [ ψ^n_{i+1,j} + ψ^n_{i-1,j} - 2 ψ^n_{i,j} ] ,  (22.21)

with the corresponding-order expansion of the evolution equation (22.20). Substituting the resulting expression for the second derivative into the 2D time-dependent Schrödinger equation results in¹)

```
ψ_{i,j}^{n+1} = ψ_{i,j}^{n-1} - 2i[ (4α + ½ Δt V_{i,j}) ψ_{i,j}^{n} - α( ψ_{i+1,j}^{n} + ψ_{i-1,j}^{n} + ψ_{i,j+1}^{n} + ψ_{i,j-1}^{n} ) ] , (22.22)
```

where α = Δt / 2(Δx)². We convert this complex equations to coupled real equations by substituting them into the wave function ψ = R + iI,

```
R_{i,j}^{n+1} = R_{i,j}^{n-1} + 2[ (4α + ½ Δt V_{i,j}) I_{i,j}^{n} - α( I_{i+1,j}^{n} + I_{i-1,j}^{n} + I_{i,j+1}^{n} + I_{i,j-1}^{n} ) ] , (22.23)
```

```
I_{i,j}^{n+1} = I_{i,j}^{n-1} - 2[ (4α + ½ Δt V_{i,j}) R_{i,j}^{n} + α( R_{i+1,j}^{n} + R_{i-1,j}^{n} + R_{i,j+1}^{n} + R_{i,j-1}^{n} ) ] . (22.24)
```

This is the algorithm we use to integrate the 2D Schrödinger equation. To determine the probability, we use the same expression (22.11) used in 1D.

## 22.3.1
### Exploration: Bound and Diffracted 2D Packet

- 1. Determine the motion of a 2D Gaussian wave packet within a 2D harmonic oscillator potential:
- V(x, y) = 0.3(x² + y²) ,  -9.0 ≤ x ≤ 9.0 ,  -9.0 ≤ y ≤ 9.0 . (22.25)

- 2. Center the initial wave packet at (x, y) = (3.0, -3) and give it momentum (k₀ₓ, k₀y) = (3.0, 1.5).

- 3. Young’s single-slit experiment has a wave passing through a small slit with the transmitted wave showing interference effects. In quantum mechanics, where we represent a particle by a wave packet, this means that an interference pattern should be formed when a particle passes through a small slit. Pass a Gaussian wave packet of width 3 through a slit of width 5 (Figure 22.3), and look for the resultant quantum interference.

## 22.4
### Wave Packet–Wave Packet Scattering²)

We have just seen how to represent a quantum particle as a wave packet and how to compute the interaction of that wave packet/particle with an external potential.

> 1) For reference sake, note that the constants in the equation change as the dimension of the equation changes; that is, there will be different constants for the 3D equation, and therefore our constants are different from the references!

> 2) This section is based on the Master of Science thesis of Jon Maestri. It is included in his memory.

Although external potentials do exist in nature, realistic scattering often involves the interaction of one particle with another, which in turn would be represented as the interaction of a wave packet with a different wave packet. We have already done the hard work needed to compute wave packet–wave packet scattering in our implementation of wave packet–potential scattering even in 2D. We now need only to generalize it a bit.

Two interacting particles are described by the time-dependent Schrödinger equation in the coordinates of the two particles

i ∂ψ(x₁, x₂, t)/∂t = - 1/(2m₁) ∂²ψ(x₁, x₂, t)/∂x₁² - 1/(2m₂) ∂²ψ(x₁, x₂, t)/∂x₂² + V(x₁, x₂)ψ(x₁, x₂, t) . (22.26)

where, for simplicity, we assume a one-dimensional space and again set ℏ = 1. Here mᵢ and xᵢ are the mass and position of particle i = 1, 2. Knowledge of the two-particle wavefunction ψ(x₁, x₂, t) at time t permits the calculation of the probability density of particle 1 being at x₁ and particle 2 being at x₂:

ρ(x₁, x₂, t) = |ψ(x₁, x₂, t)|² . (22.27)

The fact that particles 1 and 2 must be located somewhere in space leads to the normalization constraint on the wavefunction

∫_{-∞}^{+∞} ∫_{-∞}^{+∞} dx₁ dx₂ ρ(x₁, x₂, t) = 1 . (22.28)

The description of a particle within a multiparticle system by a single-particle wavefunction is an approximation unless the system is uncorrelated, in which case the total wavefunction can be written in product form. However, it is possible to deduce meaningful one-particle probabilities (also denoted by ρ) from the two-particle density by integrating over the other particle:

ρ(xᵢ, t) = ∫_{-∞}^{+∞} dxⱼ ρ(x₁, x₂, t) , (i ≠ j = 1, 2) . (22.29)

Of course, the true solution of the Schrödinger equation is ψ(x₁, x₂, t), but we find it hard to unravel the physics in a three-variable complex function, and so will usually view ρ(x₁, t) and ρ(x₂, t) as two separate wave packets colliding.

If particles 1 and 2 are identical, then their total wavefunction must be symmetric (s) or antisymmetric (a) under interchange of the particles. We impose this condition on our numerical solution ψ(x₁, x₂), by forming the combinations

ψ^{s,a}(x₁, x₂) = 1/√2 [ψ(x₁, x₂) ± ψ(x₂, x₁)] ⇒ (22.30)

2ρ(x₁, x₂) = |ψ(x₁, x₂)|² + |ψ(x₂, x₁)|² ± 2 Re [ψ*(x₁, x₂)ψ(x₂, x₁)] . (22.31)

The cross term in (22.31) places an additional correlation into the wave packets.
