The explicit nature of the propagation process also emerges by rewriting Equations 13.46 through 13.48 in matrix notations:

u^{n+1} = B · u^{n},   n = 0,1,2,…   (13.49)

The propagation matrix B is tridiagonal and the vector u^{n} gathers the solution values from all the spatial mesh points at the time step t_n:

B = [ 1 0   0 ; λ 1−2λ λ ; ⋱ ⋱ ⋱ ;   λ 1−2λ λ ; 0   0 1 ],   u^{n} = [ u_1^{n} ; u_2^{n} ; ⋮ ; u_{N_x-1}^{n} ; u_{N_x}^{n} ].   (13.50)

Each component of the propagated solution u^{n+1} results individually, by the multiplication of the matrix B with the previous solution vector u^{n}.

The routine PropagFTCS (Listing 13.6) solves an elementary Cauchy problem for the diffusion equation (13.36), propagating the initial solution u0[] over the time interval h t according to Formulas 13.46 through 13.48 obtained by applying the explicit FTCS discretization scheme. The constant diffusion coefficient, the spatial step size, and the number of nodes are received via arguments D, h x, and, respectively, n x, and the propagated solution is returned by means of the array u[]. The driving sequence in the main program is supposed to perform any additional processing and, above all, to free the array u[] for a new propagation step by saving its content to u0[].

A typical main program is included in Listing 13.7. The code first initializes the solution u0[] by a call to the user function Init and then controls the propagation within a temporal loop by repeated calls to PropagFTCS, each followed necessarily by a backward transfer of content from u[] to u0[].

The solution of the diffusion equation (13.36) by the explicit FTCS method is prone to a particular numerical phenomenology, being confronted under certain conditions with severe numerical instability. The instability implies that, instead of smooth, well-behaved spatial profiles, the propagation develops spurious oscillations, which grow exponentially in time, distorting the solution irrecoverably. This critical behavior is due to the increasing domination of the roundoff errors and always arises when the time step size exceeds a certain upper bound, which correlates with the employed spatial step size.

# Listing 13.6 Explicit FTCS Propagator for the Diffusion Equation (Python Coding)

```
# ============================================================================
def PropagFTCS(u0, u, nx, D, hx, ht):
# ----------------------------------------------------------------------------
# Propagates the solution u0[] of the diffusion equation
#   du/dt = D d2u/dx2,  D - diffusion coefficient (constant)
# over the time interv at ht, using an explicit FTCS difference scheme on
# a spatial grid with nx nodes and spacing hx. Returns the solution in u[].
# ----------------------------------------------------------------------------
lam = D * ht/(hx*hx)
lam1 = 1e0 - 2e0*lam

u[1] = u0[1]; u[nx] = u0[nx]
for i in range(2,nx):
    u[i] = lam*u0[i-1] + lam1*u0[i] + lam*u0[i+1]
```