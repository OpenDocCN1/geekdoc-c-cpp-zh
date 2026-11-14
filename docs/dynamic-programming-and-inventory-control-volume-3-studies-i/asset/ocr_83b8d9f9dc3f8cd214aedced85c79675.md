# Lemma 9.1. The set of $v$ in the right hand side of equation (9.1.7) can be bounded by

```
(9.1.8) $$ cv \le \frac{K+cD}{1-\alpha} + \frac{\alpha Dh}{(1-\alpha)^2}. $$
```

PROOF. The result will follow from the estimate

```
$$ u(x) \ge \frac{hx}{1-\alpha} - \frac{\alpha Dh}{(1-\alpha)^2}, $$
```

which is obtained by iterating on the functional equation (9.1.7), starting with $u(x) \ge hx$. Next, we look for a ceiling function for $u(x)$. Because of the constraint, we cannot as usual the function corresponding to the choice $v=0$. We shall take $v=D$. So we consider the functional equation

```
$$ w_0(x) = hx + K + cD + \alpha w_0(x), $$
```

which is simply

```
(9.1.9) $$ w_0(x) = \frac{hx + K + cD}{1 - \alpha}. $$
```

We look for solutions of (9.1.7) which are in the interval $0 \le u(x) \le w_0(x)$. From the bound below of $u$ and the bound above provided by the ceiling function, we deduce from the equation (9.1.7), that the values of $v$ can be restricted by the constraint

```
$$ hx + cv + \frac{\alpha h(x-D)}{1-\alpha} - \frac{hD\alpha^2}{(1-\alpha)^2} \le \frac{hx + K + cD}{1-\alpha}. $$
```

We see that the term in $x$ drops out, and there remains the estimate (9.1.8). This concludes the proof.

Since the set of $v$ is bounded, we can apply the techniques of Theorem (4.2.4) to claim

# **Theorem 9.1.** Under the assumption (9.1.6), the functional equation (9.1.7) has one and only one solution which is l.s.c. This solution is the value function (9.1.5). Moreover there exists an optimal control policy $\tilde{v}$ defined by a feedback $\tilde{v}(x)$, which achieves the infimum in the right hand side of (9.1.7).

# ## 9.1.3. OBTAINING THE OPTIMAL CONTROL POLICY.

In this section we are interested in characterizing the optimal feedback $\tilde{v}(x)$. We first give a different, more convenient form of the equation (9.1.7). We introduce

```
(9.1.10) $$ z(x) = cx + \alpha u(x). $$
```

Then it is fairly easy to rewrite equation (9.1.7) as follows

```
(9.1.11) $$ u(x) = (h-c)x + cD + \inf_{\eta \ge \max(x, D)} [K \mathbb{1}_{\eta > x} + z(\eta - D)]. $$
```

We begin with the inequality

# **Lemma 9.2.**

```
(9.1.12) $$ z(x) \le K + z(y), \forall y > x. $$
```