![](bbox=[0.25, 0.15, 0.85, 0.55])

Figure 20.3. The boundary segments Γ_D (where Dirichlet boundary conditions are given) and Γ_N (where Neumann boundary conditions are given) in the linear elasticity example.

The Dirichlet boundary conditions are homogeneous in Γ_D:

γ₁ = γ₂ ≡ 0.

The right-hand-side functions are

ℱ = 𝔤 = −0.1 · δ_(1,0),

where the δ-function (centered at (1,0)) is defined by the weak formula

∫_( (x,y)∈Ω ) δ_(1,0) w(x,y) dx dy = w(1,0)

for every smooth function w(x,y) defined in the domain Ω. For this example, the right-hand-side vector f in the stiffness system is, thus,

f_i = { 0.1  if i = 0 or i = N/2,
        0    otherwise. }

The adaptive-refinement algorithm is used with the criterion in Section 20.8 above (with threshold = 0.01). Automatic boundary refinement as in Chapter 14, Section 8, is also used. In each refinement level, the numerical solution is calculated by the PCG iteration in Chapter 17, Section 11. The multigrid algorithm in Chapter 17, Sections 8 and 9, is used as a preconditioner. The multigrid V-cycle uses Gauss–Seidel as the relaxation method ("useILU" = 0 and "gridRatio" = 0.95 in Chapter 17, Section 10). The modification in Section 20.9 is also used. The total cost of a multigrid V-cycle is the same as that of 2.5 symmetric Gauss–Seidel iterations.