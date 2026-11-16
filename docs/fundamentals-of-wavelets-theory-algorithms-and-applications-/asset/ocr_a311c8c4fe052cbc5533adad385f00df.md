![](bbox=[0.14, 0.08, 0.82, 0.28])

The parameter \(\alpha\) can be used to control the width of the Gaussian pulse. It is evident from (3.51) and (3.52) that a large value of \(\alpha\) produces a narrow pulse, but its spectrum spreads wider on the \(\omega\)-axis.

# 3.6 POISSON'S SUM AND PARTITION OF UNITY

We now return to the Fourier series and discuss the Poisson's sum whose derivation is made much simpler by using some properties of the Fourier transform. In many applications, it is necessary to form a periodic function from a nonperiodic function with finite energy for the purpose of analysis.

Poisson's sum formula is useful in relating the time-domain information of such a function with its spectrum. Let \(f(t) \in L^2(\mathbb{R})\). The periodic version of \(f(t)\), to be called \(f_p(t)\), is obtained by

```
\(f_p(t) := \sum_{n=-\infty}^{\infty} f(t + 2\pi n),\)
(3.53)
```