depth of the undisturbed fluid, and subscripts denote partial derivatives. Since we are interested in periodic waves, we consider periodic boundary conditions in the horizontal direction. We note that the above equations represent a free-boundary value problem for Laplace’s equation, i.e. both η and φ are unknowns. These equations readily generalize to three-dimensional fluids (with two-dimensional surfaces); however, in the present work, we limit ourselves to one-dimensional surfaces.

The water-wave equations may be reformulated in terms of only the surface variables η(x, t) and q = φ(x, η, t) as [11,33]

```
∂η/∂t = G(η)q,
∂q/∂t = -gη - q_x²/2 + (G(η)q + η_x q_x)² / [2(1 + η_x²)],
```

where G(η) represents the Dirichlet-Neumann operator (DNO) defined as

```
G(η)q = φ_y(x, η) - η_x φ_x(x, η),
```

where φ is the solution to the following boundary-value problem

```
φ_xx + φ_yy = 0,      -h < y < η,
φ(x, y) = q(x),      y = η,
φ_y = 0,             y = -h.
```

Thus G(η) maps the given Dirichlet data q to the associated Neumann data at the free surface. Consequently, to evolve the surface variables in time using some numerical scheme, we require the solution to Laplace’s equation at every time step. Numerically solving Laplace’s equation at every time step is expensive, particularly in three dimensions.

A characterization of G(η) that avoids the expensive numerical solution of Laplace’s equation is appealing. In the current work we discuss four such characterizations developed in the context of water waves. These four methods are the operator expansion method of Craig & Sulem (CS) [11], the transformed field expansion method (TFE) of Bruno & Reitich [7] and Nicholls & Reitich [23,24], the nonlocal implicit formulation of the DNO given by Ablowitz, Fokas & Musslimani (AFM) [1], and a dual version to the AFM method, derived by Ablowitz & Hal [2], which we denote by AFM*. Each of these methods has had remarkable theoretical utility in deriving reduced models for water waves in various physical regimes [10], in deriving conserved quantities [1], and also in providing the theoretical framework to pose some inverse problems [25,28]. Additionally, each of these methods readily generalizes to the case of both varying bottom boundaries and three dimensional fluids.

Of course, many traditional methods to numerically solve Laplace’s equation exist, including the boundary integral method, conformal mapping techniques, and the finite element method. In the present work we chose to compare the CS and TFE operator expansions and the AFM/AFM* nonlocal formulations with the boundary integral method. We do not consider conformal mapping [14], as it does not extend to three dimensional problems, nor traditional finite elements [26], as the trade-off between high-order elements and sparsity of the stiffness matrix makes them expensive when high accuracy is desired. Though it is not usually described in this way, we regard the TFE method as a spectrally accurate variant of the finite element method. The boundary integral method is particularly efficient in two