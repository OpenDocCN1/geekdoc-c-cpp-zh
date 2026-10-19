# 19.4
Finite-Difference Algorithm

To solve our 2D PDE numerically, we divide space up into a lattice (Figure 19.3) and solve for U at each site on the lattice. Because we will express derivatives in terms of the finite differences in the values of U at the lattice sites, this is called a finite-difference method. A numerically more efficient method, but with more complicated set up, is the finite-element method (FEM) that solves the PDE for small geometric elements and then matches the solution over the elements. We discuss FEM in Chapter 23.

To derive the finite-difference algorithm for the numeric solution of (19.5), we follow the same path taken in Section 5.1 to derive the forward-difference algorithm for differentiation. We start by adding the two Taylor expansions of the potential to the right and left of (x, y) and the two for above and below (x, y):

U(x + Δx, y) = U(x, y) + ∂U/∂x Δx + 1/2 ∂²U/∂x² (Δx)² + ⋯ , (19.20)

U(x − Δx, y) = U(x, y) − ∂U/∂x Δx + 1/2 ∂²U/∂x² (Δx)² − ⋯ , (19.21)

U(x, y + Δy) = U(x, y) + ∂U/∂y Δy + 1/2 ∂²U/∂y² (Δy)² + ⋯ , (19.22)

U(x, y − Δy) = U(x, y) − ∂U/∂y Δy + 1/2 ∂²U/∂y² (Δy)² − ⋯ . (19.23)

![](bbox=[0.12, 0.55, 0.72, 0.82])

Figure 19.3 The algorithm for Laplace's equation in which the potential at the point (x, y) = (i, j)Δ equals the average of the potential values at the four nearest-neighbor points. The nodes with white centers correspond to fixed values of the potential along the boundaries.