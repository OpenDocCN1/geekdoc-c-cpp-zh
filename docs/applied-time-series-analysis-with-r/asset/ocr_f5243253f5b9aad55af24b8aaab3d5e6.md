# G-Stationary Processes

# EXAMPLE 13A.1: ILLUSTRATION OF THE DIFFERENCE BETWEEN GIF AND IF

Let $H(t) = \cos g(t)$, where $u = g(t) = (t^\lambda-1)/\lambda$. Therefore, $t = g^{-1}(u) = (u\lambda+1)^{1/\lambda}$ and $g^{-1}(g(t)+\delta) = [(g(t)+\delta)\lambda]^{1/\lambda} = [t^\lambda+\delta]^{1/\lambda}$, for $\lambda > 0$. Difference, if $\delta$ is the $G$-process, then from Definition 13A.1, it follows that $H(t) = H^{-1}(g(t)+\delta)$. So, if $\lambda > 0$, then $\delta > 0$ and it follows that

```
$$\cos\left(\frac{t^\lambda-1}{\lambda}\right) = \cos\left(\frac{(t^\lambda+\delta)^{1/\lambda}-1}{\lambda}\right)$$\n= \cos\left(\frac{t^\lambda-1}{\lambda\|+\delta\right)$
```

Consequently, $\delta=2\pi$. Note that if $\lambda<0$, then $t^2+\delta>0$ for $t>0$, which implies $\delta<0$. In this case, $\delta=-2\pi$. Now, returning to the case $\lambda>0$, we have

```
$$\mathcal{P}(t;lambda,2\pi)=(t^\lambda+2\pi t^\lambda)^{1/\lambda}-t=t[1+2\pi t^\lambda]^{1/\lambda}-t.$
```

Then, for $t^\lambda>2\pi$, it follows that the GIF is given by

```
$$\mathcal{P}(t;lambda,2\pi)=\left\{t\left[1+\frac{1}{2}(2\pi t^\lambda)+\frac{1}{2\lambda}\left(1-\frac{1}{\lambda}\right)(2\pi t^\lambda)^2+...ight]\right\.$
```

So, the GIF is the reciprocal, which is

```
$GIF=\frac{1}{2t^{\lambda+1}(1-\lambda)(2\pi)^2t^{-2\lambda+1}}$$\n=\frac{t^{\lambda-1}}{2\pi}[1+(pi-\lambda)t^{\lambda-1}+...]$
```

Thus, for large $t$,

```
$GIF=\frac{t^{\lambda-1}}{2\pi}=\frac{g'(t)}{2\pi}=IF.$
```

Jiang et al. (2006) shows that the result of Example 13A.1 can be generalized to any monotonically increasing function $g(t)$. That is, if $H(t)=A\cos[g(t)]$, and $g(t)$ is monotonically increasing, then $\delta=2\pi$ and $\mathcal{P}(t;2\pi)=g^{-1}(g(t)+2\pi)-t$. They also show that the IF is a first-term Taylor series approximation to the GIF.