PROOF. In equation (4.5.2) we have denoted by $|x|$ the function $x \to |x|$. We provide $B_1$ with an equivalent norm

```
||u||_1 = \sup_x \frac{|u(x)|}{1 + \sigma|x|},
```

where $\sigma$ can be chosen arbitrarily and will be chosen small. For $v \in U$ we have

```
l(v, x) \le h|x| + l_1
```

```
\Phi'(|x|)x \le \theta|x| + m
```

Consider again the map $T$ defined in the proof of Theorem, this time from $B_1$ into $B_1$. Note that for $w \in B_1$ and $v \in U$ we have

```
\alpha[\Phi^w(x)] \le \alpha[|w|](1 + \sigma\Phi''(|x|)(x))
\le \alpha[|w|](1 + \sigma\theta|x| + \sigma m).
```

Then

```
||Tw_1 - Tw_2|| \le \alpha|w||| \sup_x \frac{1 + \sigma\theta|x| + \sigma m}{1 + \sigma|x|}.
```

Thanks to the assumptions we have

```
\alpha \sup_x \frac{1 + \sigma\theta|x| + \sigma m}{1 + \sigma|x|} \le \alpha(1 + \sigma m),
```

and by choosing $\sigma$ sufficiently small the number on the right hand side is strictly smaller than 1. Hence $T$ is a contraction in $B_1$. The existence and uniqueness follows.

**Remark.** Again it is possible to see the preceding result as a consequence of the fact that the maximum and the minimum solutions coincide. Indeed, take to fix the ideas $v_0 = 0$. We note first that from the growth assumptions we have

```
(4.5.3) \quad w_0(x) \le \frac{h|x|}{1 - \alpha\theta} + \frac{l_0}{1 - \alpha} + \frac{\alpha m}{1 - \alpha\theta}.
```

Take any control policy $V$. From the definition of $V$, see (4.4.6), using the fact that $\bar{u} \le w_0$, it is sufficient to prove that

```
\alpha^{j-1} E^{V,x}[y_j] \to 0 \text{ as } j \to +\infty.
```

However

```
E^{V,x}[|y_{j+1}| | Y_j] = \Phi^{v_j}[x](y_j)
\le \theta|y_j| + m.
```

hence

```
E^{V,x}[|y_{j+1}|] \le \theta E^{V,x}[|y_j|] + m,
```

from which it follows that

```
E^{V,x}[|y_j|] \le \theta^{j-1}|x| + m \sum_{k=0}^{j-2} \theta^k
\le \theta^{j-1}|x| + m(j-1)\theta^{j-2},
```

since $\theta \ge 1$ without loss of generality. It follows that $\alpha^{j-1} E^{V,x}[y_j] \to 0$ as $j \to \infty$. Therefore the maximum and minimum solutions coincide and there is uniqueness.