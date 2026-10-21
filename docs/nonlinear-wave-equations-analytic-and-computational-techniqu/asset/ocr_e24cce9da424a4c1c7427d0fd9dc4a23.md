# 3.2. Computation of the Jacobian.

To compute the k-th column of the Jacobian J = ∇_c r, which is needed by the Levenberg-Marquardt method, we solve the linearized equations along with the nonlinear ones:

```
(3.10) ∂/∂t (q \dot{q}) = ( F(q) \ DF(q) \dot{q} ),   q(0) = q0 = (η0, φ0), \dot{q}(0) = \dot{q}0 = ∂q0/∂c_k.
```

Here q = (η, φ), \dot{q} = (\dot{η}, \dot{φ}), F(q) is given in (2.1), DF is its derivative (see [49] for explicit formulas), and a dot represents a variational derivative with respect to perturbation of the initial conditions, not a time derivative. To compute ∂r_i/∂c_k for i ≥ 2 and k ≤ n, one simply puts a dot over each Fourier mode on the right-hand side of (3.7) or (3.9), including \hat{η}_j(0) and \hat{φ}_j(0) in (3.9). If k = n + 1, then c_k = T and

```
∂r_{2j}/∂T = Im{ e^{i j θ/2} (1/2) ∂_t \hat{η}_j (T/2) },   ∂(r_{4j} + i r_{4j+1})/∂T = √2 [∂_t \hat{φ}_j (T)]
```

in (3.7) and (3.9), respectively, with similar formulas for ∂(r_{4j-2} + i r_{4j-1})/∂T and ∂r_{2j+1}/∂T. The three possibilities for r1 are handled as follows:

+   case 1: ∂r1/∂c_k = \dot{E} = 1/(2π) ∫0^{2π} [\dot{η} η_t - η \dot{φ}_t]_{t=0} dx,   (k ≤ n),   ∂r1/∂c_{n+1} = 0,
+   case 2: ∂r1/∂c_k = \hat{η}_1(0) = δ_{k,1},   (k ≤ n + 1),
+   case 3: ∂r1/∂c_k = η(0,0) = 2δ_{k,odd},   (k ≤ n),   ∂r1/∂c_{n+1} = 0,

where δ_{k,j} and δ_{k,odd} equal 1 if k = j or k is odd, respectively, and equal zero otherwise. The vectors \dot{q} in (3.10) are computed in batches, each initialized with a different initial perturbation, to consolidate the work in computing the Dirichlet-Neumann operator during each timestep. See [48,49] for details.

# 4. Numerical results

As mentioned in the introduction, our idea is to use collisions of unidirectional Stokes (i.e. traveling) waves as starting guesses to find time-periodic and relative periodic solutions of the Euler equations. We begin by computing traveling waves of varying wave height and record their periods. This is easily done in the framework of §3. We set θ = π/64 (or any other small number) and minimize \tilde{f} in (3.8). The resulting “period” T will give the wave speed via c = θ/T. Below we report T = 2πc, i.e. T is rescaled as if θ were 2π. We control the amplitude by specifying \hat{η}_1(0), which is the second option listed in §3 for defining the first component r1 of the residual. A more conventional approach for computing traveling waves is to substitute η(x - ct), φ(x - ct) into (2.1) and solve the resulting stationary problem (or an equivalent integral equation) by Newton’s method [11,12,37]. Note that the wave speed c here is unrelated to the vector c of unknowns in (3.4).

With traveling waves in hand, out next goal is to collide two of them and search for a nearby time-periodic solution, with θ = 0. As shown in Figure 1, varying \hat{η}_1(0) from 0 to 7.4×10^{-4} causes the period of a Stokes wave with wavelength λ = 2π and mean fluid depth h = 0.05 to decrease from T_O = 28.1110 to T_A = 22.9739, and the wave height (vertical crest-to-trough distance) to increase from 0 to 0.02892. Solution C is the closest among the Stokes waves we computed to satisfying 5T_C = 6T_A, where p = 5 is the smallest integer satisfying (p+1)/p T_A < T_O. We then combine