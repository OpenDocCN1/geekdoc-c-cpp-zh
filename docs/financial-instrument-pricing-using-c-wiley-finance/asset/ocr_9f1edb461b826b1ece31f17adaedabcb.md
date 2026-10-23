+   Gain from dividend yield:

```
$$\sum_{j=1}^{n} D_j S_j \frac{\partial V}{\partial S_j}.$$
```

(20.6)

+   Hedging costs or slippage:

```
$$-\frac{1}{2}\sum_{i,j=1}^{n} \rho_{ij}\sigma_i\sigma_j S_i S_j \frac{\partial^2 V}{\partial S_i \partial S_j}.$$
```

(20.7)

Our interest is in discovering robust numerical schemes that produce reliable and accurate results irrespective of the size of the parameter values in equation (20.4).

Equation (20.1) has an infinite number of solutions in general. In order to define a unique solution, we need to define some constraints. To this end, we define initial condition and boundary conditions for (20.1). We achieve this by defining the space in which equation (20.1) is assumed to be valid. In general, we note that there are three types of boundary conditions associated with equation (20.1). These are:

+   First boundary value problem (Dirichlet problem).

+   Second boundary value problem (Neumann, Robin problems).

+   Cauchy problem.

The first boundary value problem is concerned with the solution of equation (20.1) in a bounded domain $D = \Omega \times (0,T)$, where $\Omega$ is a bounded subset of $\mathbb{R}^n$ and $T$ is a positive number. In this case we seek a solution of equation (20.1) satisfying the conditions:

```
$$u|_{t=0}=\phi(x)\quad\text{(inital condition)}$$ $$u|_{\Gamma}=\psi(x,t)\quad\text{(boundary condition)}$$
```

(20.8)

where $\Gamma$ is the boundary of $\Omega$. The boundary conditions in (20.8) are called Dirichlet boundary conditions because the solution is given on the boundary. These conditions arise when we model single and double barrier options in the one-factor case (see Duffy, 2006). They also occur when we model plain options on a transformed or truncated domain.

The second boundary value problem is similar to (20.8) except that instead of giving the value of $u$ on the boundary $\Gamma$ the directional derivatives are included, as seen in the following example:

```
$$\left(\frac{\partial u}{\partial \eta}+a(x,t)u\right)=\psi(x,t),\quad x\in\Gamma.$$
```

(20.9)

In this case $a(x,t)$ and $\psi(x,t)$ are known functions of $x$ and $t$, and $\frac{\partial}{\partial \eta}$ denotes the derivative of $u$ with respect to the outward normal $\eta$ at $\Gamma$. A special case of (20.9) is when $a(x,t)\equiv0$; then