# Chapter 4 Likelihood Models for Overdispersed Binomial Responses 85

When $\alpha = 0$, distribution (4.17) corresponds to independence among the Bernoulli outcomes, that is, to a Binomial($\pi, m$). When $\alpha > 0$ ($\alpha < 0$), it corresponds to the case of over (or under) dispersion. Altham showed that for certain values of $\alpha$, distribution (4.17) is a mixture of three binomials, namely,

```
$$T = \begin{cases} A+2 & \text{with probability } \frac{1}{2}m(m-1)\alpha\pi \ B & \text{with probability } \frac{1}{2}m(m-1)\alpha \ C & \text{with probability } \frac{1}{2}m(m-1)\alpha(1-\pi) \end{cases} \quad (4.19)$
```

where $A \sim \text{Binomial}(\pi, m-2)$, $B \sim \text{Binomial}(\pi, m)$ and $C \sim \text{Binomial}(\pi, m-2)$.

It can be shown that

```
$E(T) = m\pi \quad (4.20)$
```

and

```
$Var(T) = m\pi(1-\pi)\{1+(m-1)\alpha^2\}\quad (4.21)$
```

Under the assumption of overdispersion, the parameter $\alpha$ might play the role of $\rho^2$, and therefore (4.17) can be parameterized as

```
$Pr(T=t) = Pr(X=t) = \frac{1}{2}\left(\rho^2\frac{t(t-1)}{\pi} + \frac{(m-t)(m-t-1)}{1-\pi}\frac{1}{2}\right),\quad t=0,1,...,m \quad (4.22)$
```

Note that this distribution of Binomial to incorporate correlation among the Bernoulli outcomes comes at a price. The restrictions on the parameter space may present problems in applying this distribution to real life data. However, we have included this distribution in our discussion to review Altham's assumption to the attention of the reader. In the subsequent analyses, we are including it for completeness.

From Section 4.2 through the current section, we have introduced four different distributions for modeling overdispersion. The first two moments of these characterize overdispersion relative to the Binomial, as seen in equations (4.4) and (4.5). Here, we have shown that all four of the distributions can be viewed as mixtures of Binomials. This provides a useful link to compare their properties, and facilitates the computation of MLEs. In the next section we provide a comprehensive example of how these distributions can be used in practice, and we demonstrate how to obtain MLEs using the NLMIXED procedure.