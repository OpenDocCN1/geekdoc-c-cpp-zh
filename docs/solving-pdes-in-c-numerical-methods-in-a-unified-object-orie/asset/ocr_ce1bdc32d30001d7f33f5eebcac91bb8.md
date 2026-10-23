gradient of φ_i (the two-dimensional vector whose components are the x- and y-derivatives of φ_i) is given by

∇φ_i = ∇(φ_{1,0} ∘ M_e^{-1}) = ∇(φ_{1,0}) S_e^{-1},

where the gradient of φ_i, ∇(φ_i), is evaluated at a point (x, y) ∈ e, and the gradient of φ_{1,0} is evaluated at its inverse image M_e^{-1}((x, y)) ∈ r.

Further simplification is obtained by recalling that φ_{1,0} = x, so its gradient is actually the constant vector (1, 0). With this observation, the gradient of φ_i is just the first row in S_e^{-1}:

∇φ_i = ((S_e^{-1})_{1,1}, (S_e^{-1})_{1,2}).

Similarly, for φ_j we have

∇φ_j = ∇(φ_{0,1}) S_e^{-1}.

where the gradient of φ_j is evaluated at a point (x, y) ∈ e, and the gradient of φ_{0,1} is evaluated at its inverse image M_e^{-1}((x, y)) ∈ r.

Again, one can simplify the above by recalling that φ_{0,1} = y, so its gradient is just the constant vector (0, 1). With this observation, the gradient of φ_j is just the second row in S_e^{-1}:

∇φ_j = ((S_e^{-1})_{2,1}, (S_e^{-1})_{2,2}).

We are now ready to calculate the elements in the stiffness matrix A. For simplicity, we assume that K ≡ 0 in the PDE, so only the second-derivative terms remain in it. Let us use the notation

diag(P, Q) = ( P 0 ; 0 Q ).

Now, A_{i,j} in the stiffness matrix can be written as the sum of contributions from individual triangles:

A_{i,j} = Σ_e ∫_e ∇φ_j diag(P, Q) ∇φ_i dx dy.

Here, the sum goes over all triangles in the mesh. Still, only those triangles that use both i and j as vertices (like the triangle in Figure 12.1) actually contribute to A_{i,j}. It is therefore common to say that A_{i,j} (and, in fact, A) is "assembled" from the nonzero contributions from the individual finite elements.

Using the rule of the integral over a mapped domain, we have that the contribution from e to A_{i,j} is

∫_e ∇φ_j diag(P, Q) ∇φ_i dx dy
= ∫_r ∇φ_{0,1} S_e^{-1} diag(P M_e, Q M_e) S_e^{-t} ∇φ_{1,0} dM_e(x, y)
= ∫_r (0,1) S_e^{-1} diag(P M_e, Q M_e) S_e^{-t} (1; 0) |det(∂M_e(x,y)/∂(x,y))| dx dy
= ∫_r (0,1) S_e^{-1} diag(P M_e, Q M_e) S_e^{-t} (1; 0) |det(S_e)| dx dy.