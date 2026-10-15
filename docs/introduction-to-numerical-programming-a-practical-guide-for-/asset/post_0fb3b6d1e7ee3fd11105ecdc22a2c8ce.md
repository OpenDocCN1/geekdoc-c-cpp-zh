
(P12-ThrowECg.py and P12-ThrowECg.cpp), and those based on the Verlet method (P12-ThrowVg.py and P12-ThrowVg.cpp). Typical graphical output for the laminar-separated flow is shown in Figure 12.11.

## Listing 12.22 Hammer Throw Using Euler's Predictor–Corrector Method (Python Coding)

```
# Oblique throw of an object with drag using the Euler PC method
from math import *
from ode import *
from graphlib import *

g = 9.81e0                                      # gravitational acceleration

def Func(t, y, f):                             # RHSs of 1st order ODEs for oblique throw
    f[1] = y[3]                                 # y[1] = x, y[2] = y, y[3] = vx, y[4] = vy
    f[2] = y[4]
    f[3] = -k/m * y[3]*fabs(y[3])
    f[4] = -k/m * y[4]*fabs(y[4]) - g

# main

m = 7.26e0                                      # mass of hammer
R = 0.06e0                                      # radius of hammer
x0 = 0e0; y0 = 3e0                              # initial position
v0 = 29e0                                       # initial velocity
phi = 45e0 * pi/180e0                           # throw angle
vx0 = v0 *cos(phi); vy0 = v0*sin(phi)           # initial velocity
rho = 1.2                                       # density of air
Cd = 0.5e0                                      # drag coefficient
k = 0.5e0*rho*(pi*R*R)*Cd                       # velocity coefficient
tmax = 20e0                                     # time span
ht = 0.001e0                                   # time step size

n = 4                                           # number of 1st order ODEs
nt = int(tmax/ht + 0.5) + 1                     # number of time steps
y = [0]*(n+1)                                   # solution components
tt = [0]*(nt+1); xt = [0]*(nt+1); yt = [0]*(nt+1) # plotting arrays

t = 0e0; it = 1
 y[1] = x0; y[3] = vx0                           # initial values
y[2] = y0; y[4] = vy0
tt[it] = t; xt[it] = y[1]; yt[it] = y[2]         # store for plotting

while (t+ht <= tmax):                           # propagation loop
    EulerPC(t,ht,y,n,Func)
    t += ht; it += 1

    tt[it] = t; xt[it] = y[1]; yt[it] = y[2]     # store for plotting
    if (y[2] < 0.e0): break                     # stop if object hits the ground

print("xmax = {0:5.2f}".format(y[1]))

GraphInit(1200,600)
Plot(tt,yt,it,"blue",1,0.10,0.45,0.15,0.85,"t","y","Altitude")
Plot(xt,yt,it,"blue",1,0.60,0.95,0.15,0.85,"x","y","Trajectory")
MainLoop()
```

## PROBLEM 12.3

Consider a particle of mass m = 1 u (unified atomic mass units), carrying the elementary charge q = −e, which orbits around a fixed charge Q = e, located at the origin. The initial position of the particle is x0 = 1 Å and y0 = 0 and its velocity components are vx0 = 0 and vy0 = 4.5 Å/ps.

## Listing 12.23 Orbiting Charged Particle Using Euler’s Predictor–Corrector Method (Python Coding)

```
# Charged particle orbiting about a fixed charge - Euler PC method
from math import *
from ode import *
from graphlib import *

def Func(t, y, f):                     # RHS of 1st order ODEs
    factCoul = 14.3996517e0            # e**2/(4*pi*eps0) [eV*A]
                                     # charge: e, energy: eV, force: eV/A
    r2 = y[1]*y[1] + y[2]*y[2]          # mass: u, distance: A, time: ps
    r = sqrt(r2)                       # distance from force center
    fr = factCoul * q * Q / r2         # radial force
    f[1] = y[3]
    f[2] = y[4]
    f[3] = fr/m * y[1]/r
    f[4] = fr/m * y[2]/r

# main

m = 1e0                                # mass of particle
q = -1.e0; Q = 1.e0                    # charges in units of e
x0 = 1e0; y0 = 0e0                     # initial position
vx0 = 0e0; vy0 = 4.5e0                 # initial velocity
tmax = 20e0                            # time span
ht = 0.01e0                           # time step size

n = 4                                  # number of 1st order ODEs
nt = int(tmax/ht + 0.5) + 1            # number of time steps
y = [0]*(n+1)                          # solution components
tt = [0]*(nt+1); xt = [0]*(nt+1); yt = [0]*(nt+1)  # plotting arrays

t = 0e0; it = 1
 y[1] = x0; y[3] = vx0                  # initial values
y[2] = y0; y[4] = vy0
tt[1] = t; xt[1] = y[1]; yt[1] = y[2]   # store for plotting

while (t+ht <= tmax):                  # propagation loop
    EulerPC(t,ht,y,n,Func)
    t += ht; it += 1

    tt[it] = t; xt[it] = y[1]; yt[it] = y[2]  # store for plotting

GraphInit(1200,600)

Plot(tt,xt,it,"blue",1,0.10,0.45,0.15,0.85,
     "t","y","x-position of charged particle")
Plot(xt,yt,it,"blue",1,0.60,0.95,0.15,0.85,
     "x","y","Trajectory of charged particle")

MainLoop()
```

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_506_0.png)

FIGURE 12.12 Time dependence of the x-position and trajectory of a charged particle orbiting about a fixed charge, calculated using the Euler predictor–corrector method (for Problem 12.3).

Propagate the trajectory of the particle up to t_max = 20 ps using the Euler predictor–corrector method with a time step h = 0.01. Plot the time dependence of the particle’s x-position and its trajectory. Assess the stability of the orbit, and determine its defining axes and the orbital period.

## Solution

The Coulomb force components are

F_x = K (qQ x)/(r^2 r),   F_y = K (qQ y)/(r^2 r),

where K = e^2/(4π) = 14.3996517 eV/Å.

The Python program is given in Listing 12.23, while the C/C++ implementation is available as supplementary material (P12-ODEg.cpp). The graphical representations produced by the program for the time dependence of the particle’s x-position and for its trajectory are shown in Figure 12.12.

## PROBLEM 12.4

Consider the previous problem of the orbiting charged particle and use comparatively the Euler and Euler–Cromer methods for second-order ODEs with the time step h = 0.01. Assess the stability of the two orbits, explain the qualitative difference between them, and determine the time step for which Euler’s method becomes stable, as well.

## Solution

The Python implementation is shown in Listing 12.24 and the C/C++ version is available as supplementary material (P12-ChargeEC.cpp). The charged particle’s trajectories are depicted in Figure 12.13.

## Listing 12.24  Orbiting Charged Particle Using the Euler–Cromer Method (Python Coding)

```
```python
# Charged particle orbiting about a fixed charge - Euler-Cromer method
from math import *
from ode import *
from graphlib import *

def Func(t, y, dy, f):                                      # RHS of 2nd order ODEs
    factCoul = 14.3996517e0                                  # e**2/(4*pi*eps0) [eV-A]
                                                              # charge: e, energy: eV, force: eV/A
    r2 = y[1]*y[1] + y[2]*y[2]                                # mass: u, distance: A, time: ps
    r = sqrt(r2)                                               # distance from force center
    fr = factCoul * q * Q / r2                                 # radial force
    f[1] = fr/m * y[1]/r
    f[2] = fr/m * y[2]/r

# main

m = 1e0                                                     # mass of particle
q = -1.0e0; Q = 1.e0                                        # charges in units of e
x0 = 1e0; y0 = 0e0                                          # initial position
vx0 = 0e0; vy0 = 4.5e0                                      # initial velocity
tmax = 20e0                                                 # time span
ht = 0.01e0                                                 # time step size

n = 2                                                        # number of 2nd order ODEs
nt = int(tmax/ht + 0.5) + 1                                 # number of time steps
y = [0]*(n+1); dy = [0]*(n+1)                                # solution components
xt = [0]*(nt+1); yt = [0]*(nt+1)                             # plotting arrays

GraphInit(1200,600)

t = 0e0; it = 1                                               # Euler method
y[1] = x0; dy[1] = vx0                                      # initial values
y[2] = y0; dy[2] = vy0
xt[1] = y[1]; yt[1] = y[2]                                   # store for plotting
while (t+ht <= tmax):                                        # propagation loop
    Euler2(t,ht,y,dy,n,Func)
    t += ht; it += 1
    xt[it] = y[1]; yt[it] = y[2]                              # store for plotting

Plot(xt,yt,it,"red",1,0.10,0.45,0.15,0.85,
     "x","y","Trajectory of charged particle - Euler")

t = 0e0; it = 1                                               # Euler-Cromer method
y[1] = x0; dy[1] = vx0                                      # initial values
y[2] = y0; dy[2] = vy0
xt[1] = y[1]; yt[1] = y[2]                                   # store for plotting
while (t+ht <= tmax):                                        # propagation loop
    EulerCromer(t,ht,y,dy,n,Func)
    t += ht; it += 1
    xt[it] = y[1]; yt[it] = y[2]                              # store for plotting

Plot(xt,yt,it,"blue",1,0.60,0.95,0.15,0.85,
     "x","y","Trajectory of charged particle - Euler-Cromer")

MainLoop()
```
```
