from which we can obtain

```
w_\alpha(x) \le h + w_\alpha(x) - \varpi_0(w_\alpha(x) - Ew_\alpha(x - D)).
```

We have then proved

```
w_\alpha(x) \le Ew_\alpha(x - D) + \frac{h}{\varpi_0}.
```

Now

```
Ew_\alpha(x - D) = E[w_\alpha(x - D) \mathbb{I}_{D \le x}] + E[w_\alpha(x - D) \mathbb{I}_{D > x}] \le w_\alpha(x) F(x) \mathbb{I}_{x > 0} + E[w_\alpha(x - D) \mathbb{I}_{D > x}].
```

However

```
u'_\alpha(x;\sigma,\eta) \le h, \forall x \le 0 \Rightarrow w_\alpha(x) \le h, \forall x \le 0
```

from which it follows that

```
Ew_\alpha(x - D) \le w_\alpha(x^+)F(x^+) + h,
```

which implies

```
w_\alpha(x)\bar{F}(x) \le h \left(1 + \frac{1}{\varpi_0}\right),
```

and the proof has been completed.

# 13.5.3. LIMIT BEHAVIOR FOR THE CASE $K=0$.

We can now state the limit of (13.5.39).

# Theorem 13.3. Assume (13.5.1) and

```
(13.5.17) \quad \bar{F}(x) > 0, \forall x < \infty, \quad p > c.
```

There exists a sequence \(\rho_\alpha\) such that if \(\alpha \to 1\), for a subsequence

```
(13.5.18) \quad u_\alpha(x;\sigma,\eta) - \frac{\rho_\alpha}{1-\alpha} \to u(x;\sigma,\eta),
```

uniformly on any compact of \(R\). We have also \(\rho_\alpha \to \rho\). The function \(u(x;\sigma,\eta)\) is locally Lipschitz continuous and satisfies

```
|u'(x;\sigma,\eta)| \le \frac{C}{F(x)}.
```

The pair \(u(x;\sigma,\eta), \rho\) satisfies

```
(13.5.19) \quad u(x;\sigma,\eta) + \rho = -cx + \ell^{(+,\eta)}(x) + \inf_{y \ge x} \left\{ cy + \sum_{k=0}^{\sigma+\eta} \gamma(k;\sigma,\eta) u^{(\sigma+\eta+1-k)}(y,0,k) + \sum_{k=\sigma+\eta+1}^M \gamma(k;\sigma,\eta) u(y;\sigma+1,\eta) \right\}.
```