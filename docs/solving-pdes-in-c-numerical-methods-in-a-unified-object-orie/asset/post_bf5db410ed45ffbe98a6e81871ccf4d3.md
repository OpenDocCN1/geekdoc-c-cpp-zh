
![](img/1f293b0ceb2de964310ea7f941a1b580_384_0.png)

## Figure 12.10
The next, finer, mesh that better approximates the circular boundary.

each other, so $A_{i,k}$ actually vanishes. Indeed, as calculated in Section 12.7, the contribution from $\triangle(i,k,l)$ is

$$
\frac{\cot(\angle(k,l,i))}{2}
$$

where $\angle(k,l,i)$ is the angle at the vertex $l$ in $\triangle(i,k,l)$. Similarly, the contribution from $\triangle(i,j,k)$ is

$$
\frac{\cot(\angle(i,j,k))}{2}
$$

Since these two angles lie on the same circle, it follows from Euclidean geometry that

$$
\angle(k,l,i) + \angle(i,j,k) = \pi
$$

As a result,

$$
\cot(\angle(k,l,i)) + \cot(\angle(i,j,k)) = \cot(\angle(k,l,i)) + \cot(\pi - \angle(k,l,i)) = \cot(\angle(k,l,i)) - \cot(\angle(k,l,i)) = 0
$$

implying that

$$
A_{i,k} = 0
$$

On the other hand, the matrix element $A_{i,j}$ that couples the adjacent nodes $i$ and $j$ doesn't vanish. Indeed, since the only triangle that contributes to it is $\triangle(i,j,k)$, it follows from Section 12.7 that

$$
A_{i,j} = -\frac{\cot(\angle(j,k,i))}{2} = -\frac{\cot(\pi/N)}{2}
$$

where $N$ is the number of nodes. (In the case in Figure 12.10, $N = 8$; in general, $N = 2^{k+1}$, where $k$ is the number of refinement steps.) In summary, $A$ takes the tridiagonal form

$$
A = \text{tridiag}\left(-\frac{\cot(\pi/N)}{2}, \cot(\pi/N), -\frac{\cot(\pi/N)}{2}\right)
$$

More precisely, here $A$ is not exactly tridiagonal in the usual sense, because it also contains the nonzero elements

$$
A_{0,N-1} = A_{N-1,0} = - \cot(\pi / N) / 2
$$

at its upper-right and bottom-left corners. It is more accurate to say that $A$ is a circulant Toeplitz matrix with three nonzero diagonals.

The stiffness matrix constructed above may also be interpreted as the discretization of a one-dimensional Poisson equation (with periodic boundary conditions) along the circular boundary. Clearly, this is not a good scheme for the two-dimensional Poisson equation in the entire circle.

The reason for this failure is that we have concentrated too much on approximating the boundary well and ignored the interior of the domain. In practice, one must also refine the big triangles (e.g., $\Delta(i,k,l)$) to obtain a good approximation in the interior of the domain. This can be done adaptively as in Chapter 14, Section 2. The algorithm presented there also properly refines the interior of the domain.

The above mesh uses particularly small and narrow triangles near the boundary. These triangles are highly degenerate: they contain very small angles. This may lead to a large discretization error. In Chapter 14, Section 7, we propose a more balanced approach, in which the mesh is refined simultaneously both in the interior of the domain and at its boundary. This mesh is more regular and contains no degenerate triangles.

## 12.10 Exercises

1. Calculate the stiffness matrix for the PDE
   $$-u_{xx}(x,y) - u_{yy}(x,y) + u(x,y) = F(x,y)$$
   on a right-angle-triangle mesh as in Figure 12.3.

2. Calculate the stiffness matrix of the above PDE on a general triangle mesh. In particular, write the contribution from some triangle to some matrix element $A_{i,j}$ (where $i$ and $j$ are indices of vertices in this triangle) in terms of the mapping from the reference triangle to this triangle.

3. Show that the resulting stiffness matrix is SPD.

4. Calculate the stiffness matrix for the PDE
   $$-u_{xx}(x,y) - u_{yy}(x,y) + u_x(x,y) + u_y(x,y) = F(x,y)$$
   on a uniform triangle mesh with right-angle triangles as in Figure 12.3.

5. Show that the above matrix is nonsymmetric.

6. Calculate the stiffness matrix for the above PDE on a general triangle mesh. In particular, write the contribution from some triangle to some matrix element $A_{i,j}$ (where $i$ and $j$ are indices of vertices in this triangle) in terms of the mapping from the reference triangle to this triangle.

7. Show that the above matrix is nonsymmetric.

## 12.11 Advanced Exercises

1. Consider the equation
   $$-(Pu_x)_x-(Qu_y)_y=F$$
   in a domain $\Omega$ in the Cartesian plane, where $P$ and $Q$ are given uniformly positive functions and $F$ is a given function. Write the algorithm that produces the stiffness matrix $A$ on a given finite-element mesh. Consider Dirichlet, Neumann, and mixed boundary conditions of the form
   $$Pu_xn_1+Qu_yn_2+\alpha u=g,$$
   where $\vec n=(n_1,n_2)$ is the outer normal vector, $\alpha$ is a given nonnegative function, and $g$ is a given function on $\partial\Omega$.

2. Show that the bilinear form for the above equation is symmetric. Conclude that $A$ is symmetric as well.

3. Use the coercivity of the corresponding quadratic form to show that $A$ is actually SPD.

4. Consider now the equation
   $$-(Pu_x)_x-(Qu_y)_y+u=F.$$
   Write the algorithm that produces the stiffness matrix $A+K$, where $A$ is as before and $K$ results from the free term $u$ in the PDE.

5. Show that $K$ is SPD.

6. Consider the time-dependent diffusion equation
   $$u_t-(Pu_x)_x-(Qu_y)_y=F.$$
   Write the algorithms that use the above finite-element discretization in explicit, implicit, and semi-implicit time discretization. The solution follows from Chapter 19, Section 4.

7. Write the algebraic representations of your algorithms by replacing the identity matrix $I$ used in Chapter 8, Section 2, by $K$.

8. Define
   $$B\equiv(\Delta t)^{-1}K$$
   for the explicit scheme,
   $$B\equiv(\Delta t)^{-1}K+A$$
   for the implicit scheme, and
   $$B\equiv(\Delta t)^{-1}K+A/2$$
   for the semi-implicit scheme. Show that $B$ is inverted in each time step in the time marching.

9. Show that $B$ above is SPD.

10. Define the energy inner product by
    $$(u, v)_B \equiv (u, Bv) = u^T B v$$
    (where $u$ and $v$ are any two vectors). A matrix $M$ is symmetric with respect to the energy inner product if
    $$(Mu, v)_B = (u, Mv)_B$$
    for every two vectors $u$ and $v$. Show that $B^{-1} A$ and $B^{-1} K$ are symmetric with respect to the energy inner product.

11. Define the energy norm of a matrix $M$ by
    $$\|M\|_B \equiv \max_{v \neq 0} \left( \frac{(M^T v, M^T v)_B}{(v, v)_B} \right)^{1/2}.$$
    It is well known that, if $M^T$ is symmetric with respect to the energy inner product, then the above quantity is also equal to the modulus of the largest eigenvalue of $M^T$. In other words,
    $$\|M\|_B = \max_{v \neq 0} \left| \frac{(v, M^T v)_B}{(v, v)_B} \right|.$$

12. Use the SPD property of $A$ and $K$ to show that, for every nonzero vector $v$, 
    $$\frac{(v, (\Delta t)^{-1} K v)}{(v, ((\Delta t)^{-1} K + A) v)} \text{ and } \frac{(v, ((\Delta t)^{-1} K - A/2) v)}{(v, ((\Delta t)^{-1} K + A/2) v)}$$
    are smaller than 1 in magnitude, and, for sufficiently small $\Delta t$, 
    $$\frac{(v, ((\Delta t)^{-1} K - A) v)}{(v, (\Delta t)^{-1} K v)}$$
    is also smaller than 1 in magnitude.

13. Use the above results to show that the block submatrices $Q_i B_i^{-1}$ in Chapter 8, Section 3, are smaller than 1 in terms of the energy norm induced by $B_i$. Furthermore, use this result to show stability and accuracy in the time marching.

14. Compare your proof with the proof in Chapter 18 in [68].

15. Assume that the function $\alpha$ in the above mixed boundary conditions is constant in each particular boundary edge, e.g., an edge leading from node $i$ to node $j$ that both lie on the boundary segment where the mixed boundary conditions are imposed. Show that the contribution to $A_{i,i}$ from this edge is positive and twice as large as the contribution to $A_{i,j}$.

16. Consider a particular triangle in the mesh, with vertices at nodes $i$, $j$, and $k$. Show that the contribution to $K_{i,i}$ from this triangle is positive and the same as the sum of the contributions to $K_{i,j}$ and $K_{i,k}$ (which are positive as well). (You can use the reference triangle to calculate these contributions.) Conclude that $K$ is diagonally dominant.

17. As in Section 12.7, assume that the diffusion is isotropic ($P=Q$) and the angles in the triangles in the mesh never exceed $\pi/2$. Show that $A$ and $A+K$ are diagonally dominant, even when mixed boundary conditions are imposed.

18. Compare your proof with the proof in Chapter 4 in [68].

19. Use your answers to the exercises at the end of Chapter 11 and the guidelines in this chapter to calculate the stiffness matrix for the diffusion problem in three spatial dimensions:
    $$-(P u_x)_x-(Q u_y)_y-(W u_z)_z=F,$$
    where $P$, $Q$, $W$, $F$, and $u$ are scalar functions of the three spatial variables $x$, $y$, and $z$. For finite elements, use tetrahedra. A tetrahedron is a three-dimensional shape with four vertices or corners (connected to each other by four straight lines or edges) and four flat triangular sides or faces. A tetrahedron is denoted by a set of four points in the three-dimensional Cartesian space to serve as its vertices. For example, the unit cube $[0,1]^3$ can be written as the union of six disjoint tetrahedra (Section A.27 in the Appendix). Note that, in this case, the matrix $S_e$ is of order 3 rather than 2. The reference element now has four vertices, $(1,0,0)$, $(0,1,0)$, $(0,0,1)$, and $(0,0,0)$, with the corresponding standard nodal functions $x$, $y$, $z$, and $1-x-y-z$, respectively. (In general, the finite-element mesh is not necessarily structured, so the angles in the tetrahedra in it can take any value. In this exercise, however, we deal only with a uniform three-dimensional mesh, in which every cubic cell can be divided into six tetrahedra as above.) The solution can be found in Section 27.2.

20. Assume that the above three-dimensional diffusion equation is isotropic ($P=Q=W$) and the angles in each side of each tetrahedron never exceed $\pi/2$. Extend the result in Section 12.7, and show that the stiffness matrix is diagonally dominant.
