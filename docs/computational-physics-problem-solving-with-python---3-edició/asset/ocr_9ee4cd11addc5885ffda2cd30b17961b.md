# 26.4.1

# Singular Integrals (Math)

A singular integral

```
$$\mathcal{G}=\int_{a}^{b} g(k)\,\mathrm{d}k\ ,$$
```

(26.23)

is one in which the integrand $g(k)$ is singular at a point $k_0$ within the integration interval $[a,b]$, yet with the integral $\mathcal{G}$ remaining finite. (If the integral itself were infinite, we could not compute it.) Unfortunately, computers are notoriously bad at dealing with infinite numbers, and if an integration point gets too near the singularity, overwhelming subtractive cancellation or overflow may occur. Consequently, we apply some results from complex analysis before evaluating singular integrals numerically.$^{4)}$

In Figure 26.4, we show three ways to avoid the singularity of an integrand. The paths in Figure 26.4a and b move the singularity slightly off the real $k$-axis by giving the singularity a small imaginary part $\pm i\epsilon$. The Cauchy principal-value prescription $\mathcal{P}$ in Figure 26.4c is seen to follow a path that “pinches” both sides of the singularity at $k_0$, but does not to pass through it:

```
$$\mathcal{P}\int_{-\infty}^{+\infty} f(k)\,\mathrm{d}k = \lim_{\epsilon\to 0}\left[\int_{-\infty}^{k_0-\epsilon} f(k)\,\mathrm{d}k + \int_{k_0+\epsilon}^{+\infty} f(k)\,\mathrm{d}k\right]\ .$$
```

(26.24)

The preceding three prescriptions are related by the identity

```
$$\int_{-\infty}^{+\infty} \frac{f(k)\,\mathrm{d}k}{k - k_0 \pm i\epsilon} = \mathcal{P}\int_{-\infty}^{+\infty} \frac{f(k)\,\mathrm{d}k'}{k - k_0} \mp i\pi f(k_0)\ ,$$
```

(26.25)

which follows from Cauchy's residue theorem.

![](bbox=[0.12, 0.64, 0.92, 0.78])

(a)

(b)

(c)

Figure 26.4 Three different paths in the complex $k'$ plane used to evaluate line integrals when there are singularities. Here the singularities are at $k$ and $-k$, and the integration variable is $k'$.

4) Singh and Thompson (1993) describe a different approach using Maple and Mathematica.