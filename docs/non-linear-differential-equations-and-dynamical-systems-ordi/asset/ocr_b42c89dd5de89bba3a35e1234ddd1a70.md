# Non-Linear Differential Equations and Dynamical Systems

NOTE 3.16: Homogeneous Functions and Differential

A function $P(x,y)$ is said to be homogeneous of degree $q$ if it satisfies (3.334a):

```
$P(x,y) = x^q P\left(1, \frac{x}{y}\right); \quad P \in D(\mathbb{R}^2); \quad x\frac{\partial P}{\partial x} + y\frac{\partial P}{\partial y} = qP, \quad (3.334a-c)$
```

and if it is differentiable (3.334b) Euler's theorem (3.33c) applies; the latter can be proved from:

```
$x\frac{\partial P}{\partial x} + y\frac{\partial P}{\partial y} = qx^q P\left(1, \frac{x}{y}\right) - \frac{y}{x}x^{q+1} = x\frac{\partial P}{\partial x} + y\frac{\partial P}{\partial y} = qP. \quad (3.335)$
```

If the functions $X, Y$ are homogeneous of the same degree $q$, they satisfy the identity:

```
$Y\left(x\frac{\partial X}{\partial x} + y\frac{\partial X}{\partial y}\right) = YX = X\left(x\frac{\partial Y}{\partial x} + y\frac{\partial Y}{\partial y}\right), \quad (3.336a, b)$
```

that is equivalent to:

```
$\frac{\partial}{\partial y}\left(\frac{X}{XX+YY}\right) - \frac{\partial}{\partial x}\left(\frac{Y}{XX+YY}\right) = \quad (3.336c)$
```

The proof of (3.336c) follows from:

```
$(XX+YY)\left[\frac{\partial}{\partial y}\left(\frac{X}{XX+YY}\right) - \frac{\partial}{\partial x}\left(\frac{Y}{XX+YY}\right)\right]\n=(XX+YY)\left(x\frac{\partial X}{\partial y} + y\frac{\partial X}{\partial y} - X\left(x\frac{\partial (XX+YY)}{\partial x} + y\frac{\partial (XX+YY)}{\partial y}\rightright) + Y\left(x\frac{\partial Y}{\partial x} + y\frac{\partial Y}{\partial y}\right) + X\right) \quad (3.337)\n=Y\left(x\frac{\partial Y}{\partial x} + y\frac{\partial Y}{\partial y}\right) - X\left(x\frac{\partial X}{\partial x} + y\frac{\partial X}{\partial y}\right) = 0.$
```

The identities (3.336a, b) = (3.33c) for homogeneous functions (x, y) of the same degree (3.335), are used next (note 3.17) to integrate homogeneous first-order differentials.

NOTE 3.17: Integration of Homogeneous Differentials

The identity (3.336c) = (3.153c) implies that if the functions (3.338a, b) are homogeneous (3.334a) with the same degree $q$:

```
$X(x,y)=x^q X\left(1, \frac{x}{y}\right), \quad Y(x,y)=x^q Y\left(1, \frac{x}{y}\right), \quad (3.338a, b)$
```