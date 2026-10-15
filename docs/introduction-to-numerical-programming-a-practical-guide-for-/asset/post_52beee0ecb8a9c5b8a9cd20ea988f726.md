
```
    us = u[1]                                      # save solution

    tt[it] = t; ut[it] = u[1]; vt[it] = u[2]              # store for plotting

    T = 2e0 * (t2-t1) / nT                              # calculated period
    T0 = 2e0*pi*sqrt(1/g)                               # harmonic period
    Tex = 2/pi * T0 * K(el(pow(sin(0.5e0*u0),2))       # exact period
    print("u0 = {0:7.5f}  T/T0 = {1:7.5f} + ({2:7.1e})". \
          format(u0,T/T0,(Tex-T)/T0))

    GraphInit(1200,600)

    Plot(tt,ut,it,"blue",1,0.10,0.45,0.15,0.85, \
         "t (s)","u (rad)","Displacement of nonlinear pendulum")
    Plot(ut,vt,it,"blue",1,0.60,0.95,0.15,0.85, \
         "u (rad)","u' (rad/s)","Trajectory of pendulum in phase space")

    MainLoop()
```

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_512_0.png)

**FIGURE 12.15**  Time dependence of the angular displacement of a nonlinear pendulum and its trajectory in the phase space, when started from an initial displacement equal to $\pi/2$ (for Problem 12.6).

## PROBLEM 12.7

Consider the previous problem for the nonlinear pendulum and propagate trajectories started from initial angular displacements $u_0 \in [0.1, 3.1]$ separated by 0.1. Plot the time dependences of the displacement, $u = u(t)$, for the lowest and the largest initial displacements and notice the significant differences both in period and in functional form. Plot the oscillation period as a function of the initial displacement, $T = T(u_0)$, and compare the dependence with the exact result (Equation 12.114).

### Solution

The Python implementation is given in Listing 12.27 and the C/C++ variant is provided as supplementary material (P12-PendulumRKT.cpp). The time dependences of the pendulum’s angular displacement and the dependence of the period on the initial displacement are displayed in Figure 12.16.

## Listing 12.27 Oscillations of a Nonlinear Pendulum by the Runge–Kutta Method (Python Coding)

```
# Angular motion of a nonlinear pendulum by the Runge-Kutta method
#   u'' = -g/l * sin(u) - k * u',    u(0) = u0, u'(0) = u0'
from math import *
from ode import *
from integral import *
from graphlib import *

g = 9.81e0                                          # gravitational acceleration

def Func(t, u, f):                                  # RHS of 1st order ODEs
    f[1] = u[2]                                      # u[1] = u, u[2] = u'
    f[2] = -g/l * sin(u[1]) - k * u[2]

#================================================================================
def Kel(m):
#--------------------------------------------------------------------------------
#  Returns the complete elliptic integral of the 1st kind
#  Calls: qImprop2 (integral.py)
#--------------------------------------------------------------------------------
eps = 1e-7                                          # relative precision
def fKel(z): return 1e0 / sqrt((1e0-z*z)*(1e0-m*z*z))      # integrand
return qImprop2(fKel,0e0,1e0,eps)

# main

nn = [0]*3                                          # ending indexes of plots
col = [""]*3                                       # colors of plots
sty = [0]*3                                         # styles of plots

l = 1e0                                             # pendulum length
k = 0e0                                             # velocity coefficient
du0 = 0e0                                           # initial derivative
tmax = 20e0                                         # time span
ht = 0.001e0                                        # time step size
u0min = 0.1e0                                      # minimum u0
u0max = 3.1e0                                      # maximum u0
hu = 0.1e0                                          # increment for u0

n = 2                                               # number of 1st order ODEs
nt = int(tmax/ht + 0.5) + 1                         # number of time steps
nu = int((u0max-u0min)/hu + 0.5) + 1                # number of u0s
u = [0]*(n+1)                                       # solution components
tt = [0]*(2*nt+1); ut = [0]*(2*nt+1)                # arrays for t-dep. plots
tu = [0]*(2*nu+1); uu = [0]*(2*nu+1)                # arrays for u0-dep. plots

for iu in range(1,nu+1):
    u0 = u0min + (iu-1)*hu                          # initial displacement

    t = 0e0; it = 1
    u[1] = u0; u[2] = du0                            # initial values
    if (iu == 1 ): tt[1  ] = t; ut[1  ] = u[1]        # for smallest u0
    if (iu == nu): tt[1+nt] = t; ut[1+nt] = u[1]      # for largest u0

    nT = 0                                          # number of half-periods
    t1 = t2 = 0e0                                   # bounding solution zeros
    us = u[1]                                       # save solution
    while (t+ht <= tmax):                           # propagation loop
        RungeKutta(t,ht,u,n,Func)
```

```
t += ht; it += 1

if (u[1]*us < 0e0):                 # count solution passages through zero
    if (t1 == 0): t1 = t             # initial zero
    else: t2 = t; nT += 1            # final zero
us = u[1]                            # save solution
                                      # store for plotting
if (iu == 1): tt[it    ] = t; ut[it    ] = u[1]       # for smallest u0
if (iu == nu): tt[it+nt] = t; ut[it+nt] = u[1]       # for largest u0

T = 2e0*(t2-t1) / nT                 # calculated period
T0 = 2*pi*sqrt(1/g)                   # harmonic period
Tex = 2/pi * T0 * Kel(pow(sin(0.5e0*u0),2))           # exact period

uu[iu    ] = u0; tu[iu    ] = T/T0
uu[iu+nu] = u0; tu[iu+nu] = Tex/T0

GraphInit(1200,600)

nn[1] = it    ; col[1] = "blue"; sty[1] = 1          # for smallest u0
nn[2] = it+nt ; col[2] = "red" ; sty[2] = 1          # for largest u0
MultiPlot(tt,ut,ut,nn,col,sty,2,10,0e0,0e0,0,0e0,0e0,0,0.10,0.45,0.15,0.85, \
          "t (s)","u (rad)","Displacement of nonlinear pendulum")

nn[1] = nu; col[1] = "red" ; sty[1] = 0                # calculated periods
nn[2] = 2*nu; col[2] = "blue"; sty[2] = 1             # exact periods
MultiPlot(uu,tu,tu,nn,col,sty,2,10,0e0,0e0,0,0e0,0e0,0,0.60,0.95,0.15,0.85, \
          "u0 (rad)","T/T0","Period of nonlinear pendulum")

MainLoop()
```

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_514_0.png)

**FIGURE 12.16** Time dependences of the angular displacement of a nonlinear pendulum for initial displacements equal to 0.1 and, respectively, 3.1, and dependence of the period on the initial displacement $u_0 \in [0.1, 3.1]$ (for Problem 12.7).

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_515_0.png)

FIGURE 12.17 Phase space trajectories of a nonlinear pendulum of length l = 1, displaced initially by u0 = π/2, as yielded by the Euler and Euler–Cromer methods with a time step h = 0.01 s (for Problem 12.8).

## PROBLEM 12.8

Consider again the problem of the nonlinear pendulum of length l = 1 m displaced initially by u0 = π/2. Use comparatively the Euler method for second-order ODEs (routine Euler1) and the Euler–Cromer method (routine EulerCromer1) to propagate the solution up to tmax = 20 s, with a time step h = 0.01 s. For both methods, plot the phase space trajectory of the pendulum and comment on the qualitative difference between their stability properties.

### Solution

The Python and C/C++ implementations are provided as supplementary material (P12-PendulumECg.py and P12-PendulumECg.cpp). The phase space trajectories of the nonlinear pendulum for the Euler and Euler–Cromer methods are depicted in Figure 12.17.

## PROBLEM 12.9

Consider the relative motion of the Moon around the Earth in the common center-of-mass system, under the influence of its gravitational interaction force

F = G (m1 m2)/r12.

G = 6.67384 · 10^-11 m³/kg · s² is the gravitational constant, m1 = 5.97 · 10^24 kg is the Earth’s mass, m2 = 7.35 · 10^22 kg is the Moon’s mass, and r12 is the distance between them.

- a. Place initially the Earth at rest at the origin and the Moon at the approximate apogee (largest) distance d0 = 4.06 · 10^8 m, with a perpendicular relative velocity v0 = 960 m/s.* Use the routine MovetoCM (from the module coords.py given in Listing 8.10, or from the header file coords.h) to move the planets to their center-of-mass system and also to cancel their total momentum, by passing velocities instead of positions to the routine.

* http://solarsystem.nasa.gov/planets/profile.cfm?Object=Moon
