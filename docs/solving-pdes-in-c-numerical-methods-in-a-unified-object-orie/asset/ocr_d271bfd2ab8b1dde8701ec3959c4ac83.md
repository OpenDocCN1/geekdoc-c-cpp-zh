# 28.15 The Stiffness Matrix

For 0 ≤ i, j < N, the (i, j)th element in the stiffness matrix A^{(s)} is now defined by

A_{i,j}^{(s)} ≡ ∭_M ∇^t φ_j ∇ φ_i dx dy dz = Σ_{t∈M} ∭_t ∇^t φ_j ∇ φ_i dx dy dz = Σ_{t∈M, i,j∼t} ∭_t ∇^t h_{j,t} ∇ h_{i,t} dx dy dz = Σ_{t∈M, i,j∼t} |det(S_t)| ∭_T ∇^t (h_{j,t} ∘ D_t) S_t^{-1} S_t^{-T} ∇ (h_{i,t} ∘ D_t) dx dy dz.

Note that the functions of the form h_{i,t} ∘ D_t used in the above integral are easily available. Indeed, since h_{i,t} is equal to R_{n,t} for some 0 ≤ n < 56, h_{i,t} ∘ D_t is the same as R_{n,t} ∘ D_t. Furthermore, just as R_{n,t} has been produced from the r_{k,t}'s (0 ≤ k < 56), R_{n,t} ∘ D_t can be calculated directly from the r_{k,t} ∘ D_t's, which are nothing but the original basis functions p_k defined in the reference tetrahedron T in Section 28.2. Thus, all the calculations can be carried out in T only: the original calculation of R_{n,t} ∘ D_t as a linear combination of the r_{k,t} ∘ D_t's, the substitution to make it a proper basis function (using the chain rule to calculate the required degrees of freedom of the form R_{n,t}^{(m,t)} in T only), the re-indexation to form h_{i,t} ∘ D_t, and the derivation and integration of the latter to calculate the contribution from t to the stiffness matrix.

This completes the definition of the stiffness matrix A^{(s)}. The boundary term A^{(b)}, the mass matrix A^{(m)}, and the 2N × 2N matrix A^{(n)}(f) (where f is a 2N-dimensional vector grid function) used in the Newton iteration to solve the nonlinear Helmholtz equation can be defined in a similar way. This is left to the exercises.

# 28.16 The Refinement Step in a Nonlinear Equation

In order to produce the finer mesh on which the PDE can be approximated with a yet greater accuracy, the PDE must first be solved on the current (coarse) mesh, to indicate over which edges the discrete (coarse) solution has a large variation (jump). These edges are then refined or divided to produce the next finer mesh. This is the refinement step.

In order to solve the discrete problem on the coarse mesh, an inner Newton iteration should be used. To start this iteration, however, one must have a proper initial guess. Naturally, this initial guess can be prolonged from the discrete solution computed before on the previous coarser mesh.

This prolongation, however, is not trivial. If the multigrid version in Section 17.15 or 17.16 is used, then one may use the prolongation operator available within the multigrid V-cycle. Still, this is a "local" prolongation that gives the prolonged value at a particular fine-grid point in terms of its neighbor coarse-grid points only. The resulting initial guess on the current mesh thus may not be sufficiently close to the required solution, so the inner Newton iteration may fail to converge to it.

A more advanced prolongation operator is introduced in Chapter 27 in [69]. In this operator, the degrees of freedom of the discrete solution computed before on the yet coarser