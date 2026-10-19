
## 25.4.4
## Flow Assessment

- 1. Use Beam.py as a basis for your solution for the stream function u and the vorticity w using the finite-differences algorithm (25.36).
- 2. A good place to start your simulation is with a beam of size L = 8h, H = h, Reynolds number R = 0.1, and intake velocity V₀ = 1. Keep your grid small during debugging, say, Nₓ = 24 and Nᵧ = 70.
- 3. Explore the convergence of the algorithm.
  a) Print out the iteration number and u values upstream from, above, and downstream from the beam.
  b) Determine the number of iterations necessary to obtain three-place convergence for successive relaxation (ω = 0).
  c) Determine the number of iterations necessary to obtain three-place convergence for successive over-relaxation (ω ≈ 0.3). Use this number for future calculations.
- 4. Change the beam's horizontal placement so that you can see the undisturbed current entering on the left and then developing into a standing wave. Note that you may need to increase the size of your simulation volume to see the effect of all of the boundary conditions.
- 5. Make surface plots including contours of the stream function u and the vorticity w. Explain the behavior seen.
- 6. Is there a region where a big fish can rest behind the beam?
- 7. The results of the simulation (Figure 25.4) are for the one-component stream function u. Make several visualizations showing the fluid velocity throughout

![](img/bccda43674e4a93dee81c749eba8d2f7_612_0.png)

Figure 25.4 Two visualizations of the stream function u for Reynold's number R = 5. The one on the left uses contours, while the one on the right uses color.

## 25 Fluid Dynamics

![](img/bccda43674e4a93dee81c749eba8d2f7_613_0.png)

the simulation region. Note that the velocity is a vector with two components (or a magnitude and direction), and both degrees of freedom are interesting to visualize. A plot of vectors would work well here.

- 8. Explore how increasing the Reynolds number R changes the flow pattern. Start at R = 0 and gradually increase R while watching for numeric instabilities. To overcome the instabilities, reduce the size of the relaxation parameter ω and continue to larger R values.
- 9. Verify that the flow around the beam is smooth for small R values, but that it separates from the back edge for large R, at which point a small vortex develops, as can be seen in Figure 25.5.

## 25.4.5 Exploration

- 1. Determine the flow behind a circular rock in the stream.
- 2. The boundary condition at an outlet far downstream should not have much effect on the simulation. Explore the use of other boundary conditions there.
- 3. Determine the pressure variation around the beam.

![](img/bccda43674e4a93dee81c749eba8d2f7_615_0.png)

Figure 26.1 A dark particle moving in a dense medium in which it interacts with all particles present. The nonlocality of the potential felt by the dark particle at r arises from the interactions at all r′.

This type of interaction leads to a Schrödinger equation which is a combined integral and differential ("integro-differential") equation:

```
- 1/(2μ) d²ψ(r)/dr² + ∫ dr′ V(r, r′) ψ(r′) = E ψ(r) .  (26.2)
```

Your problem is to figure out how to find the bound-state energies Eₙ and wave functions ψₙ for the equation in (26.2).¹

## 26.2
## Momentum–Space Schrödinger Equation (Theory)

One way of dealing with (26.2) is by going to momentum space where it becomes the integral equation (Landau, 1996)

```
k²/(2μ) ψₙ(k) + 2/π ∫₀^∞ dp p² V(k, p) ψₙ(p) = Eₙ ψₙ(k) .  (26.3)
```

We restrict our solution to angular momentum l = 0 partial waves, but for simplicity of notation we do not include an index to indicate that. In (26.3), V(k, p) is the momentum–space representation (double Fourier transform) of the coordinate-space potential,

```
V(k, p) = 1/(k p) ∫₀^∞ dr sin(k r) V(r) sin(p r) .  (26.4)
```

ψₙ(k) is the momentum–space wave function (the probability amplitude for finding the particle with momentum k), and is the Fourier transform of ψₙ(r):

```
ψₙ(k) = ∫₀^∞ dr k r ψₙ(r) sin(k r) .  (26.5)
```

1) We use natural units in which ℏ ≡ 1.

Equation 26.3 is an integral equation for ψₙ(k). It differs from an integral representation of ψₙ(k), because the integral in it cannot be evaluated until ψₙ(p) is known. Although this may seem like an insurmountable barrier, we will transform this equation into a matrix equation that can be solved with the matrix techniques discussed in Chapter 6.

## 26.2.1
## Integral to Matrix Equations

We approximate the integral over the potential as a weighted sum over N integration points (usually Gauss quadrature points²) for p = kⱼ, j = 1, N:

```
∫₀^∞ d p p² V(k, p) ψₙ(p) ≈ Σⱼ=1^N wⱼ kⱼ² V(k, kⱼ) ψₙ(kⱼ) .    (26.6)
```

This converts the integral equation (26.3) to the algebraic equation

```
k²/(2μ) ψₙ(k) + 2/π Σⱼ=1^N wⱼ kⱼ² V(k, kⱼ) ψₙ(kⱼ) = Eₙ .    (26.7)
```

Equation 26.7 contains the N unknown function values ψₙ(kⱼ), the unknown Eₙ, as well as the unknown functional dependence of ψₙ(k). We eliminate the functional dependence of ψₙ(k) by restricting the solution to the same values of k = kᵢ as used in the approximation of the integral, which means that we are solving for wave function for k values on the grid of Figures 26.2. This leads to a set of N coupled linear equations in (N + 1) unknowns:

```
kᵢ²/(2μ) ψₙ(kᵢ) + 2/π Σⱼ=1^N wⱼ kⱼ² V(kᵢ, kⱼ) ψₙ(kⱼ) = Eₙ ψₙ(kᵢ) ,   i = 1, N .    (26.8)
```

As a concrete example, for N = 2 we have two simultaneous linear equations

```
k₁²/(2μ) ψₙ(k₁) + 2/π w₁ k₁² V(k₁, k₁) ψₙ(k₁) + w₂ k₂² V(k₁, k₂) ψₙ(k₂) = Eₙ ψₙ(k₁) ,
```

```
k₂²/(2μ) ψₙ(k₂) + 2/π w₁ k₁² V(k₂, k₁) ψₙ(k₁) + w₂ k₂² V(k₂, k₂) ψₙ(k₂) = Eₙ ψₙ(k₂) .
```

![](img/bccda43674e4a93dee81c749eba8d2f7_616_0.png)

Figure 26.2 The grid of momentum values on which the integral equation is solved.

2) See Chapter 5, for a discussion of numerical integration.

Of course, realistic examples require more than two integration points for precision.

We write our coupled equations (26.8) in the matrix form as

```
[H][ψₙ] = Eₙ[ψₙ]  (26.9)
```

or as explicit matrices

```
⎛ k₁²/(2μ) + 2/π V(k₁,k₁)k₁²w₁   2/π V(k₁,k₂)k₂²w₂   …   2/π V(k₁,k_N)k_N²w_N ⎞
⎜ 2/π V(k₂,k₁)k₁²w₁   2/π V(k₂,k₂)k₂²w₂ + k₂²/(2μ)   …   … ⎟
⎜   ⋱                ⋱                ⋱                ⋱ ⎟
⎝ …                …                …   k_N²/(2μ) + 2/π V(k_N,k_N)k_N²w_N ⎠ × ⎛ ψₙ(k₁) ⎞ = Eₙ ⎛ ψₙ(k₁) ⎞
                                   ⎜ ψₙ(k₂) ⎟           ⎜ ψₙ(k₂) ⎟
                                   ⎜  ⋮    ⎟           ⎜  ⋮    ⎟
                                   ⎝ ψₙ(k_N)⎠           ⎝ ψₙ(k_N)⎠ .  (26.10)
```

Equation 26.9 is the matrix representation of the Schrödinger equation (26.3). The wave function ψₙ(k) on the grid is the N × 1 vector

```
[ψₙ(kᵢ)] = ⎛ ψₙ(k₁) ⎞
           ⎜ ψₙ(k₂) ⎟
           ⎜  ⋮    ⎟
           ⎝ ψₙ(k_N)⎠ .  (26.11)
```

The astute reader may be questioning the possibility of solving N equations for (N + 1) unknowns, ψₙ(kᵢ), and Eₙ. Only sometimes, and only for certain values of Eₙ (eigenvalues), will the computer be able to find solutions. To see how this arises, we try to apply the matrix inversion technique (which we will use successfully for scattering in Section 26.3). We rewrite (26.9) as

```
[H − Eₙ I][ψₙ] = [0]  (26.12)
```

and multiply both sides by the inverse of [H − Eₙ I] to obtain the formal solution

```
[ψₙ] = [H − Eₙ I]⁻¹[0] .  (26.13)
```

This equation tells us that (1) if the inverse exists, then we have the trivial solution ψₙ ≡ 0, which is not revealing, and (2) for a nontrivial solution to exist, our assumption that the inverse exists must be incorrect. Yet we know from the theory of linear equations that the inverse fails to exist when the determinant vanishes:

```
det[H − Eₙ I] = 0  (bound-state condition) .  (26.14)
```

Equation 26.14 is the N + 1th equation needed to find unique solutions to the eigenvalue problem. Although, there is no guarantee that solutions of (26.14) can always be found, if they are found they are the desired eigenvalues of (26.9).
