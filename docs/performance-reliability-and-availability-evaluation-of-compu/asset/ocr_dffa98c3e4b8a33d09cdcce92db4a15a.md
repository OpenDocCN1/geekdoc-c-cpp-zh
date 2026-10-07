# Performance, Reliability, and Availability Evaluation of Computational Systems

Table 20.10

# Three Components Systems - 2003 System

| Event | x2 | x1 | x0 | $\Phi_{2003}(\mathbf{X})$ | $p_2$ | $p_1$ | $p_0$ |
| --- | --- | --- | --- | --- | --- | --- | --- |
| $E_0$ | 0 | 0 | 0 | 0 | $UR(t)$ | $UR(t)$ | $UR(t)$ |
| $E_1$ | 0 | 0 | 1 | 0 | $UR(t)$ | $UR(t)$ | $R(t)$ |
| $E_2$ | 0 | 1 | 0 | 0 | $UR(t)$ | $R(t)$ | $R(t)$ |
| $E_3$ | 0 | 1 | 1 | 1 | $UR(t)$ | $R(t)$ | $R(t)$ |
| $E_4$ | 1 | 0 | 0 | 0 | $R(t)$ | $UR(t)$ | $UR(t)$ |
| $E_5$ | 1 | 0 | 1 | 1 | $R(t)$ | $UR(t)$ | $UR(t)$ |
| $E_6$ | 1 | 1 | 0 | 1 | $R(t)$ | $R(t)$ | $R(t)$ |
| $E_7$ | 1 | 1 | 1 | 1 | $R(t)$ | $R(t)$ | $R(t)$ |

# 20.3 FACTORING METHOD

In Chapters 18 and 19, we also applied the conditioning strategy for obtaining the structure-function of systems and the respective reliability or availability. Usually, this strategy is applied to decompose a system into simpler subsystems for which solutions may be known. This method is particularly interesting for systems whose parallel-series compositions can not be represent due to more complex relations between the system components.

Consider a $n$ independent components, $\{c_i\}$, whose states are represented by the respective variables $x_i$ of the vector $\mathbf{X} = (x_i)|_n$. The structure function $\Phi(\mathbf{X})$ may be re-written by

> $\Phi(\mathbf{X}) = x_i 	imes \Phi(1_i, \mathbf{X}) + (1 - x_i) 	imes \Phi(0_i, \mathbf{X}), \quad (20.3.1)$

Where $\Phi(1_i, \mathbf{X})$ represents the state in which component $c_i$ is operational and the states of the other components are random variables $\Phi(x_1, x_2, \dots, x_n)$. Likewise, $\Phi(0_i, \mathbf{X})$ denotes the state in which component $c_i$ has failed and the states of the other components are random variables. Let us assume $p_i = P(x_i = 1)$ is the probability of the component $i$ being operational (reliability or availability); however, the probability of the system operating (reliability or availability) may be represented by

```
$P(\mathbf{X}) = 1) = P(x_i = 1) 	imes P(\Phi(1_i, \mathbf{X}) = 1) + (1 - x_i) \times P(\Phi(0_i, \mathbf{X}) = 1)$
```

```
$P(\mathbf{X}) = 1) = P(x_i = 1) 	imes P(\Phi(1_i, \mathbf{X}) = 1) + P(1 - x_i = 1) \times P(\Phi(0_i, \mathbf{X}) = 1)$
```

```
$P(\mathbf{X}) = 1) = P(x_i = 1) 	imes P(\Phi(1_i, \mathbf{X}) = 1) + P(x_i = 0) \times P(\Phi(0_i, \mathbf{X}) = 1)$
```

```
$P(\mathbf{X}) = 1) = p_i \times P(\Phi(1_i, \mathbf{X}) = 1) + (1 - p_i) \times P(\Phi(0_i, \mathbf{X}) = 1)$
```

Therefore, if the system is factored considering the state of the component $(x_i)$, the system probability can be computed based on the probability of component $i$