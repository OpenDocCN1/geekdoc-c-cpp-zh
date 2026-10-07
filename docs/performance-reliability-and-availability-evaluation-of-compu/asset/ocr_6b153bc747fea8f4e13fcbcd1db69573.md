# Reliability Block Diagram

125

![](bbox=[0.125, 0.105, 0.875, 0.411])

Parameters: $\lambda_{hw}, \lambda_{os}, \lambda_{u21}, \lambda_{u22},$ and \lambda_{u3}$ for $t \in (0, 2500h)$.

**Figure 18.38** Reliability Sensitivity Analysis.

# Table 18.12 Reliability Sensitivity at $t = 600h$

| Parameter | $\partial R(t)/\partial\lambda_i$ |
| --- | --- |
| $\lambda_{hw}$ | -242.813 |
| $\lambda_{os}$ | -242.813 |
| $\lambda_{u1}$ | -242.813 |
| $\lambda_{u21}$ | -42.5349 |
| $\lambda_{u22}$ | -42.5349 |
| $\lambda_{u3}$ | -106.793 |

Now, let us analyze how system availability is affected by changes in a parameter $p_i$. The system **availability sensitivity** can be measured by

```
$S_{P_i}^A = \frac{\partial A}{\partial p_i}. \quad (18.9.10)$
```

**Example 18.9.10.** Considering the system depicted in Figure 18.34, the availability sensitivity with respect to the parameters $\lambda_{hw}, \mu_{hw}, \lambda_{os}, \mu_{os}, \lambda_{u1}, \mu_{u1}, \lambda_{u21}, \mu_{u21}, \lambda_{u22}, \mu_{u22}, \lambda_{u3},$ and $\mu_{u3}$ are shown in the following.