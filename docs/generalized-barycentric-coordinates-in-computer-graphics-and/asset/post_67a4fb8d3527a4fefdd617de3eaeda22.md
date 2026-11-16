
![](img/4913dd83a2a14bc205a0a92cce102c82_289_0.png)

Figure 14.1 Initial mesh (left), refined mesh after two steps (middle), refined mesh after four steps (right).*

![](img/4913dd83a2a14bc205a0a92cce102c82_289_1.png)

Figure 14.2 Relative error in H^1-norm (left) and L^2-norm (right) with respect to the mesh size h.

## 14.3 ADAPTIVE BEM-BASED FEM IN 2D

In the uniform refinement strategy, each element of the mesh is split into two new elements to obtain the next finer mesh. This splitting process is performed as described below. To obtain the optimal rates of convergence according to Theorem 14.1, the solution has to be smooth. This assumption is often violated in practical applications, where singularities can arise due to discontinuous material parameters or reentrant corners in the geometry. Consequently, the convergence slows down for uniform refinement. Therefore, the meshes have to be adapted to the problem in order to recover optimal rates of convergence. For the adaptive

*Reprinted from Numerische Mathematik, Residual error estimate for BEM-based FEM on polygonal meshes, Vol. 118, 2011, pages 765-788, S. Weißer, © Springer-Verlag 2011, with permission of Springer. †Reprinted from Computers & Mathematics with Applications, Vol. 67(7), S. Weißer, Arbitrary order Trefftz-like basis functions on polygonal meshes and realization in BEM-based FEM, pages 1390-1406, Copyright (2014), with permission from Elsevier.

BEM-based FEM, we proceed by adopting a common strategy, which only selects several elements for refinement in each step, see [403]. Essential ingredients are the element-wise error indicators \(\eta_P\) that monitor the approximation quality over the single elements. In the following we assume that these indicators bound the true error in the desired norm such that

```
\(\|u - u_h\| \le c \eta_R = c \left( \sum_{P \in \mathcal{T}_h} \eta_P^2 \right)^{1/2} . \quad (14.14)\)
```

In Section 14.3.2, we present a residual-based error estimator, which bounds the error in the energy norm.

### 14.3.1 Adaptive FEM strategy

The adaptive BEM-based FEM successively refines elements that contribute most to the error. This strategy proceeds in a loop over four steps:

- **SOLVE** The boundary-value problem (14.1) is approximated by means of the BEM-based FEM on the current polygonal mesh using the approximation space \(V_h^k\).

- **ESTIMATE** An error estimator \(\eta_R\) as well as the element-wise error indicators \(\eta_P\) (see Section 14.3.2) are computed on the discretization \(\mathcal{T}_h\).

- **MARK** A minimal subset \(\mathcal{M}_h \subset \mathcal{T}_h\) of all elements are marked according to Dörfler strategy [125] such that

```
\(\left( \sum_{P \in \mathcal{M}_h} \eta_P^2 \right)^{1/2} \ge (1 - \theta) \eta_R,\)
```

where \(0 \le \theta < 1\) is a user-defined parameter. To obtain a minimal set \(\mathcal{M}_h\), it is possible to sort the elements according to their indicators \(\eta_P\) and mark those with the largest indicators. Instead of that, we implemented the marking algorithm given in [125] to achieve linear complexity. Furthermore, we choose \(\theta = 0.5\) in the numerical experiments.

- **REFINE** Each marked element is refined and we consequently obtain a new mesh for the next cycle in the loop. For the refinement of an element \(P\), we bisect \(P\) through its barycenter \(\bar{\boldsymbol{x}}\) orthogonal to its characteristic direction, see Figure 14.3, that is given by the eigenvector that corresponds to the largest eigenvalue of the matrix

```
\(M_{\text{Cov}} = \int_P (\boldsymbol{x} - \bar{\boldsymbol{x}})(\boldsymbol{x} - \bar{\boldsymbol{x}})^\top d\boldsymbol{x}, \quad \bar{\boldsymbol{x}} = \frac{1}{|P|} \int_P \boldsymbol{x} \, d\boldsymbol{x}.\)
```

For more details, see [420]. Furthermore, we check the regularity of the mesh and refine additional elements if \(c_T h_P \le h|_{u_i, u_{i+1}}\) for any \(i = 1, \dots, n\) is violated with a user-defined parameter \(c_T\).

![](img/4913dd83a2a14bc205a0a92cce102c82_291_0.png)

The adaptive mesh refinement process is kept very local. Only the marked and degenerated elements are bisected during the refinement. It is not necessary to resolve hanging nodes and keep the mesh admissible, as for example in the red-blue-green refinement procedure for triangular meshes, see [403]. This advantage is due to the polygonal meshes with very flexible elements.

### 14.3.2 Residual-based error estimate for polygonal meshes

The residual-based a posteriori error estimate bounds the difference of the exact solution and the Galerkin approximation in the energy norm associated to the bilinear form. Among others, the estimate contains the jumps of the conormal derivatives over the element edges. Let \(P \in \mathcal{T}_h\) be a polygonal element with edge \([v_i, v_{i+1}]\) and \(P' \in \mathcal{T}_h\) be the neighboring element that contains this edge. Then, the jump is given on \((v_i, v_{i+1})\) by

> \([u_h] = \frac{\partial u_h|_P}{\partial n_P} + \frac{\partial u_h|_{P'}}{\partial n_{P'}}.\)

We define the so-called edge residual by

> \(R_{P,i} = \begin{cases} 0 & \text{for } (v_i, v_{i+1}) \subset \Gamma_D, \\ g_N - \frac{\partial u_h}{\partial n_P} & \text{for } (v_i, v_{i+1}) \subset \Gamma_N, \\ -\frac{1}{2}[u_h] & \text{for } (v_i, v_{i+1}) \subset \Omega. \end{cases}\)

All ingredients are now available to state the residual-based error estimate that fulfils (14.14) for the energy norm \(\|\nabla \cdot \|_{L_2(\Omega)}\).

### Theorem 14.2 (Reliability)

Let \(\mathcal{T}_h\) be a regular mesh. Furthermore, let \(u \in V\) and \(u_h \in V_h^k\) be the solutions of (14.2) and the Galerkin approximation obtained by (14.3), respectively. Then the residual-based error estimate is reliable, i.e.,

```
\|\nabla(u - u_h)\|_{L_2(\Omega)} \le c \eta_R \quad \text{with} \quad \eta_R^2 = \sum_{P \in \mathcal{T}_h} \eta_P^2,
```

where the error indicators are defined by

```
\eta_P^2 = h_P^2 \|f + \Delta u_h\|_{L_2(P)}^2 + \sum_{i=1}^n h_{[v_i, v_{i+1}]} \|R_{P,i}\|_{L_2([v_i, v_{i+1}])}^2.
```

The constant c > 0 only depends on the regularity parameters of the mesh and the approximation order k.

The error in the energy norm decreases at least as fast as the error estimator $\eta_R$ according to the previous theorem. In order to have a good estimator, which can be used efficiently to estimate the true error, it is important that the error does not decrease faster than $\eta_R$. This behavior is shown in the next theorem, where the error indicators $\eta_P$ are bounded in terms of the error plus some data oscillations. For the lower bound, the estimate involves the neighborhood $\omega_P$ of the element $P$. This patch of elements is given by \(\bar{\omega}_P = \bigcup \{P' : P' \in \mathcal{T}_h, P \cap P' \neq \emptyset\}\).

### Theorem 14.3 (Efficiency)

Under the assumptions of Theorem 14.2, the residual-based error indicator is efficient, i.e.,

```
\eta_P \le c \left( \|\nabla(u - u_h)\|_{L_2(\omega_P)}^2 + h_P^2 \|f - \bar{f}\|_{L_2(\omega_P)}^2 + \sum_{\substack{i=1, \dots, n, \\ [v_i, v_{i+1}] \subset \Gamma_D}} h_{[v_i, v_{i+1}]} \|g_N - \bar{g}_N\|_{L_2([v_i, v_{i+1}])}^2 \right)
```

where \(\bar{f}\) and \(\bar{g}_N\) are piecewise polynomial approximations of the data \(f\) and \(g_N\), respectively. The constant c > 0 only depends on the regularity parameters of the mesh and the approximation order k.

The terms \(\|f - \bar{f}\|_{L_2(\omega_P)}\) and \(\|g_N - \bar{g}_N\|_{L_2([v_i, v_{i+1}])}\) are often called data oscillations. They are usually of higher order.

### 14.3.3 Numerical examples

Let \(\Omega = ((-1, 1) \times (-1, 1)) \setminus ([0, 1] \times [0, -1])\) and \(\Gamma_D = \partial \Omega\). Using polar coordinates \((r, \varphi)\) for \(x = (r \cos \varphi, r \sin \varphi)\), the boundary data \(g_D\) is chosen in such a way that

```
u(r \cos \varphi, r \sin \varphi) = r^{2/3} \sin \left( \frac{2\varphi}{3} \right)
```

is the solution of the boundary-value problem

```
-\Delta u = 0 \quad \text{in } \Omega, \quad u = g_D \quad \text{on } \Gamma.
```
