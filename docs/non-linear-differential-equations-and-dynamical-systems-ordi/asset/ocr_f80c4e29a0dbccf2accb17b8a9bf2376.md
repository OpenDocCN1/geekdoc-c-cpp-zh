# Non-Linear Differential Equations and Dynamical Systems

# NOTE 3.13: Exact Differentials and Integrating Factor

A first-order differential in one variable (3.327a) is always exact for an integrable coefficient (3.327a), and its solution reduces to an integration (3.227c);

```
$X \in E(\mathbb{R}); \quad X(x)dx = d\Phi \quad \Leftrightarrow \quad \Phi(x) = \int^x \Phi(\xi)d\xi; \quad (3.327a–c)
```

in this there is no curl or helicity. A first-order differential in two variables (3.145b) \equiv (3.328a) may have a vector of coefficients with non-zero curl (3.243b) \equiv (3.328b) and has zero helicity (3.243c) \equiv (3.328c):

```
$X_1 dx_1 + X_2 dx_2 = 0; \quad \Omega = \frac{\partial X_2}{\partial x_1}\frac{\partial X_1}{\partial x_2} \neq 0, \quad H = 0; \quad (3.328a–c)
```

Thus there are two cases: (i) an exact differential (3.329a) if the curl is zero; and (ii) an integrating factor for an inexact differential (3.329b) if the curl is not zero:

```
$X_1dx_1 + X_2dx_2 = \begin{cases} d\Phi & \text{if} \\Omega = 0, \ \lambda^{-1}d\Phi & \text{if} \\Omega \neq 0. \end{cases} \quad (3.329a) \quad (3.329b)
```

In both cases (Figure 3.6) the plane vector field has a family of orthogonal curves.

# NOTE 3.14: Inexact Differentials without an Integrating Factor

A differential in three variables (3.330a) can have a vector of coefficients with non-zero curl (3.330b) and non-zero helicity (3.330c):

```
$0 = X_1dx_1 + X_2dx_2 + X_3dx_3; \quad \Omega = \nabla \cdot \tilde{X} \neq 0, \quad H = \tilde{X}(\nabla \times \tilde{X}) \neq 0. \quad (3.330a–c)
```

Thus there are three cases:: (i) an exact differential (3.331a) for zero curl; (ii) an inexact differential with an integrating factor (3.331b) for non-zero curl and zero helicity; and (iii) an inexact differential without an integrating factor (3.331c) for non-zero helicity:

```
$X_1dx_1 + X_2dx_2 + X_3dx_3 = \begin{cases} d\Phi & \text{if} \\tilde{\Omega} = 0, \ \lambda^{-1}d\Phi & \text{if} \\tilde{\Omega} \neq 0, H, \ \lambda^{-1}d\Phi + d\Psi & \text{if} \\H \neq 0. \end{cases} \quad (3.331a) \quad (3.331b) \quad (3.331c)
```