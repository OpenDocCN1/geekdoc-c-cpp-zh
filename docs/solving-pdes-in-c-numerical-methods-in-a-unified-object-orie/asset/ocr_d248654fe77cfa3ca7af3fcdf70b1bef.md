# 20.10. Numerical Examples

![](bbox=[0.05, 0.12, 0.95, 0.28])

Since this part doesn’t couple unknowns corresponding to u with unknowns corresponding to v, the prolongation operator resulting from it prolongs u-values separately from v-values, preserving continuity in u and v. (A similar approach is introduced in [27] for the rectangular grid.)

The rest of the multigrid algorithm is as before (R = P^t and Q = RAP). This completes the definition of the iterative solver for the individual stiffness systems in the adaptive-refinement algorithm. The entire adaptive-refinement algorithm is displayed schematically in Figure 20.2.

# 20.10 Numerical Examples

Here, we apply the adaptive-refinement algorithm to the above linear elasticity equations with the Poisson ratio ν = 1/3.

The domain Ω is the unit circle: Ω = {(x, y) | x² + y² < 1}.

The portion of the boundary on which Dirichlet boundary conditions are imposed is Γ_D = {(x, y) | x² + y² = 1, x ≤ -0.5}.

The portion of the boundary on which Neumann boundary conditions are imposed is the rest of the boundary: Γ_N = {(x, y) | x² + y² = 1, x > -0.5}

> (Figure 20.3).