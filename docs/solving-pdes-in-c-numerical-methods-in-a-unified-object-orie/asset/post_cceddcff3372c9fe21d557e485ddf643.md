
In what follows, we’ll see how these contributions are calculated explicitly in common examples.

## 12.6 Example: Rectangular Domain and Uniform Mesh

As mentioned above, finite elements are particularly suitable for the approximation of complicated domains. Here, however, we consider a simple example in which the domain is rectangular, as in Chapter 7, Section 13. The diffusion coefficients in this example can be variable and even discontinuous. The finite-element discretization method, which is based on the well-posed weak formulation, is thus most suitable.

In the present example, the domain $\Omega$ is the rectangle $[0, L_x] \times [0, L_y]$, $K \equiv 0$, and $\Gamma_0$ contains the upper and right edges and $\Gamma$ contains the bottom and left edges in the rectangle.

For the finite-element mesh, we use a uniform triangle mesh as in Figure 12.3. We also assume that $\alpha$ is constant in each triangle in the mesh but may be discontinuous across the edges of the triangles.

![](img/1f293b0ceb2de964310ea7f941a1b580_375_0.png)

Let $e$ be a triangle in the mesh (as in Figure 12.4) with vertices $i, j$, and $k$. As in Section 12.5, let $M_e$ map the reference triangle $r$ onto $e$, and let $S_e$ be its Jacobian. As shown in Section 12.5, the first column in $S_e$ is the two-dimensional vector that represents the difference of vertices $i - k$, and the second column is $j - k$. For the right-angle triangle $e$ of Figure 12.4, $i - k = (-h_x, 0)$ and $j - k = (0, h_y)$. Therefore, we have

$$
S_e = \begin{pmatrix} -h_x & 0 \\ 0 & h_y \end{pmatrix}
$$

As a result, we have

$$
\det(S_e) = -h_x h_y
$$

and

$$
S_e^{-1} = \begin{pmatrix} -h_x^{-1} & 0 \\ 0 & h_y^{-1} \end{pmatrix}
$$

![](img/1f293b0ceb2de964310ea7f941a1b580_376_0.png)

### Figure 12.4. The original finite element $e$ in the uniform mesh. The reference element $r$ is mapped to $e$ by $M_e$.

The contribution from $e$ to $A_{i,k}$ is, thus,

$$
\begin{align*}
\int_e \nabla \phi_k \text{diag}(P, Q) \nabla \phi_i \, dx \, dy \\
= \int_r \nabla \phi_{0,0} S_e^{-1} \text{diag}(P M_e, Q M_e) S_e^{-1} \nabla \phi_{1,0} |\det(S_e)| \, dx \, dy \\
= \int_r (-1, -1) S_e^{-1} \text{diag}(P M_e, Q M_e) S_e^{-1} (1 \setminus 0) h_x h_y \, dx \, dy \\
= -h_x^{-2} h_x h_y \int_r P M_e \, dx \, dy.
\end{align*}
$$

The other triangle that contributes to $A_{i,k}$ is the triangle $t$ that lies below the edge connecting $i$ to $k$ (Figure 12.5). The contribution from $t$ is calculated in a similar way. The rest of the triangles contribute nothing to the $A_{i,k}$-element, because either $\phi_i$ or $\phi_k$ vanishes on them. The final result is, thus,

$$
A_{i,k} = -h_x^{-1} h_y \left( \int_r P M_e \, dx \, dy + \int_r P M_t \, dx \, dy \right).
$$

A similar method is used to calculate $A_{i,k}$ for every two nodes $i$ and $k$. Of course, when $i$ and $k$ don't lie in the same triangle, $A_{i,k}$ vanishes. Thus, $A$ is sparse in the sense that most of its elements vanish. In an efficient implementation of sparse matrices, only nonzero matrix elements are stored (see Chapters 4 and 16).

The main-diagonal elements in $A$ ($k = i$ in the above discussion) can be calculated using the same method. In this case, however, the six triangles that surround the node $i$ contribute to $A_{i,i}$.

Let us now calculate the contribution to $A_{i,k}$ from the boundary conditions. Assume that the edge that connects $i$ to $k$ lies on the bottom edge of the rectangular domain, so there is no triangle $t$ below it. In this case, the mixed boundary condition imposed on the bottom edge also contributes to $A_{i,k}$. In the following, we calculate this contribution.

![](img/1f293b0ceb2de964310ea7f941a1b580_377_0.png)

### Figure 12.5. The finite element $t$ onto which the reference element $r$ is mapped by $M_t$.

Let $M_{i,k}$ denote the restriction of $M_e$ to the interval $[0,1]$, so that $M_{i,k}$ maps the interval $[0,1]$ onto the interval $[k,i]$, with the Jacobian, or derivative, $-h_x$. For simplicity, assume also that $\alpha$ is constant at the line connecting $i$ to $k$, and its value there is denoted by $\alpha_{i,k}$. The contribution from the mixed boundary conditions to $A_{i,k}$ is, thus,

$$
\begin{align*}
\int_{[i,k]} \alpha \phi_k \phi_i \, dx \\
= \alpha_{i,k} \int_{M_{i,k}^{-1}([i,k])} \phi_{0,0} \phi_{1,0} \left| \frac{dM_{i,k}}{dx} \right| \, dx \\
= \alpha_{i,k} \int_0^1 (1 - x - 0) x |-h_x| \, dx \\
= \frac{\alpha_{i,k} h_x}{6}.
\end{align*}
$$

The stiffness matrix for the present example has the same stencil (structure) as the difference operator in Chapter 7, Section 13. In fact, every node in the mesh is connected in $A$ only to its nearest (immediate) neighbors, namely, the nodes to its right, left, top, and bottom. Thus, the stiffness matrix can actually be implemented most efficiently as a "difference2" object (Section A.10 of the Appendix).

In Chapter 13, we introduce a more general implementation, which is suitable not only for uniform meshes such as the present one but also for general unstructured meshes, which are used often in practical applications. With this implementation, the stiffness matrix has a far more complex structure and must be implemented as a more sophisticated sparse-matrix object (Chapter 16).

The remainder of this book deals with the construction and numerical solution of the stiffness system on general unstructured meshes. In realistic applications, where the domain is complicated and the solution of the weak formulation may have sharp variation, the finite-element triangulation must be highly unstructured. For example, the finite-element mesh can be rather coarse (low resolution) where the solution is expected to be rather smooth, and rather fine (high resolution) where the solution is expected to vary sharply. It is in this case that the advantage of C++ becomes most clear.

## 12.7 M-Matrix Property in the Isotropic Case

This section gives motivation to why finite-element meshes should be regular in the sense that the triangles should have moderate angles. Readers who are mainly interested in the practical aspects can skip it and proceed to Section 12.8.

As discussed in Section 12.4 above, the M-matrix property is most attractive. Although the stiffness matrix is not always an M-matrix, it is possible to specify sufficient conditions that guarantee that it is. This indicates that the finite-element discretization method indeed makes sense.

Assume that the diffusion equation is isotropic; that is, the diffusion coefficients are the same in both the $x$ and $y$ spatial directions:

$$
P(x, y) = Q(x, y), \quad (x, y) \in \Omega.
$$

With this assumption, the contribution from $e$ to $A_{i,j}$ at the end of Section 12.5 takes the form

$$
(0, 1) S_e^{-1} S_e^{-t} (1 \setminus 0) |\det(S_e)| \int_r P M_e \, dx \, dy.
$$

Note that the above integral won’t be affected if $S_e$ is multiplied by an orthogonal matrix on the left. Indeed, if $S_e$ is replaced by $O S_e$ for some orthogonal matrix $O$ (orthogonality means that $O^t = O^{-1}$), then we will still have

$$
(O S_e)^{-1} (O S_e)^{-t} = S_e^{-1} O^{-1} O^{-t} S_e^{-t} = S_e^{-1} S_e^{-t}
$$

and

$$
\det(O S_e) = \det(O) \det(S_e) = \det(S_e).
$$

Therefore, we may assume without loss of generality that the edge connecting $i$ to $k$ in $e$ is parallel to the $x$-axis, as in Figure 12.6, so that the $y$-coordinate of $i - k$ vanishes.

For a finite element $e$ as in Figure 12.6, $S_e$ takes the upper triangular form

$$
S_e = \begin{pmatrix} (S_e)_{1,1} & (S_e)_{1,2} \\ 0 & (S_e)_{2,2} \end{pmatrix},
$$

![](img/1f293b0ceb2de964310ea7f941a1b580_378_0.png)

### Figure 12.6. The rotated finite element.

with $(S_e)_{1,1} > 0$ and $(S_e)_{2,2} > 0$. Therefore, we have

$$
\det(S_e) = (S_e)_{1,1}(S_e)_{2,2}.
$$

Furthermore, $S_e^{-1}$ takes the upper triangular form

$$
S_e^{-1} = \begin{pmatrix} (S_e^{-1})_{1,1} & (S_e^{-1})_{1,2} \\ 0 & (S_e^{-1})_{2,2} \end{pmatrix} = \begin{pmatrix} (S_e)_{1,1}^{-1} & -(S_e)_{1,1}^{-1}(S_e)_{1,2}(S_e)_{2,2}^{-1} \\ 0 & (S_e)_{2,2}^{-1} \end{pmatrix}.
$$

As a result, the above integral that represents the contribution from $e$ to $A_{i,j}$ takes the form

$$
(S_e^{-1})_{2,2} (S_e^{-1})_{1,2} |\det(S_e)| \int_r P M_e \, dx \, dy = -(S_e)_{1,2}(S_e)_{2,2}^{-1} \int_r P M_e \, dx \, dy = -\cot(\theta) \int_r P M_e \, dx \, dy,
$$

where $\theta$ is the (positive) angle between $i - k$ and $j - k$ in Figures 12.1 and 12.6, and cot stands for the cotangent function (cosine divided by sine).

We conclude from the above calculations that the contribution from $e$ to $A_{i,j}$ depends not on the area of $e$ but only on the cotangent of the angle $\theta$ that lies between $i - k$ and $j - k$. If $\theta$ is greater than $\pi/2$, then this cotangent is negative, so the contribution from $e$ to $A_{i,j}$ is positive. In this case, $A$ may not be an L-matrix unless there are negative contributions to $A_{i,j}$ from other triangles to balance this positive contribution. On the other hand, if triangles in the mesh have acute or right angles only, then all contributions to off-diagonal matrix elements in $A$ are nonpositive, and $A$ is an L-matrix.

Let us show that, for triangulation with acute or right angles only, $A$ is also diagonally dominant. Since we have already seen that $A$ is an L-matrix, it is sufficient to show that its row-sums are nonnegative. To see this, consider a node $i$ in the mesh. The sum of the $i$th row in $A$ is the same as $a(v,\phi_i)$, where $v$ is the sum of the nodal basis functions at $i$ and the nodes surrounding it. But since these nodal basis functions are linear, $v$ must be constant on the triangles surrounding $i$, so its gradient vanishes there. It is easy to see that the boundary conditions normally increase the row-sum. This shows that $A$ is indeed diagonally dominant.

The combination of diagonal dominance and the L-matrix property implies that $A$ is indeed also an M-matrix [78]. This property indicates that the finite-element discretization indeed produces a good approximation to the original problem (Section 12.4).

For less regular meshes with angles greater than $\pi/2$, the stiffness matrix may no longer be an M-matrix. Still, it is likely that the finite-element discretization will provide a good approximation on these meshes as well, provided that the irregularity is limited to a rather small area such as the neighborhood of irregular boundaries.

In the next section, we’ll see that the M-matrix property may also apply to the more difficult case of highly anisotropic equations.
