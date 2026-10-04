# Applied Time Series Analysis with R

![](bbox=[0.218, 0.118, 0.781, 0.313])

FIGURE 1.5
Realization from X, in Example 1.2.

length 100 from the model in Equation 1.8. Notice that the realization seems to “wander” back and forth around the mean $\mu = 0$ suggesting the possibility of a stationary process.

# EXAMPLE 1.3: A STATIONARY COSINE PROCESS
Define $X(t)$ for $t \in (-\infty, \infty)$ by

```
$X(t) = C\cos(\lambda t + Y)
```

where
C and $\lambda$ are real-valued constants
Y is a random variable

Then, as we will show in the following, $X(t)$ is stationary if and only if $\varphi(1) = \varphi(2) = 0$, where $\varphi(u)$ is the characteristic function of $Y$, that is,

```
$\varphi(u) = E[e^{iuY}] \quad \text{for } i = \sqrt{-1}$.
```

Before verifying this result we first note that $\varphi(u)$ can be written as

```
$\varphi(u) = E[cos(uY) + iE[sin(uY)]. \quad (1.12)$
```

We also make use of the trigonometric identities

+   1. $\coscosA + B) = \cos A \cos B - \sin A \sin B$
2. $\cos A \cos B = \frac{1}{2}\cos(A + B) + \frac{1}{2}\cos(A - B)$.

Using identity (1), we know that $X(t)$ in Equation 1.11 can be expressed as

```
$X(t) = C[cos\lambda t \cos Y - \sin \lambda t \sin Y], \quad (1.13)$
```