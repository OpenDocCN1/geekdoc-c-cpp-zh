In general, the PDEs of relevance are of the *convection–diffusion–reaction* type in $n$ space variables and one time variable. The space variables correspond to underlying financial quantities such as an asset, volatility or interest rate while the non-negative time variable $t$ is bounded above by the *expiration* $T$. The space variables are usually defined in their respective positive half-planes.

We model derivatives by *initial boundary value problems* of parabolic type. To this end, consider the general parabolic equation:

```
$$L u \equiv \sum_{i,j=1}^{n} a_{ij}(x,t)\frac{\partial^{2}u}{\partial x_{i}\partial x_{j}} + \sum_{j=1}^{n} b_{j}(x,t)\frac{\partial u}{\partial x_{j}} + c(x,t)u - \frac{\partial u}{\partial t} = f(x,t)\tag{20.1}$$
```

where the functions $a_{ij}, b_{j}, c$ and $f$ are real valued, $a_{ij}=a_{ji}$ and:

```
$$\sum_{i,j=1}^{n} a_{ij}(x,t)a_{i}a_{j} > 0 \quad \text{if}\quad \sum_{j=1}^{n} a_{j}^{2} > 0.\tag{20.2}$$
```

In equation (20.1) the variable $x$ is a point in $n$-dimensional space and $t$ is considered to be a positive time variable. Equation (20.1) is the general equation that describes the behaviour of many derivative types. For example, in the one-dimensional case ($n=1$) it reduces to the Black–Scholes equation (here $t^{*}=T-t$):

```
$$\frac{\partial V}{\partial t^{*}} + \frac{1}{2}\sigma^{2}S^{2}\frac{\partial^{2}V}{\partial S^{2}} + (r-D)S\frac{\partial V}{\partial S} - rV = 0\tag{20.3}$$
```

where $V$ is the derivative type (for example, a call or put option), $S$ is the underlying asset (or stock), $\sigma$ is the constant volatility, $r$ is the constant interest rate and $D$ is a constant dividend. Equation (20.3) is a one-factor case and it can be generalised, for example to the multivariate case:

```
$$\frac{\partial V}{\partial t^{*}} + \sum_{j=1}^{n}(r-D_{j})S_{j}\frac{\partial V}{\partial S_{j}} + \frac{1}{2}\sum_{i,j=1}^{n}\rho_{ij}\sigma_{i}\sigma_{j}S_{i}S_{j}\frac{\partial^{2}V}{\partial S_{i}\partial S_{j}} - rV = 0.\tag{20.4}$$
```

This equation models a multi-asset environment. In this case $\sigma_{i}$ is the volatility of the $i$th asset and $\rho_{ij}$ is the correlation ($-1 \le \rho_{ij} \le 1$) between assets $i$ and $j$. The term $D_{j}$ is the constant dividend for asset $j$. In this case we see that the elliptic part of equation (20.4) ($t^{*}=T-t$, where $T$ is the expiration) is written as the sum of three terms:

+   - Interest earned on cash position:

```
$$r\left(V - \sum_{j=1}^{n} S_{j}\frac{\partial V}{\partial S_{j}}\right).\tag{20.5}$$
```