
## Chapter 31
## Application in the Navier–Stokes Equations

In this chapter, we use the present object-oriented framework to form a numerical solver for the Navier–Stokes system of nonlinear PDEs in an adaptive mesh of tetrahedra. Linear finite elements are used to discretize the velocity functions, and constant finite elements are used to discretize the pressure function. Newton’s iteration is then used to linearize the nonlinear term. An inner GMRES iteration is used to solve the linear system in each Newton iteration. Unfortunately, a point Gauss–Seidel or Jacobi preconditioner cannot be used within GMRES due to the zero main-diagonal elements in the lower-right block in the coefficient matrix. Instead, we use the Kaczmarz preconditioner or a multigrid preconditioner that uses Kaczmarz relaxation.

### 31.1 The Strong Formulation

The Navier–Stokes system of nonlinear PDEs has already been discussed briefly in Section 21.9 above in the context of two-dimensional problems. In a three-dimensional domain of the form

Ω ⊂ (−∞,∞)³

the system still has the same strong formulation:

⎛ −εΔ + (∇v)ᵗ   ∇ ⎞ ⎛ v ⎞ = ⎛ f ⎞
⎝   −∇·        0 ⎠ ⎝ p ⎠   ⎝ g ⎠

where ε is a small parameter and, for (x, y, z) ∈ Ω,

v ≡ (v₁(x, y, z), v₂(x, y, z), v₃(x, y, z))ᵗ

is the unknown velocity (real) vector function,

p ≡ p(x, y, z)

is the unknown (real) scalar pressure function, and

f ≡ (f₁(x, y, z), f₂(x, y, z), f₃(x, y, z))ᵗ

and

g ≡ g(x, y, z)

are some given real functions. More explicitly, the system can also be written as

−εΔv + (∇v)ᵗv + ∇p = f
−∇·v = g.

Assume also that ∂Ω, the boundary of Ω, can be written as the union of two disjoint subsets:

∂Ω = Γ_D ∪ Γ_N.

with Dirichlet boundary conditions imposed on Γ_D to specify v there explicitly and mixed boundary conditions of the form

−p n̂ + εv_n + v = −p n̂ + ε(∇v)ᵗ n̂ + v = γ

imposed on Γ_N, where γ is a given real vector function in Γ_N and

n̂ ≡ (n̂₁(x,y,z), n̂₂(x,y,z), n̂₃(x,y,z))ᵗ

is the outer normal vector at (x, y, z) ∈ Γ_N. With these boundary conditions, the system has indeed a well-posed weak formulation with a unique solution.

### 31.2 The Weak Formulation

Recall that, for a 3 × 3 matrix M̃, the trace

trace(M̃) ≡ M̃₁,₁ + M̃₂,₂ + M̃₃,₃

is the sum of the main-diagonal elements in M̃. Furthermore, let

w ≡ (w₁(x,y,z), w₂(x,y,z), w₃(x,y,z))ᵗ

be some real vector function in Ω that vanishes in Γ_D. Let us now take the inner product of the three-dimensional vector w with the left-hand side in the first equation in the above strong formulation, and integrate over Ω. Using also Green’s divergence formula, the fact that w vanishes in Γ_D, and the mixed boundary conditions in Γ_N, we have

−ε ∭_Ω (Δv)·w dxdydz + ∭_Ω ((∇v)ᵗv)·w dxdydz + ∭_Ω (∇p)·w dxdydz

= ε ( ∭_Ω trace((∇v)ᵗ(∇w)) dxdydz − ∭_Ω ∇·((∇v)w) dxdydz )

+ ∭_Ω vᵗ(∇v)ᵗ w dxdydz − ∭_Ω p(∇·w) dxdydz + ∭_Ω ∇·(p w) dxdydz

= ε ( ∭_Ω trace((∇v)ᵗ(∇w)) dxdydz − ∬_{Γ_N} n̂ᵗ(∇v)w dΓ_N )

+ ∭_Ω vᵗ(∇v)w dxdydz − ∭_Ω p(∇·w) dxdydz + ∬_{Γ_N} p w·n̂ dΓ_N

= ε ∭_Ω trace((∇v)ᵗ(∇w)) dxdydz + ∭_Ω vᵗ(∇v)w dxdydz

− ∭_Ω p(∇·w) dxdydz + ∬_{Γ_N} v·w dΓ_N − ∬_{Γ_N} γ·w dΓ_N.

Let us now use the above to integrate the entire first equation in the strong formulation in Section 31.1 over Ω:

ε ∬_Ω trace((∇v)ᵗ (∇w)) dx dy dz + ∬_Ω vᵗ (∇v) w dx dy dz
- ∭_Ω p (∇·w) dx dy dz + ∫_Γ_N v·w dΓ_N
- ∫_Γ_N γ·w dΓ_N
= -ε ∬_Ω (Δv)·w dx dy dz + ∬_Ω ((∇v)ᵗ · w) dx dy dz
+ ∭_Ω (∇p)·w dx dy dz
= ∭_Ω f·w dx dy dz

or

ε ∬_Ω trace((∇v)ᵗ (∇w)) dx dy dz + ∬_Ω vᵗ (∇v) w dx dy dz
- ∭_Ω p (∇·w) dx dy dz + ∫_Γ_N v·w dΓ_N
= ∭_Ω f·w dx dy dz + ∫_Γ_N γ·w dΓ_N

Note that this equation can be written equivalently as a system of three such equations, the first of which uses

- w = (w₁(x,y,z),0,0)ᵗ
- w = (0, w₂(x,y,z),0)ᵗ
- w = (0,0, w₃(x,y,z))ᵗ

Indeed, the sum of these three equations is the original equation.

Finally, let q ≡ q(x,y,z) be some real scalar function in Ω. Let us multiply the second equation in the strong formulation in Section 31.1 by q and integrate over Ω:

- ∬_Ω q ∇·v dx dy dz = ∬_Ω q g dx dy dz

These four equations in the four unknown functions v₁, v₂, v₃, and p represent the original Navier–Stokes system in its well-posed weak form. This form serves as the basis for the finite-element discretization below.

### 31.3 The Finite-Element Discretization

The discrete finite-element algebraic system is obtained from the above weak formulation by approximating the original domain Ω by a mesh of tetrahedra M and assuming that v₁, v₂, v₃, w₁, w₂, and w₃ are continuous in M and piecewise linear (linear in each particular tetrahedron t ⊂ M) and that p and q are piecewise constant (constant in each particular tetrahedron t ⊂ M). More specifically, v₁, v₂, and v₃ can be written as a sum of nodal basis functions of the form ψⱼ (corresponding to nodes j ∈ M \ Γ_D), each of which is multiplied by some unknown scalar coefficient cⱼ^(k) (1 ≤ k ≤ 3):

v₁ ≡ Σ_{j ∈ M \ Γ_D} cⱼ^(1) ψⱼ,

v₂ ≡ Σ_{j ∈ M \ Γ_D} cⱼ^(2) ψⱼ,

v₃ ≡ Σ_{j ∈ M \ Γ_D} cⱼ^(3) ψⱼ.

Furthermore, p can be written as a sum of elemental basis functions of the form βₜ with the value 1 in some particular tetrahedron t ⊂ M and 0 elsewhere:

βₜ(x, y, z) ≡ { 1 if (x, y, z) ∈ t, 0 if (x, y, z) ∈ M \ t }

each of which is multiplied by some unknown scalar coefficient dₜ:

p ≡ Σ_{t ⊂ M} dₜ βₜ.

The discrete finite-element system is thus a system of algebraic equations in the unknown coefficients cⱼ^(k) (j ∈ M \ Γ_D, 1 ≤ k ≤ 3) and dₜ (t ⊂ M). Each equation in this system is obtained by picking w₁, w₂, or w₃ to be some nodal basis function of the form ψₗ for some node l ∈ M \ Γ_D or by picking q to be some elemental basis function of the form βₛ for some tetrahedron s ⊂ M, whereas the other functions that are not picked vanish. To make this more precise, let us define the three-dimensional vector function with one component that is a nodal basis function and two components that vanish:

ψⱼ^(1) ≡ (ψⱼ, 0, 0)ᵗ,
ψⱼ^(2) ≡ (0, ψⱼ, 0)ᵗ,
ψⱼ^(3) ≡ (0, 0, ψⱼ)ᵗ

(j ∈ M \ Γ_D). With this notation, an algebraic equation in the first three block-rows in the discrete (stiffness) system is obtained by picking

w ≡ ψₗ^(m)

for some node l ∈ M \ Γ_D and some integer 1 ≤ m ≤ 3. Furthermore, an algebraic equation in the fourth (and lower) block-row in the system is obtained by picking

q ≡ βₛ

for some tetrahedron s ⊂ M. This way, the number of equations is indeed the same as the number of unknown coefficients, that is, three times the total number of nodes that are away from Γ_D plus the total number of tetrahedra in the mesh.

### 31.4 Linearization

In each Newton iteration, the nonlinear term

∭_Ω v' (∇v) w dx dy dz

must be linearized at the current approximate solution v. For this purpose, the above representation of v is particularly helpful. Indeed, to have the required Jacobian, we have to take the partial derivative with respect to some unknown coefficient c_j^(k) (j ∈ M \ Γ_D, 1 ≤ k ≤ 3). Fortunately, as in Section 27.5 above, this can be done under the integral sign. Furthermore, this can also be done under the gradient sign:

∂/∂c_j^(k) ∭_Ω v' (∇v) w dx dy dz = ∭_Ω ∂/∂c_j^(k) (v' (∇v)) w dx dy dz = ∭_Ω (∂/∂c_j^(k) v') (∇v) w dx dy dz + ∭_Ω v' (∂/∂c_j^(k) (∇v)) w dx dy dz = ∭_Ω (ψ_j^(k))' (∇v) w dx dy dz + ∭_Ω v' (∇ψ_j^(k)) w dx dy dz.

For instance, by picking

w ≡ ψ_l^(m)

(for some node l ∈ M \ Γ_D and some integer 1 ≤ m ≤ 3) as at the end of Section 31.3 above, the above linearized term contributes to the ((l,m),(j,k))th element in the stiffness matrix the amount

∭_Ω (ψ_j^(k))' (∇v) ψ_l^(m) dx dy dz + ∭_Ω v' (∇ψ_j^(k)) ψ_l^(m) dx dy dz = ∭_Ω (∇v)_{k,m} ψ_j ψ_l dx dy dz + ∭_Ω (k == m) v' ∇ψ_j ψ_l dx dy dz = Σ_{t∈M} (∇v)_{k,m} ∭_t ψ_j ψ_l dx dy dz + (k == m) ∇' ψ_j ∭_t v ψ_l dx dy dz.

where

(k == m) ≡ { 1 if k = m, 0 if k ≠ m. }

### 31.5 The Modified Multigrid Version

In each Newton iteration, the linear system obtained from calculating the above Jacobian at the current approximate solution u is solved by an inner GMRES iteration. Unfortunately, this inner iteration may converge rather slowly, unless a good preconditioner is used.

Because the lower-right block in the stiffness matrix vanishes, point Gauss-Seidel or Jacobi preconditioners cannot be used, due to forbidden division by zero. Instead, one may use the more stable Kaczmarz preconditioner (Section 17.6).

Unfortunately, even with the Kaczmarz preconditioner, the inner GMRES iteration may still converge rather slowly. This is why suitable multigrid preconditioners should be considered, with Kaczmarz pre- and postrelaxation.

An attractive approach may be the modified multigrid algorithm, designed specifically for systems of PDEs in Section 20.9. To define the prolongation operator P in this multigrid version, the coefficient matrix A must be written in a block form, with blocks corresponding to the different unknown functions in the original system of PDEs. This way, the prolongation operator P in Algorithm 17.3 can be defined not from the original matrix A but rather from its block-diagonal part, in which the zero lower-right block has been replaced by the nonzero lower-right block of A' A (with the signs of the off-diagonal elements reversed):

where A₁,₁ corresponds to the first unknown velocity function u₁ (in its discrete piecewise-linear form), A₂,₂ corresponds to u₂, A₃,₃ corresponds to u₃, and (A' A)₄,₄ corresponds to the unknown pressure function p (in its discrete piecewise-constant form).

Note that, in the above, the order of A₁,₁, A₂,₂, and A₃,₃ is the same as the number of nodes in the mesh, whereas the order of (A' A)₄,₄ is the same as the number of tetrahedra in the mesh. In the recursive call to design the next prolongation operator based on the coarse-level matrix Q ≡ R A P, on the other hand, the orders of the four blocks are the same as the numbers of the coarse unknowns in the four original blocks, respectively.

Unfortunately, the above multigrid algorithm may work rather well only for nearly SPD systems with ε as large as 100, but not for highly nonsymmetric or indefinite systems, such as systems with ε as small as 0.01, which are much more common in practical applications. It is therefore necessary to design the multigrid algorithm not only algebraically in terms of the stiffness matrix A assembled in the current fine mesh, but also geometrically, using the original PDE and the original domain in which it is defined.

### 31.6 Towards Geometric Multigrid Versions

As discussed above, algebraic multigrid versions as in Sections 17.8, 17.9, and 20.9 don't work well for highly nonsymmetric or indefinite problems, such as problems with ε ≤ 1. In fact, even the trick in Section 17.12 doesn't help. One should no doubt use some more information that is available about the original PDE and the original domain to design the multigrid algorithm not only algebraically but also geometrically.

More to the point, the coarse mesh in algebraic multigrid versions is just a subset of unknowns that are picked from the original set of unknowns using the elements in A. This
