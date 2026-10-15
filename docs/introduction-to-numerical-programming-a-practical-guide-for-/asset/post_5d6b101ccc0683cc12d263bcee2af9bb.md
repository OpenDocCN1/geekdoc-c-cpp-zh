
![](img/5c6c126e3d8cf2b3029f4242e9ad2887_508_0.png)

**FIGURE 12.13** Trajectories of a charged particle orbiting about a fixed charge, as calculated using the Euler and Euler–Cromer methods (for Problem 12.4).

## PROBLEM 12.5

Consider the previous problem of the orbiting charged particle and use for propagation the Verlet algorithm with the (rather large) time step *h* = 0.1. Plot the kinetic, potential, and total energies, as well as the particle’s trajectory. Identify the aspects that accompany the occurrence of instability. Decrease the time step to *h* = 0.01 and observe the qualitative changes in the total energy and the particle’s trajectory.

## Solution

The Python implementation is provided in Listing 12.25 and the C/C++ version is available as supplementary material (P12–ChargeV.cpp). The charged particle’s energies and trajectory are plotted in Figure 12.14.

**Listing 12.25** Orbiting Charged Particle Using the Verlet Method (Python Coding)

```python
# Charged particle orbiting about a fixed charge - Verlet method
from math import *
from ode import *
from graphlib import *


def Forces(m, x, y, vx, vy):
    factCoul = 14.3996517e0                 # e**2/(4*pi*eps0) [eV*A]
                                             # charge: e, energy: eV, force: eV/A
    r2 = x*x + y*y                          # mass: u, distance: A, time: ps
    r = sqrt(r2)                            # distance from force center
    fr = factCoul * q * Q / r2              # radial force
    fx = fr * x/r                           # force components
    fy = fr * y/r
    Epot = fr * r                           # potential energy
    return (fx, fy, Epot)

# main

nn  = [0]*4; sty = [0]*4                   # end-indexes, styles of plots
col = ["w"]*4                             # colors of plots
```

```
m = 1e0                                                                 # mass of particle
q = -1.e0; Q = 1.e0                                                      # in units of e
x0 = 1e0; y0 = 0e0                                                       # initial position
vx0 = 0e0; vy0 = 4.5e0                                                    # initial velocity
tmax = 20e0                                                              # time span
ht = 0.1e0                                                               # time step size

nt = int(tmax/ht + 0.5) + 1                                              # number of time steps
tt = [0]*(3*nt+1); Et = [0]*(3*nt+1)                                      # plotting arrays
xt = [0]*(nt+1); yt = [0]*(nt+1)

t = 0e0; it = 1
x = x0; vx = vx0                                                         # initial values
y = y0; vy = vy0

(fx, fy, Epot) = Forces(m,x,y,vx,vy)                                     # initial forces and potential energy
ax = fx/m; ay = fy/m                                                      # initial acceleration
Ekin = 0.5e0 * m * (vx*vx + vy*vy)                                        # initial kinetic energy
xt[it] = x; yt[it] = y                                                    # store for plotting
tt[it] = tt[nt+it] = t; tt[2*nt+it] = t
Et[it] = Ekin; Et[nt+it] = Epot; Et[2*nt+it] = Ekin + Epot

while (t < tmax):                                                        # propagation loop
    (x,y,vx,vy,ax,ay,Ekin,Epot) = Verlet2(ht,m,x,y,vx,vy,ax,ay,Forces)
    t += ht; it += 1

    xt[it] = x; yt[it] = y                                                # store for plotting
    tt[it] = tt[nt+it] = t; tt[2*nt+it] = t
    Et[it] = Ekin; Et[nt+it] = Epot; Et[2*nt+it] = Ekin + Epot

GraphInit(1200,600)

nn[1] = nt; col[1] = "blue"; sty[1] = 1                                   # Ekin
nn[2] = 2*nt; col[2] = "green"; sty[2] = 1                               # Epot
nn[3] = 3*nt; col[3] = "red"; sty[3] = 1                                 # Etot
MultiPlot(tt,Et,nn,col,sty,3,10,0e0,0e0,0,0e0,0e0,0,
          0.10,0.45,0.15,0.85,"t","Ek,Ep,Et","Energies of charged particle")
Plot(xt,yt,nt,"blue",1,0.60,0.95,0.15,0.85,
     "x","y","Trajectory of charged particle")

MainLoop()
```

## PROBLEM 12.6

Consider the equation of motion for the angular displacement $u$ of a nonlinear rigid pendulum of length $l$ ($g$ is the gravitational acceleration):

$$u'' = -\frac{g}{l} \sin u, \tag{12.112}$$

with the initial conditions:

$$u(0) = u_0, \quad u'(0) = 0. \tag{12.113}$$

The period of oscillations of arbitrary amplitude explicitly depends on the initial displacement $u_0 \in [-\pi, \pi]$ (Beléndez et al. 2007):

$$T = T_0 \frac{2}{\pi} K\left(\sin^2 \frac{u_0}{2}\right). \tag{12.114}$$

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_510_0.png)

FIGURE 12.14 Time dependence of the kinetic, potential, and total energies and trajectory of a charged particle orbiting about a fixed charge, using the Verlet method (for Problem 12.5).

Here

```
$T_0 = 2\pi \sqrt{\frac{l}{g}}$
```

is the harmonic period, specific for the limit of vanishing amplitudes, and $K(m)$ is the complete elliptic integral of the first kind, defined as (Abramowitz and Stegun 1972)

```
$K(m) = \int_{0}^{1} \frac{dz}{\sqrt{(1 - z^2)(1 - m z^2)}}.$
(12.115)
```

- a. Write a routine to calculate the elliptic integral $K(m)$ based on its definition and use the function Improp2 (defined in integral.py or integral.h) to evaluate the involved improper integral of the second kind (having a singular integrand at one of the boundaries; see Section 10.8).
- b. Consider a pendulum of length $l = 1$ m and an initial angular displacement $u_0 = \pi/2$. Use the Runge–Kutta method to propagate the dynamic state up to $t_{max} = 20$ s, with a time step $h = 0.001$ s. Determine the number of half-periods covered by the propagation by counting the zeros (sign changes) of the solution and, from the time span between the first and the last zero, calculate the oscillation period and compare it with the exact value.
- c. Plot the time dependence of the displacement to verify the determined period qualitatively. Plot the trajectory of the pendulum in the phase space, $u' = u'(u)$, to check the stability of the solution visually.

## Solution

To apply the Runge–Kutta method, the equation of the pendulum is transformed into a system of first-order ODEs:

```
$\begin{cases} u'_1 = u_2, \\ u'_2 = -(g/l)\sin(u_1) - k u_2, \end{cases}\qquad \begin{cases} u_1(0) = u_0, \\ u_2(0) = 0. \end{cases}$
```

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
