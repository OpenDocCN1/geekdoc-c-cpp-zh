# Differentials and First-Order Equations

# 3.8.6 Infinitely Many Integrating Factors

The integrating factor $\lambda$ for a general inexact differential (3.145b) is a function $\lambda(x,y)$ that is not unique. For example, substituting (3.178a) in (3.176b) leads to (3.178b):

```
$$\lambda = \mu\Phi; \quad \frac{\partial Y}{\partial x}-\frac{\partial X}{\partial y\|+\left(Y\frac{\partial}{\partial x}-X\frac{\partial}{\partial y}\right)\log\mu = \left(X\frac{\partial}{\partial x}-Y\frac{\partial}{\partial x}\right)\log\Phi; \quad (3.178a, b)$
```

from (3.173a) $\mu$ is (3.179a) if the r.h.s. of (3.17b) vanishes, leading to

```
$$\frac{\partial \Phi}{\partial x}=X\frac{\partial \Phi}{\partial y}; \quad \left(Y\frac{\partial}{\partial x}-X\frac{\partial}{\partial y}\right)\log\mu = 0, \quad \;\quad;\quad (3.179a, b)$
```

that proves that $\mu$ is also an integrating factor that satisfies (3.176b). This result can be stated in two equivalent ways: (a) if $\lambda,\mu$ are integrating factors (3.176b; 3.179b) of the (standard LXVII) inexact differential (3.145b), their ratio $\Phi=\lambda\mu$ in (3.148a) is a solution (3.146c); or if $\Phi$ is a solution (3.146c) of the inexact differential (3.145b) and $\mu$ an integrating factor (3.179b), then (3.178a) and also (3.180b) are also integrating factors (3.176b), where (3.180a) is a differentiable function of the solution:

```
$G \in D(R); \quad\quad\quad\quad\quad\lambda = \muG(\Phi). \quad\quad (3.180a, b)$
```

The latter result follows from one of the statements: (i) if (3.148c) is a solution of the inexact differential (3.145b), then (3.181a) is also a solution:

```
$G(\Phi(x,y))=G(C_1); \quad\lambdaG(dX+dY)=G(\Phi)d\Phi; \quad\quad (3.181a, b)$
```

+   ii if the inexact differential (3.145b; 3.174a) is transformed into an exact differential (3.174b) by multiplying the integrating factor $\lambda$, then (3.181b) is also an exact differential proving that $\lambdaG$ is an integrating factor.

# 3.8.7 Integrating Factor Depending Only on One Variable

Since the integrating factor is not unique it may be sought in several forms that exist only if they satisfy (3.176a, b). The simplest integrating factor that is a function of only the variable x is given by (3.176b) by (3.182a) [[3.182b]:

```
$$\Omega = \frac{\partial Y}{\partial x}-\frac{\partial X}{\partial y}=-Y\frac{\d}{\dx}{\log[\lambda(x)]\}; \quad\quad X\frac{\d}{\dy}{\log[\lambda(y)]\}; \quad\quad (3.182a, b)$
```