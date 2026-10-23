In general, it is recommended to use STL algorithms as building blocks when creating higher-level functionality. This avoids reinvention of the software wheel. In particular, we discussed the relevant STL algorithms in Chapters 17 and 18.

# 23.7 ACCURACY AND PERFORMANCE

We know that the Saul’yev scheme is unconditionally stable and that it is first-order accurate (Saul’yev, 1964). This is in contrast to the FTCS scheme that is also first-order accurate but only conditionally stable. This means that we need to choose a large number of time steps in order to avoid oscillations. Furthermore, we use upwinding or downwinding in the y variable in equation (23.7) depending on the sign of the convection coefficient. The method can be applied to the model problem:

∂u/∂t + a ∂u/∂x = 0,  −∞ < x < ∞, t > 0.  (23.10)

The simplest upwind scheme is the explicit first-order upwind scheme defined by:

u_j^{n+1} − u_j^{n} / Δt + a (u_j^{n} − u_{j−1}^{n}) / h = 0 for a > 0  (23.11)

and

u_j^{n+1} − u_j^{n} / Δt + a (u_{j+1}^{n} − u_j^{n}) / h = 0 for a > 0.  (23.12)

It can be shown using von Neumann stability analysis (see Duffy, 2006) that this scheme is stable if the Courant–Friedrichs–Lewy (CFL) condition is satisfied:

c = |a Δt / h| ≤ 1.  (23.13)

The schemes (23.11) and (23.12) are first-order accurate in space and time but they can introduce severe numerical diffusion and dissipation in the solution due to the presence of large gradients. In our work here we take a modified version of schemes (23.11) and (23.12), namely:

u_j^{n+1} − u_j^{n} / Δt + a (u_j^{n+1} − u_{j−1}^{n}) / h = 0 for a > 0  (23.14)

and

u_j^{n+1} − u_j^{n} / Δt + a (u_{j+1}^{n} − u_j^{n+1}) / h = 0 for a > 0.  (23.15)

Schemes (23.14) and (23.15) could be called semi-implicit schemes.
We can verify (again by von Neumann stability analysis) that this scheme is unconditionally stable and hence we have ignored the constraint (23.13) in our code, which is highly