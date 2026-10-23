# Chapter 7

# The Convection-Diffusion
Equation

In this chapter, we describe finite-difference methods to discretize the convection-diffusion equation in one and two spatial dimensions. In particular, we use explicit, implicit, and semi-implicit schemes to march from the current time step to the next one and the upwind scheme to discretize the spatial derivatives. The entire algorithm is implemented in C++ using a hierarchy of objects: from the time-space grid at the high level to the individual grid lines at the low level, with the difference operators that act upon them.

# 7.1  Initial-Boundary-Value Problems

We are now ready to use the programming tools developed above in the numerical solution of initial-boundary-value problems. Here, we consider one of the most important parabolic PDEs, which is commonly used to model physical processes: the convection-diffusion equation [54], [60]. In one spatial dimension, this equation takes the form

$$u_t(t,x)-\varepsilon u_{xx}(t,x)+C(t,x)u_x(t,x)=F(t,x), \qquad 0<t<T,\ 0<x<L.$$

Here, $T$ is the maximal time, $L$ is the length of the $x$-interval, $F(t,x)$ is the given right-hand side, $\varepsilon$ is the small diffusion coefficient, $C(t,x)$ is the given convection coefficient, and $u(t,x)$ is the unknown solution.

We further assume that initial conditions are given in the following form:

$$u(0,x)=u^{(0)}(x), \qquad 0<x<L,$$

where $u^{(0)}(x)$ is a given function. We also assume that Dirichlet boundary conditions are imposed on the right edge:

$$u(t,L)=G(t,L), \qquad 0<t<T,$$

and mixed boundary conditions are imposed on the left edge:

$$\alpha(t,0)u(t,0)+u_n(t,0)=G(t,0), \qquad 0<t<T,$$

where $\alpha(t)$ and $G(t)$ are given functions and $n=-x$ is the direction that points away from the interval $[0,L]$ at its left edge 0 (the outer normal direction).