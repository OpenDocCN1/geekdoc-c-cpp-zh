# G-Stationary Processes

Definition 13.7 says that if $\lambda\neq0$ and $g(t)=(t^{\lambda}-1)/\lambda$, or $\lambda=0$ and $u=\ln t, h>1$, then the $G(\lambda)$-process in Equation 13.14 has stationary continuous $AR(p)$ dual $Y(u)$ given by

```
$$\prod_{j=1}^{p}(D-\alpha_{j})Y(u)=a(u).$\quad (13.15)
```

As a simple example, take the case $p=1$ in Equation 13.14, which is

```
$$(t^{\lambda}-1)D-\alpha_{1})X(t)=e(t).$\quad (13.16)
```

If $u=(t^{\lambda}-1)/\lambda$, then $t=<u\lambda$, and proceeding formally, we obtain

```
$$\frac{dX(t)}{dt}=\frac{dX}{du}\frac{du}{dt}=t^{\lambda-1}dX(t).$
```

So, from Equation 13.16, we have $t^{\lambda-1}(dX(t)/dt)-\alpha_{1}X(t)=(dX(t)/du)-\alpha_{1}X(t)=e(t)$. Since $X(t)=Y(u)$, it follows that $dY/du-\alpha_{1}Y(u)=a(u)$, where $a(u)$ is white noise. Therefore, $Y(u)$ is a continuous AR(1) process as noted in Equation 13.15.

The $G(p,\lambda)$ in Equation 13.14 has been extended to the $G(p,q;\lambda)$ process

```
$$\prod_{j=1}^{p}(d^{\lambda-1}-\alpha_{j})X(t)=\prod_{j=1}^{q}(d^{\lambda-1}-\delta_{j})\epsilon(t).$\quad (13.17)
```

We will not pursue this here except to note that for a further discussion of the Euler$(p,q)$ and $G(p,q;\lambda)$ process, as Choi et al. (2006) and Jiang et al. (2006).

# 13.3.2 Sampling the Continuous $G(\lambda)$-Stationary Processes

Suppose $X(t)$ is a continuous $G(\lambda)$-stationary process, and suppose

```
$t_{k}=(k+\xi)\Delta\lambda+1)^{1\lambda},\quad (13.18)
```

where $k=1, 2, ... , \Delta>0$, and $(k+\xi)\Delta\lambda+1\ge0$, in this case $\xi$ determines the offset and $\Delta$ is the sampling interval. Then, the dual, $Y_{k}=X(t_{k})$, is a stationary process. Further, if exists, the dual process is a discrete $ARMA(p,r)$ with $r\le p-1$. The Nyquist frequency of the discrete dual, $Y_{k}$ is given by $1/(2\Delta)$. Note that $\lim_{\lambda\to\infty}h^{k}=h^{\xi}$. For discussion and proof of these remarks, see Jiang et al. (2006).