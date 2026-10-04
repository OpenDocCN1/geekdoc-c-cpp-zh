
# 582 Applied Time Series Analysis with R

![](img/41dcbfb9af56fa48895afde322197b0b_598_0.png)

**13.19**
(a) Realization from model in Equation 13.27, (b) dual data, (c) periodogram for data in (a), (d) periodogram for data in (b), (e) low-pass filtered dual data using cutoff $f=0.075$, and (f) low-pass filtered data after transforming back to original time.

## 13.6 Concluding Remarks

TVF analysis as that described above has also been applied to TVF data with long-memory dual models. See Bao (2014). Additionally, Chen (2014) has developed techniques for obtaining the time-transformation function using nonparametric methods as an alternative to the $G(\lambda)$ and linear chirp models which use specific functional forms for the time-transformation function. See Chen (2014).

In this chapter, we have introduced important and relatively new methods for analyzing nonstationary time series with TVF behavior. The general

## G-Stationary Processes

approach is to transform the time axis to a dual space in order to obtain a stationary realization that can then be analyzed using standard techniques based on stationarity. A surprisingly large number of applications (chirp signals, Doppler signals, echolocation signals, seismic data, etc.) can be advantageously analyzed using these techniques. For more details concerning analysis and theoretical details, see the references listed throughout this chapter.

## Appendix 13A: G-Stationary Basics

### 13A.1 Generalized Instantaneous Period and IF of a G-Stationary Process

For nonstationary signals, whose spectral content varies with time, the frequency at a particular time is described by the concept of IF. We consider first a simple sinusoidal signal of the form

```
X(t) = A \cos(\phi(t)), (13A.1)
```

With $A$ is constant and $\phi$ is called the cumulative phase of the signal. A common definition (Boashash, 1992a,b) the IF of $X(t)$ in Equation 13A.1 is

```
IF = \phi'(t)/2\pi.
```

Note that this definition shows the rate of change of $\phi(t)$ per $2\pi$ units. However

# Definition 13A.1

Let $H$ be a function such that $H(t)=H(g^{-1}(g(t)+\delta_m))$, $m=1, 2, ...$ where $g$ is any monotonic function and $-\infty < \delta_m < \infty$. Then $H$ is said to be a G-periodic function

with the $G$-period $\delta$ which is equal to the $\delta_m$ for which $|\delta_m|$ is a minimum over $m$. The GIP of the function $H$ at time $t$, denoted $\mathcal{P}(t; \delta)$, is defined by

$$\mathcal{P}(t; \delta) = g^{-1}(g(t) + \delta)-t.$$

Remark: If $GIP=0$, then $H$ is a “aG-periodic,” that is, not G-periodic. Note that $\delta=\mathcal{P}(t)-g(t)$.

# Definition 13A.2

The generalized instantaneous frequency (GIF), $f$, of a function $g(t)$ is a function of time defined as

$$\mathcal{P}(t; \delta) = \frac{1}{\mathcal{P}(t; \delta)}.$$

If $\mathcal{P}(t; \delta) > 0$, then $\mathcal{P}$ is the period starting at $t$ and measured in the positive direction. If $\mathcal{P}(t; \delta) < 0$, then $\mathcal{P}$ is the period starting at $t$ but in the negative direction.

For a $G(\lambda)$-stationary process, such as the one in Example 13A.1 that follows with a single “periodic component,” it is easy to show that the GIP of the $G(\lambda)$-autocovariance is

$$\mathcal{P}(t; \delta) = \begin{cases} {t^\lambda + \lambda\delta}^{1/\lambda}-t, & \lambda \neq 0, \ t(e^{\delta}-1), & \lambda=0,\end{cases} \quad (13A.2)$$

where $\delta > 0$.

The quantity $\delta$ can be interpreted as the period of the autocovariance of the dual process. In the GIP and GIF of the $G(\lambda)$-stationary processes are denoted by $\mathcal{P}(t; \lambda)$ and $f(t; \lambda)$ since $\lambda$ is the only parameter of the function $g$. If $\lambda=1$ (i.e., the stationary case), then $\mathcal{P}(t; 1)=\delta$ and $f(t; 1)=1/\delta$. Consequently, as was expected, in this case the GIP is the standard period, $\delta$, for any $t>0$, $1/\delta$ is the usual frequency.

As already described in Section 13.3, differing values of $\lambda$ produce a large variety of periodic behaviors of the process, or more specifically, of the $G(\lambda)$-autocovariance. Jiang et al. (2006) show that for $0<\lambda<1$, the GIP is a monotonically increasing concave function, while for $\lambda<0$, it is monotonically decreasing and convex. If $\lambda>1$, the GIP is monotonically decreasing concave and convex.

From Example 13A.1 which follows, it is clear that the GIF and IF are not the same. However, for G-stationary processes, the IF is a first-order approximation of the GIF.

## G-Stationary Processes

### EXAMPLE 13A.1: ILLUSTRATION OF THE DIFFERENCE BETWEEN GIF AND IF

Let $H(t) = \cos g(t)$, where $u = g(t) = (t^\lambda-1)/\lambda$. Therefore, $t = g^{-1}(u) = (u\lambda+1)^{1/\lambda}$ and $g^{-1}(g(t)+\delta) = [(g(t)+\delta)\lambda]^{1/\lambda} = [t^\lambda+\delta]^{1/\lambda}$, for $\lambda > 0$. Difference, if $\delta$ is the $G$-process, then from Definition 13A.1, it follows that $H(t) = H^{-1}(g(t)+\delta)$. So, if $\lambda > 0$, then $\delta > 0$ and it follows that

```
$$\cos\left(\frac{t^\lambda-1}{\lambda}\right) = \cos\left(\frac{(t^\lambda+\delta)^{1/\lambda}-1}{\lambda}\right)$$
= \cos\left(\frac{t^\lambda-1}{\lambda}+\delta\right)
```

Consequently, $\delta=2\pi$. Note that if $\lambda<0$, then $t^2+\delta>0$ for $t>0$, which implies $\delta<0$. In this case, $\delta=-2\pi$. Now, returning to the case $\lambda>0$, we have

```
$$\mathcal{P}(t;lambda,2\pi)=(t^\lambda+2\pi t^\lambda)^{1/\lambda}-t=t[1+2\pi t^\lambda]^{1/\lambda}-t.$$
```

Then, for $t^\lambda>2\pi$, it follows that the GIF is given by

```
$$\mathcal{P}(t;lambda,2\pi)=\left\{t\left[1+\frac{1}{2}(2\pi t^\lambda)+\frac{1}{2\lambda}\left(1-\frac{1}{\lambda}\right)(2\pi t^\lambda)^2+...\right]\right\}.$$
```

So, the GIF is the reciprocal, which is

```
$GIF=\frac{1}{2t^{\lambda+1}(1-\lambda)(2\pi)^2t^{-2\lambda+1}}$
= \frac{t^{\lambda-1}}{2\pi}[1+(pi-\lambda)t^{\lambda-1}+...]
```

Thus, for large $t$,

```
$GIF=\frac{t^{\lambda-1}}{2\pi}=\frac{g'(t)}{2\pi}=IF.$
```

Jiang et al. (2006) shows that the result of Example 13A.1 can be generalized to any monotonically increasing function $g(t)$. That is, if $H(t)=A\cos[g(t)]$, and $g(t)$ is monotonically increasing, then $\delta=2\pi$ and $\mathcal{P}(t;2\pi)=g^{-1}(g(t)+2\pi)-t$. They also show that the IF is a first-term Taylor series approximation to the GIF.

### 13A.2 Instantaneous Spectrum of a G(\lambda$) Process

Since in signals the entire frequency structure is evolving with time, the concept of an instantaneous spectrum of a G(\lambda$) process is needed. In this regard, let $f'=1/delta$, and let $G_X(f^*; \lambda)$ denote the G(\lambda$) spectral density. For example, in the case of a G($p; \lambda$) model, the G(\lambda$) spectral density is the AR($p$) spectral density associated with the AR($p$) model fit to the dual. Definition 13A.2 and Equation 13A.2, it is clear that $f^*$ is a function of $f$ (= GIF) and $t$. That is, from Equation 13A.2

```
$f^*=0, \text{if } f=0$,
$\left[\ln\left(1+\frac{1}{f}\right)\right]^{-\gamma}, \text{if } f \neq 0, \lambda=0$,
=\left(t+\frac{1}{f}\right)^{-t^{\lambda}} \quad (13A.3)
```

We can, therefore, capture the instantaneous frequencies through $f^*$ defined in Equation 13A.3. Note that since $G_X(f^*; \lambda) = G_X(-f^*; \lambda)$, we will always keep $f^* \geq 0$ and $f \geq 0$.

# Definition 13A.3

If $X(t)$ is a G(\lambda$) process and $G_X(f^*; \lambda)$ is its G($\lambda$)-spectrum, then the instantaneous spectrum of $X(t)$ at time $t$, denoted $S(f, t; \lambda)$, is defined as

```
$S(f, t; \lambda) = G_X(f^*; \lambda). \quad (13A.4)
```

# Theorem 13A.1

If $X(t)$ is a G($p; \lambda$) process, then the instantaneous spectrum of $X(t)$ at time $t$ is given by

```
$S(f, t; \lambda) = \sigma_{\lambda}^2 \prod_{j=1}^{q} \frac{|\beta_j - i2\pi f^*|^2}{\prod_{k=1}^{q} |\alpha_k - i2\pi f^*|^2} \quad (13A.5)
```

where $f^*$ is given by Equation 13A.3.

Proof: Follows from Equation 13A.4.
