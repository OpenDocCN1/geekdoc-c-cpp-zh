
```
```python
out = open("diffusion.txt","w")
out.write("      x      ")
for i in range (1,nx+1): out.write("{0:10.5f}".format(x[i]))   # print x-mesh
out.write("\n")
out.write("      t        u\n")

for it in range (1,nt+1):                                      # time loop
    t = it*ht                                                # propagate solution
    PropagDiff(u0,u,D,nx,hx,ht,iopBC1,iopBC2,Jdiff1,Jdiff2)

    for i in range (1,nx+1): u0[i] = u[i]                     # shift solutions

    if (it % nout == 0 or it == nt):                          # output every nout steps
        out.write("{0:10.5f}".format(t))
        for i in range (1,nx+1): out.write("{0:10.5f}".format(u[i]))
        out.write("\n")

        GraphClear()
        title = "Diffusion t = {0:4.2f}".format(t)
        Plot(x,u,nx,"blue",1,0.15,0.95,0.50,0.90,"None","u",title)
        Plot(x,D,nx,"red",1,0.15,0.95,0.08,0.48,"x","D","")
        GraphUpdate()
out.close()

MainLoop()
```
```

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_599_0.png)

**FIGURE 13.20** Solution of the discretized diffusion problem 13.157–13.160 and spatial distribution of the diffusion coefficient (lower panel) for a stack of three layers at time *t* = 2.0 (for Problem 13.6).

# PROBLEM 13.7

Investigate the time evolution of the quantum Gaussian wave packet

Ψ(x, 0) = 1 / sqrt((2π)^{1/2} σ) e^{-(x - x0)^2 / (4σ^2)} e^{i k0 x}, (13.161)

scattered by the square potential

V(x) = { V0, |x| ≤ a/2; 0, |x| > a/2. } (13.162)

Employ the Crank–Nicolson scheme for discretizing the Schrödinger equation and the LU factorization technique for tridiagonal systems described in the main text and implemented in routine PropagQTD. Build Python and C/C++ codes similar to program 13.14, adding graphic capabilities to visualize the probability density profiles.

Set ħ = 1 and m = 1, and consider for the potential barrier the parameters a = 5 and V0 = 25, and for the wave packet, the initial position x0 = −20, the half-width σ = 1, and the average wave vector k0 = 10 (the energy is ħ²k0²/2m = 2V0). Use a spatial grid in the range (−xmax, xmax), with xmax = 100 and nodes spaced regularly by hx = 5·10⁻². Propagate the wave packet up to tmax = 5, with a time step ht = 5·10⁻³.

Print and plot the probability density every nout = 40 time steps. Discuss the change in the final distribution of the probability density in relation to the case presented in the main text, in which the total energy was equal to the barrier height (V0 = 50).

# Solution

The Python implementation is presented in Listing 13.24 and the C/C++ version is available as supplementary material (P13-ScatterQTD1.cpp). Snapshots of the time evolution of the probability density of the wave packet are shown in Figure 13.21.

# Listing 13.24 Scattering of a Quantum Wave Packet by a Potential Barrier (Python Coding)

```
# Reflexion/transmission of quantum wave packet using tridiagonal solver
from math import *
from cmath import *
from pde import *
from graphlib import *

def Pot(x, a, V0):
    return V0 if fabs(x) <= 0.5e0*a else 0e0

# Potential
#================================================================================
def Init(Psi, x, nx, x0, sig, k0):
#--------------------------------------------------------------------------------
#  Initial Gaussian wave packet
#     Psi(x,0) = 1/sqrt(sqrt(2*pi)*sig) * exp[-(x-x0)^2/(4*sig^2)] * exp(ikx)
#  x0 - position of center, sig - half-width, k0 - average wave number
#--------------------------------------------------------------------------------
    a = 1e0/sqrt(sqrt(2e0*pi)*sig)
    b = -1e0/(4e0*sig*sig)
    for i in range(1,nx+1):
        dx = x[i] - x0
        f = a * exp(b*dx*dx)
        if (f < 1e-10): f = 0e0
        Psi[i] = f * complex(cos(k0*x[i]),sin(k0*x[i]))
#================================================================================
```

```
def ProbDens(Psi, Psi2, nx, hx):
#-------------------------------------------------------------------------------
# Calculates the probability density Psi2[] of the wave function Psi[]
#-------------------------------------------------------------------------------
    for i in range(1,nx+1):
        Psi2[i] = abs(Psi[i])*abs(Psi[i])      # unnormalized probability density
        if (Psi2[i] <= 1e-10): Psi2[i] = 0e0

    PsiNorm = 0.5e0*(Psi2[1] + Psi2[nx])          # integral by trapezoidal rule
    for i in range(2,nx): PsiNorm += Psi2[i]
    PsiNorm *= hx

    for i in range(1,nx+1): Psi2[i] /= PsiNorm      # normalized prob. density
    return PsiNorm

# main

a    = 5e0                                   # width of potential barrier
V0   = 25e0                                 # height of potential barrier
x0   = -20e0                                # initial position of wave packet
sig  = 1e0                                  # half-width of packet
k0   = 10e0                                 # average wave number of packet
xmax = 100e0                                # maximum x
hx   = 5e-2                                 # spatial step size
tmax = 5e0                                  # maximum propagation time
ht   = 5e-3                                 # time step
nout = 40                                   # output every nout steps

nx = 2*(int)(xmax/hx + 0.5) + 1             # odd number of spatial nodes
nt = (int)(tmax/ht + 0.5)                   # number of time steps
nx2 = int(nx/2); nx4 = int(nx/4) + 1

Psi  = [complex(0,0)]*(nx+1)                # wave function
Psi2 = [0]*(nx+1)                           # probability density
V    = [0]*(nx+1)                           # potential
x    = [0]*(nx+1)                           # spatial mesh

for i in range(1,nx+1):                     # tabulate spatial mesh and potential
    x[i] = (i-nx2-1)*hx
    V[i] = Pot(x[i],a,V0)

Init(Psi,x,nx,x0,sig,k0)                    # initial wave packet

GraphInit(1000,700)

for it in range(1,nt+1):                    # time loop
    t = it*ht
    PropagQTD(Psi,V,nx,hx,ht)               # propagate solution by tridiagonal solver

    PsiNorm = ProbDens(Psi,Psi2,nx,hx)      # probability density

    if (it % nout == 0 or it == nt):        # output every nout steps
        fname = "scatter_{0:4.2f}.txt".format(t)
        out = open(fname,"w")
        out.write("t = {0:4.2f}\n".format(t))
        out.write("     x          V          PsiR        PsiI        Psi2\n")
        for i in range(1,nx+1):
            out.write("{0:10.5f}{1:10.5f}{2:10.5f}{3:10.5f}\n".\
                    format(x[i],V[i],Psi[i].real,Psi[i].imag,Psi2[i]))
```

```
out.close

GraphClear()
title = "Scattering of wave packet  t = {0:4.2f}".format(t)
Plot(x[nx4:],Psi2[nx4:],nx2,"blue",1,0.15,0.95,0.50,0.90,
"None","Psi2",title)
Plot(x[nx4:],V[nx4:],nx2,"red",1,0.15,0.95,0.08,0.48,"x","V","")
GraphUpdate()

MainLoop()
```

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_602_0.png)

FIGURE 13.21 Scattering of a quantum Gaussian wave packet by a square potential, calculated by Program 13.14, using the LU decomposition technique implemented in routine PropagQTD. Upper panel: the energy is equal to twice the barrier height, V0 = 25. Lower panel: the energy is equal to the absolute value of the well depth, V0 = −50 (for Problem 13.7).

# PROBLEM 13.8

Solve the classical wave equation

∂²u/∂t² = c² ∂²u/∂x²,  t > 0,  (13.163)

for the initial wave packet

u(x,0) = sin xΔk / (xΔk),  −x_max ≤ x ≤ x_max,  (13.164)

with the initial time derivative (∂u/∂t)(x,0) = 0 and satisfying the Dirichlet boundary conditions

u(±x_max,t) = sin x_max Δk / (x_max Δk),  t > 0.  (13.165)

Consider the phase velocity c = 10 and the domain extent x_max = 100, and propagate the solution with the step sizes h_x = 5 · 10^-2 and h_t = 5 · 10^-3 up to t_max = 40. Verify that the chosen parameters satisfy the von Neumann stability condition.

For shaping the initial wave packet, use comparatively the wave number interval widths Δk = 0.5, 1, and 5. Discuss the effect of changing Δk and use in each case the amplitude of the final wave packet, which is reconstructed at the origin, to obtain an error estimate. Correlate the error estimates with the half-widths of the initial wave packets.

Print and plot the output every n_out = 500 time steps.

# Solution

The Python implementation is presented in Listing 13.25 and the C/C++ version is available as supplementary material (P13-Wave.cpp). Snapshots of the time evolution of the wave packets for Δk = 0.5 and Δk = 5 are shown in Figures 13.22 and 13.23.

# Listing 13.25 Finite-Difference Solution of the Classical Wave Equation (Python Coding)

```
# Solve 1D wave equation by the explicit finite-difference method
from math import *
from pde import *
from graphlib import *

#===============================================================================
def Init(u0, u1, x, nx, c, dk, hx, ht):
#-------------------------------------------------------------------------------
#   Returns initial solutions u0 and u1, for the first two time steps
#       u0(x,0) = sin(x*dk) / (x*dk)                     initial solution
#       v0(x,0) = 0                                      initial time derivative
#   x - spatial mesh, nx - number of nodes
#   c - phase velocity of wave, dk - wave number interval
#   hx - x-spacing, ht - time step size
#-------------------------------------------------------------------------------
    for i in range(1,nx+1):                                 # time step 0
        u0[i] = sin(dk*x[i])/(dk*x[i]) if dk*x[i] else 1e0   # initial solution

    lam = c*ht/hx; lam = lam*lam                            # time step 1
    lam2 = 2e0*(1e0 - lam)
    u1[1] = u0[1]; u1[nx] = u0[nx]                           # constant boundary values
    for i in range(2,nx):
        v0 = 0e0                                            # initial time derivative
        u1[i] = 0.5e0*(lam*u0[i-1] + lam2*u0[i] + lam*u0[i+1]) - ht*v0

# main

c     = 10e0                                                # phase speed of wave
dk    = 1e0                                                 # wave number interval
xmax  = 100e0                                               # maximum x
hx    = 5e-2                                                # spatial step size
tmax  = 40e0                                                # maximum propagation time
ht    = 5e-3                                                # time step
nout  = 500                                                 # output every nout steps

nx = 2*(int)(xmax/hx + 0.5) + 1                             # odd number of spatial nodes
nt = (int)(tmax/ht + 0.5)                                   # number of time steps
nx2 = int(nx/2)

u0 = [0]*(nx+1)                                            # initial solution
u1 = [0]*(nx+1)                                            # first propagated solution
u  = [0]*(nx+1)                                            # solution
```
