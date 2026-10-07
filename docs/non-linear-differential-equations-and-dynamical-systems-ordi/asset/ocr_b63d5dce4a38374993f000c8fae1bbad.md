# Non-Linear Differential Equations and Dynamical Systems

and the conditions (3.222b--d) mean that it vanishes. The integrability conditions (3.222b--d) are necessary; they are also sufficient as follows from the first-order Stokes theorem (3.150a, b; 3.151a, b). It has been shown that the first-order differential in three variables (3.219) exact (3.220a = 3.224b) and has general integral (3.224e):

```
$$\check{X} \in C^1(\mathbb{R}) : 0 = \dot{\check{X}}=d\Phi \Leftrightarrow \Omega = \nabla \wedge \check{X} = 0 \Leftrightarrow \check{X} = V\Phi \Leftrightarrow \Phi(x)=C,$$
\quad\(3.224a-e)$
```

specifying a family of twice continuously differentiable (3.221e) surfaces orthogonal (3.234b) to the continuously differentiable (3.222a) vector of coefficients if the latter has zero curl (3.222b--d) = 3.223a, b; 3.224c). For example (3.225a) is an exact differential:

```
$0 = \alpha x^{\alpha-1}y^\beta z^\gamma + \beta x^\alpha y^{\beta-1}z^\gamma + \gamma x^\alpha y^\beta z^{\gamma-1}dz = d(x^\alpha y^\beta z^\gamma), \quad x^ay^bz=C,$n\quad\(3.225a, b)$
```

with general integral (3.225b), it can be checked that the vector of coefficients has zero curl (3.222b--d).

# 3.9.2 Integrating Factor and Integrability Condition

If the integrability conditions (3.222b--d) are not met, then the differential in three variables (3.219) is not. A surface orthogonal to the vector of coefficients will still exist (Figure 3.7) if there is an integrating factor multiplied by the inex differential (3.219) renders it exact (3.226a), implying (3.226b):

```
$$\lambda(Xdx + Ydy + Zdz) = d\Phi: \left( \frac{\partial\Phi}{\partial x}, \frac{\partial\Phi}{\partial y}, \frac{\partial\Phi}{\partial z} \right) = \lambda(X,Y,Z). \quad\(3.226a, b)$
```

There are: i conditions to be satisfied, the components $\{X,Y,Z\}$ of the vector of coefficients (3.226b); ii only two free functions, namely the integrating $\Phi$ and the integrating factor $\lambda$. That one constraint or integrability condition must be imposed on the vector of coefficients so that an integrating factor exists. This condition is obtained by substituting (3.226b in (3.222b-d), assuming that the integral has continuous second-order derivatives:

```
$$\frac{\partial}{\partial y}(\lambda X) = \frac{\partial}{\partial x}(\lambda Y), \quad \frac{\partial}{\partial z}(\lambda X) = \frac{\partial}{\partial x}(\lambda Z), \quad \frac{\partial}{\partial z}(\lambda Y) = \frac{\partial}{\partial y}(\lambda Z); \quad\(3.227a-c)$
```