# Unsteady, Non-Linear, and Chaotic Systems

In the case of a force depending only on its position: (i) specifies the acceleration (4.429a), and (ii) derives from a potential (4.429b) specified to within an added constant (4.429c):

```
$\dot{x} = f(x;q) = -\frac{\partial\Phi(x;q)}{\partial x} \quad \Phi(x;q) = \int^x f(\xi;q)d\xi + C. \quad (4.429a-c)$
```

The equilibrium position(s) correspond to zero force (4.430a) [stationary position (4.430b)] and (i) the force has negative (positive) gradient (4.430c) [4.430e]; and (ii) the potential is minimum (4.430d) [maximum (4.430f):

```
$0 = f(\bar{x};q) = -\frac{\partial\Phi(\bar{x};q)}{\partial x} \quad \begin{cases} stable: &-\frac{\partial f}{\partial x}\frac{\partial^2\Phi}{\partial x^2} > 0, \ unstable: &-\frac{\partial f}{\partial x}\frac{\partial^2\Phi}{\partial x^2} < 0. \end{cases} \quad (4.430a-d)$
```

Next to be considered is the dependence of the equilibrium positions $ar{x}$ on the parameter(s) $q$ that leads to bifurcations and stability boundaries (section 4.8).

# 4.8.2 Equilibria, Bifurcations, and Stability Boundaries (Poincaré 1881)

The equilibrium position (4.430a) = (4.431a) leads to (4.431b) by differentiation with respect to the parameter:

```
$0 = f(\bar{x};q): \quad \frac{\partial f}{\partial q} =-\frac{\partial f}{\partial \bar{x}}\frac{\partial\bar{x}}{\partial q} \quad (4.431a, b)$
```

where the equilibrium position depends on the parameter (Figure 4.22). If the equilibrium is stationary (4.432a), then, the potential has an inflection point (4.432b):

```
$\frac{\partial f}{\partial \bar{x}}=-\frac{\partial^2\Phi}{\partial \bar{x}^2}: \quad \begin{cases} =0 & singular bifurcation, \ \neq 0 & vertical bifurcation, \end{cases} \quad (4.432a-d)$
```

two cases arise: (i) in case (4.432c) $d\bar{x}/dq$ is indeterminate, corresponding to a singular point, where no curve or several integrals may pass, for example at the point $A$; (ii) in the sub-case (4.432d) $d\bar{x}/dq=\infty$ or $dq=0$, implying that there is a double root, as the transition from two distinct real roots to a complex conjugate pair, for example at the point $B$. In both cases there is a change in the number of roots, and a change in the qualitative behavior and both points correspond to a bifurcation, namely