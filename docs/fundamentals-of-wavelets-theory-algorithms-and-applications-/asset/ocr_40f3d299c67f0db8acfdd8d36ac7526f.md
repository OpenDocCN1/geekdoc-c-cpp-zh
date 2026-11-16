$a_{k,2}^n$ will coincide with $c_{-2}$. The next index, $c_{k+1,2}^n$, will then lie between $c+1,2$ and $c+2,2$.

# FIGURE 8.6: The first term of $\{a_{k,M}^n\}$ when $\{a_{k,M}\}$ starts with $k \neq 0$.

![](bbox=[0.15, 0.26, 0.85, 0.45])

Taking all of these points into account, we can obtain $a_M^n$ from $a_M$ by following these steps:

+   1. Based on the given discretized function data, determine the starting index of $a_M^n$. Let it be $a_{l,M}^n$.

+   2. Let $a_{l,M}^n$ lie between $a_{s,M}$ and $a_{s+1,M}$.

+   3. Let $a_{l,M}^n$ be shifted from $a_{s,M}$ toward the right by $\zeta$ in time. Then starting with $r=0$, compute

```
(8.30) $a_{l,M}^n = (1 - 2^M \xi) \tilde{a}_{s+r,M} + 2^M \xi \tilde{a}_{s+1+r,M}$.
```