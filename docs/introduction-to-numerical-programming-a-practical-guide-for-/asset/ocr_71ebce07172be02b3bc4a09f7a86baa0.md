The Python code is provided in Listing 12.26 and the C/C++ version is available as supplementary material (P12-PendulumRKg.cpp). The time dependence of the pendulum’s angular displacement and the trajectory in the phase space are shown in Figure 12.15. The found period, $T/T_0 = 1.18036$, is exact to five significant digits. The program also makes provisions for taking into account the drag on the pendulum.

**Listing 12.26**　Oscillations of a Nonlinear Pendulum by the Runge-Kutta Method (Python Coding)

```
```python
# Angular motion of a nonlinear pendulum by the Runge-Kutta method
#     u'' = -g/l * sin(u) - k * u',   u(0) = u0, u'(0) = u0'
from math import *
from ode import *
from integral import *
from graphlib import *

g = 9.81e0                                      # gravitational acceleration

def Func(t, u, f):                              # RHS of 1st order ODEs
    f[1] = u[2]                                 # u[1] = u, u[2] = u'
    f[2] = -g/l * sin(u[1]) - k * u[2]

#==========================================================================
def Kel(m):
#--------------------------------------------------------------------------
# Returns the complete elliptic integral of the 1st kind
# Calls: qImprop2 (integral.py)
#--------------------------------------------------------------------------
    eps = 1e-7                                   # relative precision
    def fKel(z): return 1e0 / sqrt((1e0-z*z)*(1e0-m*z*z))   # integrand
    return qImprop2(fKel,0e0,1e0,eps)

# main

l = 1e0                                         # pendulum length
k = 0e0                                         # velocity coefficient
u0 = 0.5e0*pi                                   # initial displacement
du0 = 0e0                                       # initial derivative
tmax = 20e0                                     # time span
ht = 0.001e0                                    # time step size

n = 2                                           # number of 1st order ODEs
nt = int(tmax/ht + 0.5) + 1                    # number of time steps
u = [0]*(n+1)                                   # solution components
tt = [0]*(nt+1); ut = [0]*(nt+1); vt = [0]*(nt+1)  # arrays for plotting

t = 0e0; it = 1
u[1] = u0; u[2] = du0                           # initial values
tt[1] = t; ut[1] = u[1]; vt[1] = u[2]           # store for plotting

nT = 0                                          # number of half-periods
t1 = t2 = 0e0                                   # bounding solution zeros
us = u[1]                                       # save solution
while (t+ht <= tmax):                            # propagation loop
    RungeKutta(t,ht,u,n,Func)
    t += ht; it += 1

    if (u[1]*us < 0e0):                          # count solution passages through zero
        if (t1 == 0): t1 = t                     # initial zero
        else: t2 = t; nT += 1                   # final zero
```
```