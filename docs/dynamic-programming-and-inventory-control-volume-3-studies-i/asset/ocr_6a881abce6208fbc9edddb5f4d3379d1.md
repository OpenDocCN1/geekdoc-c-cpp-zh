hence also by appropriate conditioning

```
u_\alpha(x) - \frac{\rho}{1-\alpha} = E \left[ \sum_{n=1}^{\tau-1} \alpha^{n-1} (hy_n + p(y_n - D_{n+1})^- - \rho) \right] + E \alpha^{\tau-1} (h - c)(y_\tau - E(S - D)^+)
```

and letting \(\alpha\) tend to 1 we obtain

```
u_\alpha(x) - \frac{\rho}{1-\alpha} \to E \left[ \sum_{n=1}^{\tau-1} (hy_n + p(y_n - D_{n+1})^- - \rho) \right] + E(h-c)(y_\tau - E(S - D)^+).
```

Replacing \(-(h-c)E(S-D)^+\) by \(cS + pE(S-D)^- - \rho\), we obtain the probabilistic interpretation of the function \(u(x)\) as defined by (6.2.8). (6.2.9).

# 6.3. ERGODIC CONTROL OF INVENTORIES WITH BACKLOG

# 6.3.1. CONVERGENCE RESULTS.

We consider the situation of Theorem 5.6.1. The functional equation is given by

```
(6.3.1) \(u_\alpha(x) = -cx + hx^+ + px^- + \inf_{v \ge 0} [c(x+v) + \alpha E u_\alpha(x+v-D)].\)
```

We know that the optimal feedback is defined by a Base stock policy \(S_\alpha\) with

```
(6.3.2) \(F(S_\alpha) = \frac{\alpha(h+c)-c}{\alpha(h+p)},\)
```

which has a unique solution provided \(\alpha > \frac{c}{p+c}\). This will be assumed since we will let \(\alpha\) tend to 1.

Our objective is to prove the

# **Theorem 6.5.** Define \(S\) uniquely by

```
(6.3.3) \(F(S) = \frac{h}{p+h},\)
```

the number \(\rho\) by

```
(6.3.4) \(\rho = c\bar{D} + pE(S - D)^- + hE(S - D)^+,\)
```

and

```
(6.3.5) \(g(x) = (h - (h + p)\bar{F}(x))^+,\)
```

then \(S_\alpha \uparrow S\) and

```
\(u_\alpha(x) - \frac{\rho}{1 - \alpha} \to u(x),\)
```

where \(u\) is defined by

```
(6.3.6) \(\begin{cases} u(S) = (h - c)\bar{D} - (p + h)E(S - D)^- \\ u'(x) = -c + h\bar{I}_{x>0} - p\bar{I}_{x<0} + z(x) \end{cases},\)
```

where

```
(6.3.7) \(z(x) = \sum_{n=1}^{+\infty} g * f^{*(n-1)}(x).\)
```