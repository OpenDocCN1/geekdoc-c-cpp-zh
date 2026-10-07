# Reliability Block Diagram

The Risk Reduction Worth (RRW) importance is the ratio of the actual system unreliability with the system unreliability given component $i$ is replaced by a perfect component $(R_i(t) = 1)$) [352].

```
$I_i^{RRW}(t) = \frac{1 - R_s(t)}{1 - R_s(1, \mathbf{X}(t))}. \quad (18.9.15)$
```

where $R_s(t)$ is the system reliability at $t$, and $R_s(1_i, \mathbf{X}(t))$ is the system reliability given component $i$.

**Example 18.9.13.** Consider the system in Figure 18.34. The system reliability at $t = 800h$ is $R(800h) = 0.28594$. The RRW importance measure of each component at $t = 800h$ is shown in column $I_i^{RRW}$ of Table 18.17.

# **Table 18.17**
Risk Reduction Worth - $r^{RRW}$

| Component | $R(1, \mathbf{X}(800h))$ | $I_i^{RRW}$ |
|---|---|--|
| $hw$ | 0.29453 | 1.01219 |
| $os$ | 0.42657 | 1.24525 |
| $a_1$ | 0.48741 | 1.39305 |
| $a_{21}$ | 0.31638 | 1.04452 |
| $a_{22}$ | 0.32786 | 1.06237 |
| $a_3$ | 0.38176 | 1.15499 |

![](bbox=[0.855, 0.615, 0.875, 0.628])

There are two definitions of *criticality importance* of components. One definition considers the system success and the second is specified in terms of the system failure. At it is worth noting that a system is critical if a given state $\mathbf{X}$ is $\Phi(1, \mathbf{X}) = 1$ and $\Phi(0, \mathbf{X}) = 0$ (see Section 18.8), and that it is equivalent to

$\Phi(1, \mathbf{X}) - \Phi(0, \mathbf{X}) = 1$.

The criticality importance of a component may be defined as the probability of that component being critical to the system operation (success) and the component $i$ is operational, given the system is operational, then the criticality importance for success is

```
$I_i^{CS} = \frac{R_s(1_i, \mathbf{X}(t)) - R_s(0_i, \mathbf{X}(t)) R_s(t)}{R_s(\mathbf{X}(t))}. \quad (18.9.15)$
```