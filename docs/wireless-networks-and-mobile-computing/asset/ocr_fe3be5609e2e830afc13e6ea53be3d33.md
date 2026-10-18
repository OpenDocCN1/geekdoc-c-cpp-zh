# **TABLE 3.6:** Frequency separation matrix for Scheme 2

| Nodes ↓ / → | a | b | c | d | e | f | g | h | i |
|---|---|---|---|---|---|---|---|---|---|
| **a** | 0 | $s_1$ | $s_1$ | $s_1$ | $s_1$ | $s_2$ | $s_1$ | $s_1$ | $s_2$ |
| **b** | $s_1$ | 0 | $s_1$ | $s_2$ | $s_1$ | $s_1$ | $s_2$ | $s_1$ | $s_1$ |
| **c** | $s_1$ | $s_1$ | 0 | $s_1$ | $s_2$ | $s_1$ | $s_1$ | $s_2$ | $s_1$ |
| **d** | $s_1$ | $s_2$ | $s_1$ | 0 | $s_1$ | $s_1$ | $s_1$ | $s_2$ | $s_1$ |
| **e** | $s_1$ | $s_1$ | $s_2$ | $s_1$ | 0 | $s_1$ | $s_1$ | $s_1$ | $s_2$ |
| **f** | $s_2$ | $s_1$ | $s_1$ | $s_1$ | $s_1$ | 0 | $s_2$ | $s_1$ | $s_1$ |
| **g** | $s_1$ | $s_2$ | $s_1$ | $s_1$ | $s_1$ | $s_2$ | 0 | $s_1$ | $s_1$ |
| **h** | $s_1$ | $s_1$ | $s_2$ | $s_2$ | $s_1$ | $s_1$ | $s_1$ | 0 | $s_1$ |
| **i** | $s_2$ | $s_1$ | $s_1$ | $s_1$ | $s_2$ | $s_1$ | $s_1$ | $s_1$ | 0 |

frequency assignment to nodes of the entire cellular network following the assignment patterns shown in Figure 3.14, without conflict.

We now use the *Algorithm GA* over the nine-node subgraph of Figure 3.13 with the frequency separation requirements given by Table 3.6. Depending on the relationship between $s_1$ and $s_2$, the results of the algorithm can be stated by the following two lemmas.

**Lemma 4.** *In a hexagonal cellular network of two-band buffering with a demand of only one channel per cell, there exists a frequency assignment scheme which requires a bandwidth of $8s_2$ for $s_2 < s_1 \leq 2s_2$.*

**Proof:** For the case when $s_2 < s_1 \leq 2s_2$, the *Algorithm GA* gives the result such that $\phi(a) = (0, 0)$, $\phi(b) = (0, 6)$, $\phi(c) = (0, 3)$, $\phi(d) = (0, 5)$, $\phi(e) = (0, 2)$, $\phi(f) = (0, 8)$, $\phi(g) = (0, 7)$, $\phi(h) = (0, 4)$ and $\phi(i) = (0, 1)$. Note that, the inequality $2s_2 \geq s_1$ has been used here because the frequencies $(0, 6)$ and $(0, 8)$ are assigned to nodes that are Distance 1 apart from each other. In this case, the maximum frequency assigned is $(0, 8)$. This assignment is shown in Figure 3.15 and obtained by replacing the values of $\phi(a)$, $\phi(b)$, $\phi(c)$, $\phi(d)$, $\phi(e)$, $\phi(f)$, $\phi(g)$, $\phi(h)$, and $\phi(i)$ by $(0, 0)$, $(0, 6)$, $(0, 3)$, $(0, 5)$, $(0, 2)$, $(0, 8)$, $(0, 7)$, $(0, 4)$, and $(0, 1)$, respectively, in Figure 3.14.