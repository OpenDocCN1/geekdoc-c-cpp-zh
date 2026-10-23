
Let us use our original assumption to bound the blocks in $Q$ in the following sense:
$$
\begin{aligned}
\|J_{i+1} Q_i B_i^{-1} J_i^{-1}\| &= \|J_{i+1} J_i^{-1} (I - \frac{\Delta t \Lambda_i}{2})(I + \frac{\Delta t \Lambda_i}{2})^{-1}\| \\
&\le \|J_{i+1} J_i^{-1}\| \cdot \|(I - \frac{\Delta t \Lambda_i}{2})(I + \frac{\Delta t \Lambda_i}{2})^{-1}\| \\
&\le 1.
\end{aligned}
$$

(When the eigenvalues of $\Delta t A_i$ lie well away from the origin, this bound can actually be improved to a constant smaller than 1.)

As a result, we have
$$
\|J Q J^{-1}\| \le 1.
$$

Let $M$ denote the number of time steps. Using the above results and the formula
$$
(I - Q)^{-1} = \sum_{k=0}^{M-1} Q^k,
$$
we have
$$
\begin{aligned}
\|J(I - Q)^{-1} J^{-1}\| &= \| \sum_{k=0}^{M-1} (J Q J^{-1})^k \| \\
&\le \sum_{k=0}^{M-1} \|J Q J^{-1}\|^k \\
&\le M.
\end{aligned}
$$

(When the eigenvalues of $\Delta t A_i$ lie well away from the origin, this upper bound can actually be improved to a constant independent of $M$.)

Thus, the application of $(I - Q)^{-1}$ to a vector also produces no instability. This guarantees stability in the time-marching process. In fact, we have
$$
\begin{aligned}
\|J A^{-1} J^{-1}\| &= \|J B^{-1} J^{-1} J(I - Q)^{-1} J^{-1}\| \\
&\le \|J B^{-1} J^{-1}\| \cdot \|J(I - Q)^{-1} J^{-1}\| \\
&\le \Delta t \cdot M = T
\end{aligned}
$$

(where $T$ is the maximal time). This guarantees that small errors in $\mathcal{F}$ indeed produce only small errors in the numerical solution $u$.

## 8.4 Accuracy and Adequacy

Here, we use the above stability result to show that the numerical schemes are accurate and adequate in the sense described below.

Let $\tilde{u}$ be the numerical solution and $u$ be the vector obtained from the solution $u(t,x)$ of the original PDE when confined to the discrete time-space grid. The discretization error
$$
\tilde{u} - u
$$
is the difference between the numerical solution $\tilde{u} = A^{-1} \mathcal{F}$ and the true values in $u$.

We say that a numerical scheme is accurate (and converges to the analytic solution) if the discretization error is sufficiently small. More precisely, the discretization error must approach zero as both $h$ and $\Delta t$ approach zero at the same time.

Of course, the discretization error is never available explicitly, because the solution of the original PDE is unknown. Fortunately, it can be estimated from the truncation error defined below.

The truncation error is the vector
$$
\mathcal{T}=A u.
$$

When the truncation error approaches zero pointwise with $h$ and $\Delta t$, we say that the scheme is consistent. Although $u$ is unknown, the truncation error can still be estimated when the solution of the original PDE is smooth and has a Taylor expansion. In fact, it can be shown that the truncation error at interior grid points $(t,x)$, where $u(t,x)$ is smooth, is as small as
$$
\Delta t\,u_{tt}(t,x)+h\,u_{xx}(t,x)
$$
for the explicit and implicit schemes and
$$
(\Delta t)^2u_{tt}(t,x)+h\,u_{xx}(t,x)
$$
for the semi-implicit scheme. Thus, the truncation error approaches zero whenever both $h$ and $\Delta t$ approach zero at the same time, as required.

The assumption that the solution of the PDE is smooth is fair. Indeed, even when there are discontinuities in the initial or boundary conditions, they are smoothed away by the diffusion term $-\varepsilon u_{xx}(t,x)$ (or $-\varepsilon(u_{xx}(t,x,y)+u_{yy}(t,x,y))$ in the two-dimensional case). Therefore, one can assume that the truncation error is indeed small.

In order to estimate the discretization error $\tilde{u}-u$, note that
$$
\tilde{u}-u=A^{-1}(\mathcal{T}-Au).
$$

In other words, the discretization-error vector is just $A^{-1}$ times the truncation-error vector. Thus, in order to be accurate, the numerical scheme must be stable in the sense that applying $A^{-1}$ to a vector can enlarge its norm only moderately. Using the result in Section 8.3 above, we indeed have
$$
\begin{aligned}
\|J(\tilde{u}-u)\| &= \|JA^{-1}(\mathcal{T}-Au)\| \\
&= \|JA^{-1}J^{-1}J(\mathcal{T}-Au)\| \\
&\leq \|JA^{-1}J^{-1}\|\,\|J(\mathcal{T}-Au)\| \\
&\leq T\|J(\mathcal{T}-Au)\|.
\end{aligned}
$$

This guarantees that the discretization error is indeed small, and the scheme is indeed accurate.

The accuracy property, however, is not always sufficient. In some important applications, the diffusion coefficient $\varepsilon$ is very small and may in practice be even smaller than $h$ and $\Delta t$. Assuming that $\varepsilon$ is fixed as $h$ and $\Delta t$ approach zero is no longer realistic; it suits only problems with substantial diffusion and smooth solution but not problems with little diffusion and practically discontinuous solution. There is a need for a property that suits these cases as well: adequacy.

We say that the numerical scheme is adequate if the discretization error approaches zero as the three parameters $h$, $\Delta t$, and $\varepsilon$ approach zero at the same time. (See [67] and Chapter 3, Sections 8–9, in [68].)

The above discretization-error estimate can still be used to show not only accuracy but also adequacy. For adequacy, however, one should keep in mind that $u$, $\tilde{u}$, and $A$ also depend on $\varepsilon$. Therefore, the derivatives used in the Taylor expansion may grow indefinitely as $\varepsilon$ approaches zero. As a result, a truncation error as large as $h^{-1}$ or $(\Delta t)^{-1}$ may appear next to lines of sharp variation in the solution.

Fortunately, the Jordan matrix $J$ used in these estimates multiplies values at such grid points by very small numbers, whereas values at grid points away from sharp variation in the solution are multiplied by relatively very large numbers. We’ll return to this subject in Chapter 9, Section 9.

## 8.5 Towards Hyperbolic Equations

In hyperbolic equations such as the wave equation in Section 22.1 below, the above setting could still be used. The only difference is that each block submatrix in $A$ should correspond to two consecutive time levels rather than to one time level only. Advancing from the previous pair of time levels (that contains the previous time level and the one before it) to the current pair (that contains the current and previous time levels) is then governed by the corresponding row of blocks in $A$. (The algebraic structure is as in Section 2.2 in [66].) The complete analysis can be found in, e.g., [1], [71].

## 8.6 Exercises

- 1. The heat equation is obtained from the convection-diffusion equation by setting the convection coefficient $C(t,x)$ to 0 and the diffusion coefficient $\varepsilon$ to 1:
  $$
  u_t(t,x) - u_{xx}(t,x) = F(t,x).
  $$
  Let $A_i$ be the tridiagonal matrix representing the discrete second derivative with respect to the spatial variable $x$ at the $i$-th time step. Show that $A_i$ is symmetric and diagonally dominant.

- 2. Use the above result to show that the stability condition in Section 8.3 holds, so the implicit and semi-implicit schemes are stable (and, hence, accurate) with respect to the usual norm.

- 3. Find a bound for $\Delta t / h^2$ for which the explicit scheme is also stable and, hence, accurate. The solution can be found in Section A.11 of the Appendix.

- 4. The time-dependent diffusion equation with variable coefficient is defined by
  $$
  u_t(t,x) - (P(t,x)u_x(t,x))_x = F(t,x),
  $$
  where $P(t,x)$ is a given positive and differentiable function. The $x$-derivative at the midpoints is discretized by
  $$
  P u_x(i\Delta t,(j+1/2)h) \simeq h^{-1} P(i\Delta t,(j+1/2)h)[u(i\Delta t,(j+1)h) - u(i\Delta t,jh)].
  $$
  The spatial term in the PDE is discretized by the divided difference of approximations of the above form at $x = (j + 1/2)h$ and $x = (j - 1/2)h$ [78]. Show that this discretization produces a tridiagonal matrix $A$, that is symmetric and diagonally dominant.

- 5. Use the above result to show that the implicit and semi-implicit schemes are stable (and, hence, accurate) with respect to the usual norm.

- 6. Find a bound for $\Delta t / h^2$ for which the explicit scheme is also stable (and, hence, accurate). The solution can be found in Section A.11 of the Appendix.

- 7. Using the above guidelines, show that the above time-marching schemes are stable and accurate with respect to the usual norm for the heat equation in two spatial dimensions:
  $$
  u_t(t,x,y) - u_{xx}(t,x,y) - u_{yy}(t,x,y) = F(t,x,y).
  $$

- 8. Similarly, show that the above time-marching schemes are stable and accurate with respect to the usual norm for the time-dependent diffusion equation in two spatial dimensions:
  $$
  u_t(t,x,y) - (P(t,x,y)u_x(t,x,y))_x - (Q(t,x,y)u_y(t,x,y))_y = F(t,x,y),
  $$
  where $P(t,x,y)$ and $Q(t,x,y)$ are given positive and differentiable functions and the spatial discretization is done as in the one-dimensional case above.

- 9. Assume that the convection coefficient $C()$ in the convection-diffusion equation is independent of $t$. (For example, $C = 1$ in the left half of the $x$-interval and $C = -1$ in the right half of it.) Show that the stability condition in Section 8.3 holds, and, hence, the implicit and semi-implicit schemes are stable, accurate, and adequate with respect to the norm used there.

- 10. For the general convection-diffusion equation, assume that the stability condition in Section 8.3 holds, so the implicit and semi-implicit schemes are stable (and, hence, accurate and adequate) with respect to the norm used there. Find the bound for $\Delta t$ for which the explicit scheme is also stable (and, hence, accurate and adequate) with respect to that norm. The solution can be found in Section A.11 of the Appendix.
