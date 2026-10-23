
## 12.4 Properties of the Stiffness Matrix

Here, we discuss some properties of the stiffness matrix. It turns out that it has some attractive properties, which indicate that the finite-element discretization is indeed appropriate.

The properties of the stiffness matrix $A$ follow from the corresponding properties of the bilinear form $a(\cdot,\cdot)$ defined in Chapter 11, Section 2. First, the symmetry of $a(\cdot,\cdot)$ implies that $A$ is also symmetric. Indeed,

\[
A_{i,j}=a(\phi_j,\phi_i)=a(\phi_i,\phi_j)=A_{j,i}.
\]

Furthermore, $A$ is also positive semidefinite, in the sense that, for every $N$-dimensional vector $v$,

\[
v^tAv\ge 0.
\]

Indeed,

\[
\begin{aligned}
v^tAv&=\sum_{0\le i,j<N}v_iA_{i,j}v_j\\
&=\sum_{0\le i,j<N}v_i a(\phi_j,\phi_i)v_j\\
&=a\left(\sum_{j=0}^{N-1}v_j\phi_j,\sum_{i=0}^{N-1}v_i\phi_i\right)\\
&\ge 0.
\end{aligned}
\]

Furthermore, the coercivity of the quadratic form $a(u,u)$ implies that $A$ is also positive definite in the sense that, for every nonzero $N$-dimensional vector $v$,

\[
v^tAv>0.
\]

Indeed, because $v$ is nonzero, the function

\[
\sum_{j=0}^{N-1}v_j\phi_j
\]

is not identically zero. Still, it vanishes at nodes that lie in $\Gamma_0$, so it has a reference point on which it vanishes. Thanks to the coercivity property, we must have

\[
a\left(\sum_{j=0}^{N-1} v_j \phi_j, \sum_{j=0}^{N-1} v_j \phi_j\right) > 0,
\]

which implies that $v^T A v > 0$, as required.

In summary, the stiffness matrix $A$ is symmetric and positive definite, or SPD for short.

In some special cases, the stiffness matrix $A$ may have more attractive properties. Consider, for example, triangulation with angles that never exceed $\pi/2$ ($90^\circ$). Assume also that the diffusion problem is isotropic ($P \equiv Q$). In this case, it is shown in Section 12.7 below that $A$ is an L-matrix, which means that all of its off-diagonal elements are negative or 0:

\[
A_{i,j} \le 0, \quad 0 \le i, j < N, \, i \neq j.
\]

Furthermore, in this case, $A$ is also diagonally dominant in the sense described in Chapter 8, Section 1.

The combination of these two properties (L-matrix and diagonal dominance) implies that $A$ is also an M-matrix in the sense that it has a nonnegative inverse [78]:

\[
(A^{-1})_{i,j} \ge 0, \quad 0 \le i, j < N.
\]

This property is particularly attractive, because it indicates that the numerical solution is obtained from some weighted average of the conditions imposed at the boundary and the right-hand-side function $F$. In particular, in the Laplace equation, where $P \equiv Q \equiv 1$ and $F \equiv 0$, it implies that the maximum principle is observed not only in the original boundary-value problem but also in the discrete system. This indicates that the discrete system indeed approximates the original PDE well.

In the more general case where $P$ and $Q$ can be variable and $F$ is not necessarily zero, the M-matrix property still indicates that the discretization is well done. Indeed, the inverse of the differential operator can be written as an integral operator with a nonnegative kernel, known as the Green function. The M-matrix property is just the discrete analogue of this property.

As discussed in Section 12.7 below, the above properties exist if the diffusion problem is isotropic ($P \equiv Q$) and the angles in the triangulation are either acute or right. In general, it is a good idea to keep the angles in the triangulation moderate and avoid degenerate triangles with too small or too large angles. Stretched triangles with very small angles should be used only when necessary, for example, at curved boundaries.

A mesh with moderate angles is called regular. Meshes with high regularity have a better chance of producing good numerical approximations. Increasing regularity in the mesh is thus an important guideline in mesh construction and is also used in the adaptive mesh refinement in Chapter 14, Section 2.

## 12.5 Calculating the Stiffness Matrix

In order to calculate the stiffness matrix $A$, we use a standard reference triangle on which the integration is carried out. The integral over a triangle in the mesh is calculated by mapping the triangle onto the reference triangle. The reference triangle, denoted by $r$, is displayed in Figure 12.2. The three typical (standard) nodal functions in $r$ are

\[
\begin{aligned}
\phi_{1,0} &= x, \\
\phi_{0,1} &= y, \\
\phi_{0,0} &= 1 - x - y.
\end{aligned}
\]

Each of these linear functions has the value 1 at one of the vertices of $r$ and 0 at the other two vertices. (This is why they are called "nodal.") The typical nodal functions are essential in the calculation of the stiffness matrix.

Let us now show how $r$ is used to calculate the stiffness matrix. Let $e$ denote a triangle in the mesh, as in Figure 12.1, with vertices denoted by $i$, $j$, and $k$. Let $M_e : r \to e$ be the affine mapping that maps $r$ onto $e$, namely, the mapping composed of a linear transformation followed by a shift by a constant vector:

\[
M_e(x, y) = S_e \begin{pmatrix} x \\ y \end{pmatrix} + s_e,
\]

where $(x, y)$ is any point in the Cartesian plane, $S_e$ is a $2 \times 2$ matrix, and $s_e$ is a two-dimensional constant vector. It is assumed that the vertices of $r$ are mapped to the vertices of $e$.

![](img/1f293b0ceb2de964310ea7f941a1b580_372_0.png)

Figure 12.1. The original finite element $e$ in the mesh.

![](img/1f293b0ceb2de964310ea7f941a1b580_372_1.png)

Figure 12.2. The reference element $r$ that is mapped to $e$ by $M_e$.

The gradient of $\phi_i$ (the two-dimensional vector whose components are the $x$- and $y$-derivatives of $\phi_i$) is given by

\[
\nabla\phi_i = \nabla(\phi_{1,0} \circ M_e^{-1}) = \nabla(\phi_{1,0}) S_e^{-1},
\]

where the gradient of $\phi_i$, $\nabla(\phi_i)$, is evaluated at a point $(x, y) \in e$, and the gradient of $\phi_{1,0}$ is evaluated at its inverse image $M_e^{-1}((x, y)) \in r$.

Further simplification is obtained by recalling that $\phi_{1,0} = x$, so its gradient is actually the constant vector $(1, 0)$. With this observation, the gradient of $\phi_i$ is just the first row in $S_e^{-1}$:

\[
\nabla\phi_i = \left( (S_e^{-1})_{1,1}, (S_e^{-1})_{1,2} \right).
\]

Similarly, for $\phi_j$ we have

\[
\nabla\phi_j = \nabla(\phi_{0,1}) S_e^{-1},
\]

where the gradient of $\phi_j$ is evaluated at a point $(x, y) \in e$, and the gradient of $\phi_{0,1}$ is evaluated at its inverse image $M_e^{-1}((x, y)) \in r$.

Again, one can simplify the above by recalling that $\phi_{0,1} = y$, so its gradient is just the constant vector $(0, 1)$. With this observation, the gradient of $\phi_j$ is just the second row in $S_e^{-1}$:

\[
\nabla\phi_j = \left( (S_e^{-1})_{2,1}, (S_e^{-1})_{2,2} \right).
\]

We are now ready to calculate the elements in the stiffness matrix $A$. For simplicity, we assume that $K \equiv 0$ in the PDE, so only the second-derivative terms remain in it. Let us use the notation

\[
\text{diag}(P, Q) = \begin{pmatrix} P & 0 \\ 0 & Q \end{pmatrix}.
\]

Now, $A_{i,j}$ in the stiffness matrix can be written as the sum of contributions from individual triangles:

\[
A_{i,j} = \sum_e \int_e \nabla\phi_j \, \text{diag}(P, Q) \, \nabla\phi_i \, dx \, dy.
\]

Here, the sum goes over all triangles in the mesh. Still, only those triangles that use both $i$ and $j$ as vertices (like the triangle in Figure 12.1) actually contribute to $A_{i,j}$. It is therefore common to say that $A_{i,j}$ (and, in fact, $A$) is "assembled" from the nonzero contributions from the individual finite elements.

Using the rule of the integral over a mapped domain, we have that the contribution from $e$ to $A_{i,j}$ is

\[
\begin{aligned}
\int_e \nabla\phi_j \, \text{diag}(P, Q) \, \nabla\phi_i \, dx \, dy
&= \int_r \nabla\phi_{0,1} S_e^{-1} \, \text{diag}(P M_e, Q M_e) S_e^{-t} \, \nabla\phi_{1,0} \, dM_e(x, y) \\
&= \int_r (0,1) S_e^{-1} \, \text{diag}(P M_e, Q M_e) S_e^{-t} \begin{pmatrix} 1 \\ 0 \end{pmatrix} \left| \det\left(\frac{\partial M_e(x,y)}{\partial (x,y)}\right) \right| \, dx \, dy \\
&= \int_r (0,1) S_e^{-1} \, \text{diag}(P M_e, Q M_e) S_e^{-t} \begin{pmatrix} 1 \\ 0 \end{pmatrix} |\det(S_e)| \, dx \, dy.
\end{aligned}
\]
