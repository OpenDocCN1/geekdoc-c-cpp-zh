# Non-Linear Differential Equations and Dynamical Systems

and a necessary and sufficient condition is that it zero curl (4.438c) as follows from: (i) the two-dimensional form (subsection III.5.8.1) of the theorem on irrotational flows (III.5.240-d) = (4.438a-c); and (ii) the condition (subsection 3.8.1) that $d\Phi$ is an exact differential (3.153a-d = (4.438a-c). A dynamical system is conservative if there is a conserved quantity (4.439a):

```
$E(x, \dot{x}) = const; \quad \ddot{x} = -rac{\partial\Phi}{\partial x}, \quad E = \frac{\dot{x}^2}{2} + \Phi(x), \quad (4.439a-c)$
```

for example, a force depending on position (4.439b) leads to the conservation of energy (4.439c) as follows:

```
$0 = \dot{x} \left(\\ddot{x} + \frac{\partial\Phi}{\partial x}\right) = x\ddot{x} + \frac{\partial\Phi}{\partial x}\frac{dx}{dt} + \left(\frac{\dot{x}^2}{2} + \Phi\right)\frac{dE}{dt} = 0 \quad (4.439d)$
```

Taking as example the linear second-order system with constant coefficients (4.437b) = (4.440a), it follows (4.440b):

```
$\ddot{x} = -2\lambda\dot{x} - \omega_x^2x; \quad -4\lambda^2x = 2\dot{x}(\ddot{x} + \omega_x^2x) = \frac{d}{dt}(\dot{x}^2 + \omega_x^2x), \quad (4.440a, b)$
```

that the system is conservative (4.441b) only if there is no damping or amplification (4.441a):

```
$\lambda = 0; \quad const = x^2 + \omega_x^2x = 2E. \quad (4.441a, b)$
```

The main motivation for the consideration of bifurcations of dynamical systems (subsections 4.8.1–4.8.3) is the non-linear cases addressed next (subsections 4.8.4–4.8.9):

# 4.8.4 Non-Linear Perturbation of a Spiral Flow

A constant angular velocity (4.442a) and linear radial velocity (4.442b) form a linear dynamical system (4.442c) corresponding to section I.12.6) to a spiral flow (4.442d):

```
$$\frac{d\theta}{dt} = \Omega = const, \quad \frac{dr}{dt} = qr = \frac{q}{\Omega}r,\quad \Omega\log r - q = const. \quad (4.442a–d)$
```

The general non-linear perturbation of (4.443a), corresponding to a gradient dynamical system is:

```
$$\frac{d\theta}{dt} = \Omega + \frac{\partial\Phi}{\partial t}, \quad \frac{dr}{dt} = qr + \frac{\partial\Phi}{\partial r}. \quad (4.443a, b)$
```