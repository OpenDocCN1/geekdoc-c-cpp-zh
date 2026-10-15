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