x₂ functional dependences if needed). For example, we have used both a “soft” potential with a Gaussian dependence and a “hard” potential with a square-well dependence:

```
V(x₁, x₂) = { V₀ exp[ -|x₁ - x₂|² / (2a²) ]   (Gaussian)
               { V₀ θ(α - |x₁ - x₂|)      (Square) ,   (22.38)
```

where α is the range parameter and V₀ is the depth parameter.

Because we are solving a PDE, we must specify both initial and boundary conditions. For scattering, we assume that particle 1 is initially at x₁⁰ with momentum k₁, and that particle 2 is initially far away at x₂⁰ ≃ ∞ with momentum k₂. Since the particles are initially too far apart to be interacting, we assume that the initial wave packet is a product of independent wave packets for particles 1 and 2

```
ψ(x₁, x₂, t = 0) = e^{i k₁ x₁} e^{-(x₁ - x₁⁰)² / (4σ²)} × e^{i k₂ x₂} e^{-(x₂ - x₂⁰)² / (4σ²)} .   (22.39)
```

Because of the Gaussian factors here, ψ is not an eigenstate of the momentum operator −i∂/∂xᵢ for either particle 1 or 2, but instead contains a spread of momenta about the mean, initial momenta k₁ and k₂. If the wave packet is made very broad (σ → ∞), we would obtain momentum eigenstates, but then would have effectively eliminated the wave packets. Note that while the Schrödinger equation may separate into one equation in the relative coordinate x = x₁ − x₂ and another in the center-of-mass coordinate X = (m₁x₁ + m₂x₂)/(m₁ + m₂), the initial condition (22.39), or more general ones, cannot be written as a product of separate functions of x and X, and accordingly, a solution of the partial differential equation in two variables is required (Landau, 1996).

We start the staggered-time algorithm with the real part the wavefunction (22.39) at t = 0 and the imaginary part at t = Δt/2. The initial imaginary part follows by assuming that Δt/2 is small enough and σ is large enough for the initial time dependence of the wave packet to be that of the plane wave parts:

```
I(x₁, x₂, t = Δt/2) ≃ sin[ k₁x₁ + k₂x₂ − (k₁²/(2m₁) + k₂²/(2m₂)) (Δt/2) ]
                     × exp[ -[ (x₁ - x₁⁰)² + (x₂ - x₂⁰)² ] / (2σ²) ] .   (22.40)
```

In an actual scattering experiment, a projectile starts at infinity and the scattered particles are observed also at infinity. We model that by solving our partial differential equation within a box of side L that in ideal world would be much larger than both the range of the potential and the width of the initial wave packet. This leads to the boundary conditions

```
ψ(0, x₂, t) = ψ(x₁, 0, t) = ψ(L, x₂, t) = ψ(x₁, L, t) = 0 .   (22.41)
```

The largeness of the box minimizes the effects of the boundary conditions during the collision of the wave packets, although at large times there will be artificial collisions with the box that do not correspond to actual experimental conditions.