
![](img/1f293b0ceb2de964310ea7f941a1b580_474_0.png)

**Figure 17.3.** The domain decomposition. The bullets denote nodes in the coarse grid $c$.

![](img/1f293b0ceb2de964310ea7f941a1b580_474_1.png)

**Figure 17.4.** The first prolongation step, in which the known values at the bullets are prolonged to the line connecting them by solving a homogeneous subproblem in the strip that contains this line.

In the domain-decomposition approach, the original domain is viewed as the union of disjoint subdomains. The vertices of these subdomains form the coarse grid $c$ (Figure 17.3). The prolongation operator $P$ consists of two steps: the first step extends a vector defined on $c$ to the nodes that lie on the edges of subdomains, and the second extends it further to the interiors of the subdomains.

For a given coarse-grid vector $v$, the first prolongation step produces the values of the extended vector $Pv$ at nodes that lie on the edges of the subdomains (between coarse-grid nodes). The second prolongation step uses these values as Dirichlet data to solve a homogeneous PDE in each individual subdomain (Figure 17.5). The numerical solution of these subproblems produces $Pv$ in the interiors of the subdomains as well. Because these subproblems are independent of each other, they can be solved simultaneously in parallel.

The first prolongation step, which extends $v$ to the edges in Figure 17.3, is trickier than the second one. Clearly, it should use the original values of $v$ at the endpoints of each edge as Dirichlet data for a one-dimensional equation in this edge. However, it is not clear how this one-dimensional equation should be defined.

![](img/1f293b0ceb2de964310ea7f941a1b580_476_0.png)

**Figure 17.6.** Prolonging to node $i$ by solving a homogeneous Dirichlet–Neumann subproblem in the "molecule" of finite elements that share $i$ as their joint vertex.

in it is formulated in a more general way in the AMGe method [19]. No subdomains or edges are used. The coarse grid $c$ is constructed algebraically using the coefficient matrix $A$ only. The prolongation operator $P$ is defined as follows. At each node $i \in f$, $(Pv)_i$ is obtained by solving the homogeneous PDE numerically in the "molecule" of finite elements that share $i$ as their joint vertex (Figure 17.6). The boundary conditions for this subproblem are of Dirichlet type at nodes in $c$ (where $v$ is available) and of homogeneous Neumann type elsewhere. The numerical solution of this subproblem at $i$ is then accepted as the prolonged value $(Pv)_i$. This defines $(Pv)_i$ at every $i \in f$, so no second prolongation step is needed.

In the AMGM method [43], the above approach is reformulated in pure algebraic terms. The molecules are defined algebraically and can also be used in the recursive calls in the multigrid V-cycle.

We conclude this section by showing that the domain-decomposition approach also leads to the present definition of $P$ in Section 17.8 above. Instead of solving a subproblem on a molecule, we assume that the prolonged vector $Pv$ should satisfy the $i$th equation in the homogeneous linear system

$$ \sum_{j \in c} A_{i,j} v_j + \sum_{j \in f} A_{i,j} (Pv)_j = 0. $$

Our algebraic molecule is, thus, the set of unknowns $j$ for which $A_{i,j} \neq 0$. Of these unknowns, $v_j$ is available for each $j \in c$, which is the algebraic analogue to the Dirichlet conditions. Furthermore, we use the algebraic analogue of the discrete homogeneous Neumann conditions to assume that $(Pv)_j$ is the same for every $j \in f$ in the molecule, which leads to the definition

$$ (Pv)_i \equiv -\frac{\sum_{j \in c} A_{i,j} v_j}{\sum_{j \in f} A_{i,j}}, $$

which is practically the same as the definition used in Section 17.8.

The above definition applies to every $i \in f$, so it actually completes the definition of $P$. Still, one could use the resulting values of $Pv$ to improve the prolongation with a second step. In this step, the algebraic Dirichlet conditions are used at the unknowns $j \neq i$, using the values $(Pv)_j$ from the first prolongation step:

$$ (Pv)_i \equiv -\frac{\sum_{j \in c} A_{i,j} v_j + \sum_{j \in f, j \neq i} A_{i,j} (Pv)_j}{A_{i,i}}. $$

This amounts to an extra Jacobi relaxation on the values $(Pv)_i$ at each $i \in f$. The second prolongation step can thus be formulated more compactly as follows. Define the diagonal matrix $D$ by

$$ D_{i,i} \equiv \begin{cases} 1 & \text{if } i \in f, \\ 0 & \text{if } i \in c. \end{cases} $$

Modify the prolongation matrix $P$ in Section 17.8 by the substitution

$$ P \leftarrow (I - \operatorname{diag}(A)^{-1} D A) P $$

(where $I$ is the identity matrix of the same order as $A$).

The rest of the multigrid algorithm is as before ($R = P^t$, $Q = R A P$, and recursion). When this modified preconditioner is used in PCG in the applications in Part VI below, the number of PCG iterations is reduced by up to 50%. Unfortunately, the amount of setup time required to construct the "multigrid" object increases substantially due to the extra matrix-times-matrix operations. This is why we stick to the original definition of $P$ and don't use the above modification here. This modification may be worthwhile when a powerful parallel computer is available to carry out matrix-times-matrix operations efficiently. This is the subject of the next chapter.

### 17.14 Multigrid for Systems of PDEs

Consider now a system of PDEs with, say, two unknown functions. In a multigrid algorithm for this problem, the discrete vector function $(u, v)$ defined on the coarse grid (the bullets in Figure 17.6) should be prolonged into a vector function of the form $(P_1 u, P_2 v)$ defined on the entire fine grid. For this, we need to define $(P_1 u)_i$ and $(P_2 v)_i$ at the node $i$ that lies in between the bullets in Figure 17.6.

prolong $u$ $\leftarrow$ assume $v \equiv 0$

prolong $v$ $\leftarrow$ assume $u \equiv 0$

**Figure 17.7.** Prolongation for a system of PDEs with two unknown functions. To prolong $u$, assume that $v$ vanishes. To prolong $v$, assume that $u$ vanishes.

A sensible way to do this is to prolong $u$ completely separately from $v$ (Figure 17.7). More precisely, in the definition of $(P_1 u)_i$, it is assumed that $v \equiv 0$. This way, the subproblem solved in the molecule contains no $v$-terms at all, so $u$-values are prolonged in terms of $u$-values only. Similarly, in the definition of $(P_2 v)_i$, it is assumed that $u \equiv 0$, so $v$-values are prolonged in terms of $v$-values only. This approach is indeed used in the elasticity system in Section 20.9 below.

### 17.15 Multigrid for High-Order Finite Elements

In the above, a domain decomposition approach is used to define a prototype multigrid algorithm for linear finite elements. The idea behind this algorithm is then used to define an algebraic multigrid version, which is completely automatic and ready to be applied to many different applications.

Although algebraic multigrid can be applied to linear systems arising from either linear or high-order finite elements, we design here a multigrid version that is particularly suitable for high-order finite elements, and hence has a better chance of converging rapidly to the desired solution.

Consider a high-order finite-element mesh as in Figure 15.3. In order to define a suitable multigrid algorithm, one must first define the coarse grid (or level). In this case, the coarse grid is the set of basis functions whose value is 1 at some node (bullet), and 0 at all the other degrees of freedom in the entire mesh (Figure 17.8).

![](img/1f293b0ceb2de964310ea7f941a1b580_478_0.png)

**Figure 17.8.** The coarse grid that contains the bullets: each bullet stands for a basis function whose value is 1 at the bullet only, and 0 for all the other degrees of freedom in the entire mesh.

![](img/1f293b0ceb2de964310ea7f941a1b580_478_1.png)

**Figure 17.9.** Prolongation from the given value at the bullet at the center to the extra nine degrees of freedom corresponding to partial derivatives at the center and normal derivatives at the four edge midpoints around it.

All that is left to do is to define the prolongation operator $P$ that transforms a coarse-grid function $u$ defined in the coarse grid only into a fine-grid function $Pu$ defined in the entire high-order finite-element mesh. For this, assume that the value of $u$ is given at the center node in Figure 17.9. To prolong this value to the rest of the degrees of freedom in
