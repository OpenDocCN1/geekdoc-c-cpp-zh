
away their energy. We solve (24.57) in a finite region of 2D space and for positive times:

-x₀ < x < x₀ ,   -y₀ < y < y₀ ,   t ≥ 0 .  (24.58)

We take x₀ = y₀ = 7 and impose the boundary conditions that the derivative of the displacement vanishes at the ends of the region:

∂u/∂x(-x₀, y, t) = ∂u/∂x(x₀, y, t) = ∂u/∂y(x, -y₀, t) = ∂u/∂y(x, y₀, t) = 0 .  (24.59)

We also impose the initial condition that at time t = 0 the waveform is that of a pulse (Figure 24.6) with its surface at rest:

u(x, y, t = 0) = 4 tan⁻¹(e^{3-√(x²+y²)}),   ∂u/∂t(x, y, t = 0) = 0 .  (24.60)

We discretize the equation first by looking for solutions on a space–time lattice:

x = mΔx ,   y = lΔx ,   t = nΔt ,  (24.61)

uₘ,ₗⁿ  def = u(mΔx, lΔx, nΔt) .  (24.62)

Next we replace the derivatives in (24.57) by their finite-difference approximations:

uₘ,ₗⁿ⁺¹ ≈ -uₘ,ₗⁿ⁻¹ + 2[1 - 2(Δt/Δx)²]uₘ,ₗⁿ + (Δt/Δx)²(uₘ₊₁,ₗⁿ + uₘ₋₁,ₗⁿ + uₘ,ₗ₊₁ⁿ + uₘ,ₗ₋₁ⁿ) - Δt² sin[1/4(uₘ₊₁,ₗⁿ + uₘ₋₁,ₗⁿ + uₘ,ₗ₊₁ⁿ + uₘ,ₗ₋₁ⁿ)] .  (24.63)

To make the algorithm simpler and establish stability, if we make the time and space steps proportional, Δt = Δx/√2. This leads to all of the uₘ,ₗⁿ terms dropping out:

uₘ,ₗ² ≈ ½(uₘ₊₁,ₗ¹ + uₘ₋₁,ₗ¹ + uₘ,ₗ₊₁¹ + uₘ,ₗ₋₁¹) - (Δt²/2) sin[1/4(uₘ₊₁,ₗ¹ + uₘ₋₁,ₗ¹ + uₘ,ₗ₊₁¹ + uₘ,ₗ₋₁¹)] .  (24.64)

Likewise, the discrete form of vanishing initial velocity (24.60) becomes

∂u(x, y, 0)/∂t = 0  ⇒  uₘ,ₗ² = uₘ,ₗ⁰ .  (24.65)

This will be useful in setting the initial conditions. The lattice points on the edges and corners cannot be obtained from these relations, but must be obtained by

applying the boundary conditions (24.59):

```
∂u/∂z (x₀, y, t) = [u(x + Δx, y, t) - u(x, y, t)] / Δx = 0    (24.66)
⇒ u₁,ₗⁿ = u₂,ₗⁿ .    (24.67)
```

Similarly, the other derivatives in (24.59) give

```
uₙₘₐₓ,ₗⁿ = uₙₘₐₓ₋₁,ₗⁿ ,   uₘ,₂ⁿ = uₘ,₁ⁿ ,   uₘ,ₙₘₐₓⁿ = uₘ,ₙₘₐₓ₋₁ⁿ ,    (24.68)
```

where Nₘₐₓ is the number of grid points used for one space dimension.

![](img/bccda43674e4a93dee81c749eba8d2f7_596_0.png)

Figure 24.6 A circular ring soliton at times 8, 20, 40, 60, 80, and 120. This has been proposed as a model for an elementary particle.

## 24.6.5

### 2D Soliton Implementation

- 1. Define an array u[Nₘₐₓ, Nₘₐₓ, 3] with Nₘₐₓ = 201 for the space slots and the 3 for the time slots.
- 2. The solution (24.60) for the initial time t = 0 is placed in u[m, l, 1].
- 3. The solution for the second time Δt is placed in u(m, l, 2), and the solution for the next time, 2Δt, is placed in u[m, l, 3].
- 4. Assign the constants, Δx = Δy = 7/100, Δt = Δx / √2, y₀ = x₀ = 7.
- 5. Start off at t = 0 with the initial conditions and impose the boundary conditions to this initial solution. This is the solution for the first time step, defined over the entire 201 × 201 grid.
- 6. For the second time step, increase time by Δt and use (24.64) for all points in the plane. Do not include the edge points.
- 7. At the edges, for i = 1, 2, ..., 200, set

      u[i, 1, 2] = u[i, 2, 2] ,      u[i, N_max, 2] = u[i, N_max−1, 2]
      u[1, i, 2] = u[2, i, 2] ,      u[N_max, i, 2] = u[N_max−1, i, 2] .
- 8. To find values for the four points in the corners for the second time step, again use initial condition (24.64):

      u[1, 1, 2] = u[2, 1, 2] ,      u[N_max, N_max, 2] = u[N_max−1, N_max−1, 2]
      u[1, 1, N_max] = u[2, N_max, 2] ,      u[N_max, 1, 2] = u[N_max−1, 1, 2] .
- 9. For the third time step (the future), use (24.64).
- 10. Continue the propagation forward in time, reassigning the future to the present, and so forth. In this way, we need to store the solutions for only three time steps.

## 24.6.6

### SGE Soliton Visualization

We see in Figure 24.6 the time evolution of a circular ring soliton that results for the stated initial conditions. We note that the ring at first shrinks in size, then expands, and then shrinks back into another (but not identical) ring soliton. A small amount of the particle does radiate away, and in the last frame we can notice some interference between the radiation and the boundary conditions. An animation of this sequence can be found online.

## 25

Fluid Dynamics

> We have already introduced some fluid dynamics in the previous chapter’s discussion of shallow-water solitons. This chapter confronts the more general equations of computational fluid dynamics (CFD) and their solutions.¹ The mathematical description of the motion of fluids, although not a new subject, remains a challenging one. Equations are complicated and nonlinear, there are many degrees of freedom, the nonlinearities may lead to instabilities, analytic solutions are rare, and the boundary conditions for realistic geometries (like airplanes) are not intuitive. These difficulties may explain why fluid dynamics is often absent from undergraduate and even graduate physics curricula. Nonetheless, as an essential element of the physical world that also has tremendous practical importance, we encourage its study. We recommend Fetter and Walecka (1980); Landau and Lifshitz (1987) for those interested in the derivations, and Shaw (1992) for more details about the computations.

### 25.1

River Hydrodynamics

**Problem**  In order to give migrating salmon a place to rest during their arduous upstream journey, the Oregon Department of Environment is placing objects in several deep, wide, fast-flowing streams. One such object is a long beam of rectangular cross section (Figure 25.1a), and another is a set of plates (Figure 19.4b). The objects are to be placed far enough below the water’s surface so as not to disturb the surface flow, and far enough from the bottom of the stream so as not to disturb the flow there either. Your *problem* is to determine the spatial dependence of the stream’s velocity when the objects are in place, and, specifically, whether the wake of the object will be large enough to provide a resting place for a meter-long salmon.

![](img/bccda43674e4a93dee81c749eba8d2f7_599_0.png)

**Figure 25.1** Side view of the flow of a stream around a submerged beam (a) and around two parallel plates (b). Both beam and plates have length *L* along the direction of flow. The flow is seen to be symmetric about the center-line and to be unaffected at the bottom and at the surface by the submerged object.

### 25.2

### Navier–Stokes Equation (Theory)

As with our study of shallow-water waves, we assume that water is *incompressible* and thus that its density ρ is constant. We also simplify the theory by looking only at steady-state situations, that is, ones in which the velocity is not a function of time. However, to understand how water flows around objects, like our beam, it is essential to include the complication of frictional forces (*viscosity*).

For the sake of completeness, we repeat here the first equation of hydrodynamics, the continuity equation (24.2):

$$\frac{\partial \rho(\mathbf{x},t)}{\partial t}+\nabla\cdot\mathbf{j}=0,\qquad \mathbf{j}\mathrel{\mathop{=}^{\mathrm{def}}}\rho\mathbf{v}(\mathbf{x},t).$$ \tag{25.1}

Before proceeding to the second equation, we introduce a special time derivative, the *hydrodynamic derivative* $D\mathbf{v}/Dt$, which is appropriate for a quantity contained in a moving fluid (Fetter and Walecka, 1980):

$$\frac{D\mathbf{v}}{Dt}\mathrel{\mathop{=}^{\mathrm{def}}}(\mathbf{v}\cdot\nabla)\mathbf{v}+\frac{\partial\mathbf{v}}{\partial t}.$$ \tag{25.2}

This derivative gives the rate of change, as viewed from a stationary frame, of the velocity of material in *an element of flowing fluid* and so incorporates changes as a result of the motion of the fluid (first term) as well as any explicit time dependence of the velocity. Of particular interest is that $D\mathbf{v}/Dt$ is of second order in the velocity, and so its occurrence introduces nonlinearities into the theory. You may think of these nonlinearities as related to the fictitious (inertial) forces that occur when we describe the motion in the fluid’s rest frame (an accelerating frame to us).
