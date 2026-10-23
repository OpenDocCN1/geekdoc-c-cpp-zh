vector functions E and B (with square-integrable curl and divergence in Ω) so that

1/c ∫_Ω E_t · Ē dΩ − ∫_Ω (∇ × B) · Ē dΩ = −4π/c ∫_Ω J · Ē dΩ
∫_Ω (∇ × E) · B̄ dΩ + 1/c ∫_Ω B_t · B̄ dΩ = 0
∫_{Γ_k} L_k(E,B) p_k dΓ_k = 0   (1 ≤ k ≤ 5)
∫_Ω (∇ · E) p_6 dΩ = 4π ∫_Ω ρ p_6 dΩ

for all vector functions Ē and B̃ that satisfy the homogeneous constraints L_k(Ē, B̃) = 0 weakly in Γ_k (1 ≤ k ≤ 6) and all scalar functions p_k that are square-integrable in Γ_k (1 ≤ k ≤ 6). (In the setting in [21], p_5 and p_6 are no longer arbitrary, but rather dependent on B̃ and Ē: p_5 is chosen to be the complex conjugate of ∇ · B̃, and p_6 is chosen to be the complex conjugate of ∇ · Ē.)

Note that the first two equations in this system (the time-dependent curl equations) can be added to each other, yielding an equivalent system that holds for every pair of the form (Ē, B̃) rather than all individual fields Ē and B̃. Indeed, the original curl equations can be obtained from their sum by considering pairs of the form (Ē,0) and (0, B̃). The sum form, however, is particularly useful, because its left-hand side defines the bilinear form a((E,B),(Ē,B̃)), used in the finite-element discretization below. (In the setting in [21] mentioned above, in which p_5 ≡ ∇ · B̃ and p_6 ≡ ∇ · Ē, the two final constraint equations are added to this sum as well, so the bilinear form a contains integrals of ∇ · B ∇ · B̃ and ∇ · E ∇ · Ē as well.)

Because it is rather difficult to design fields Ē and B̃ that satisfy the homogeneous constraints, it makes sense to resort to the original Lagrange-multiplier form introduced in Sections 29.2–29.4 above, in which no homogeneous constraints are used. This approach is indeed used in the discretization below.

# 29.10 The Finite-Element Discretization

Assume now that the three-dimensional domain Ω is approximated by a mesh of tetrahedra M as in Chapter 26. Then the unknown electric field E can be approximated by three scalar functions that are continuous in the mesh and linear in each particular tetrahedron. The number of degrees of freedom in each such function is the same as the number of nodes in the mesh. In fact, each degree of freedom is associated with a piecewise linear nodal basis function with the value 1 at a particular node and 0 at all the other nodes. Thus, each of the three unknown functions in E is approximated by a linear combination of these nodal basis functions, with scalar coefficients that serve as unknowns in the discrete system of algebraic equations.

The fields B, Ē, and B̃ can be approximated in the same way. The scalar functions p_5 and p_6, on the other hand, can be approximated by functions that are constant in each individual tetrahedron in the mesh. The number of degrees of freedom in p_5 and p_6 is, thus, the same as the number of tetrahedra in the entire mesh. In fact, each degree of freedom is