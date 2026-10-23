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

# 31.2 The Weak Formulation

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