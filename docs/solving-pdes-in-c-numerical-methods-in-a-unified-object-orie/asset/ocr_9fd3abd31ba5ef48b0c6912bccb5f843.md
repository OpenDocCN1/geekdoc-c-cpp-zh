# Chapter 20

# The Linear Elasticity Equations

In this chapter, we apply the adaptive-refinement algorithm to the linear elasticity system of PDEs in a circular domain. We show the efficiency of this algorithm, particularly when used in conjunction with the multigrid preconditioner to solve the individual linear systems in the individual refinement levels. For this purpose, the multigrid algorithm must be modified in such a way that the transfer of data between fine and coarse grids is done separately for each unknown function.

# 20.1 System of PDEs

So far, we have considered scalar PDEs, with scalar unknown function $u \equiv u(x, y)$. In this chapter, we consider the more complicated case of a system of PDEs in which two or more unknown functions, say $u \equiv u(x, y)$ and $v \equiv v(x, y)$, need to be solved for. The unknown functions $u$ and $v$ are coupled in the system of PDEs in the sense that they depend on each other and cannot be solved for separately.

The system of coupled PDEs is also called a “vector PDE,” because it can be rewritten as a single equation in the unknown (two-dimensional) vector $\bar{u} \equiv (u, v)$ and the corresponding derivatives $\bar{u}_x = (u_x, v_x)$ and $\bar{u}_y = (u_y, v_y)$. In this style, the coefficients in the PDE are placed in a $2 \times 2$ matrix.

# 20.2 The Strong Formulation

Here, we consider the system of linear elasticity equations in the two-dimensional domain $\Omega$. The system is characterized by the Poisson ratio $\nu$, $0 \le \nu < 1$, which is a typical constant that depends on the particular material under consideration. For most materials, $0.25 \le \nu \le 0.35$; the prominent exception is rubber, for which $\nu = 0.5$.

The system of linear elasticity equations in its strong form is given by

```
$u_{xx} + \frac{1-\nu}{2} u_{yy} + \nu v_{yx} + \frac{1-\nu}{2} v_{xy} = \mathcal{F}$,
```

```
$\frac{1-\nu}{2} u_{yx} + \nu u_{xy} + \frac{1-\nu}{2} v_{xx} + v_{yy} = \mathcal{G}$
```

at points $(x, y) \in \Omega$. Here, $\mathcal{F}$ and $\mathcal{G}$ are given right-hand-side functions in $\Omega$.