# Applied Time Series Analysis with R

circle. A zero-mean process, $X_t$, is said to follow a multiplicative seasonal ARUMA$(p,d,q) \times (P_v, D_v, Q_v)$ model if it can be written in the form

```
$\phi(B)\Phi(B')\lambda(B)\lambda(B')X_t = \theta(B)\theta(B')a_t, \quad (1.16)$
```

the roots of $\phi(z)=0, \Phi(z')=0, \theta(z)=0,$ and $\Theta(z')=0$ all lie outside the unit circle, the roots of $\lambda(z)=0$ and $\lambda(z')=0$ on the unit circle are

Using Theorem 5.1, it follows that for the multiplicative seasonal model $\phi(B)\Phi(B)(1-B^s)X_t = \theta(B)\theta(B')a_t$, for which the only roots on the unit circle are the roots of $1-z^s=0$, the limiting autocorrelations are given by

```
$\rho_k'=1, \quad k=0, \pm s, \pm2s,\dots$
$=0, \quad \text{elsewhere.}$
```

In this example $\lambda(B')=1-B'$ and $D_s=1.
A example of a nonstationary multiplicative seasonal model is given by

```
$\phi(B)(1-B^4)(X_t-\mu) = \theta(B)a_t, \quad (1.17)$
```

for which the limiting autocorrelations are given by

```
$\rho_k'=1, \quad k=0, \pm4, \pm8,\dots$
$=0, \quad \text{elsewhere.}$
```

In model in Equation 5.17 $d=0$ and $D_s=1$.

# **5.3.1 Factor Tables for Seasonal Models of the Form**
of Equation 5.17 with $s=4$ and $s=12$

Although the seasonal order, $s$, can take on any integer greater than in its applications, it is the case that $s=4$ (quarterly data) and $s=12$ (monthly data). In the case of $s=4$, we have $(1-B)(1+B)(1+B^2)$ so that the roots of the characteristic equation $1-z^4=0$ are 1 and $\pm i$. Specifically, the factor table associated with the $(1-B^s)X_t=a_t$, is given in Table 5.4. In Table 5.5, we see the more complicated factor table for $(1-B^{12})X_t=a_t$. The roots of $1-z^{12}=0$ are the 12 roots of unity that are shown in Table 5.5 along with the associated factors and system frequencies. When analyzing data for which seasonal model with $s=4$ or $s=12$ is a candidate, it will be useful to refer to Tables 5.4 and 5.5 to see how the factors of the estimated model agree with expected for the seasonal models represented in these two tables. This will be further discussed in Section 8.5.3.