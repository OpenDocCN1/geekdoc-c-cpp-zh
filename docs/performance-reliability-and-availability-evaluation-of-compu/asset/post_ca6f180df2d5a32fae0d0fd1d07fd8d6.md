
# Reliability Block Diagram

```
$$\frac{\partial A}{\partial \mu_{a3}} = \frac{\mu_{a1}\lambda_{a3}\mu_{hw}(\mu_{a21}\lambda_{a22} + \lambda_{a21})(\lambda_{a22} + \mu_{a22})(\lambda_{a3} + \mu_{a3})^2}{(\lambda_{hw} + \mu_{hw})(\lambda_{os} + \mu_{os})}$
```

Assuming the respective MTTFs and MTTRS are presented in Table 18.10, the availability sensitivity of each parameter is shown in Table 18.13. The parameters are presented in order of significance. It is worth mentioning that a positive number implies a positive impact on the availability. On the other hand, negative numbers depict the opposite relation.

# Table 18.13 Availability Sensitivity

| Parameter $p_i$ | $\partial A/\partial p_i$ | Component |
|---|---|---|
| $\lambda_{hw}$ | $-19.8378$ | $hw$ |
| $\lambda_{os}$ | $-7.90935$ | $os$ |
| $\lambda_{a1}$ | $-3.95993$ | $a_1$ |
| $\mu_{os}$ | $3.16374 \times 10^{-2}$ | $os$ |
| $\mu_{hw}$ | $1.46947 \times 10^{-2}$ | $hw$ |
| $\lambda_{a3}$ | $-1.28233 \times 10^{-2}$ | $a_{22}$ |
| $\mu_{a1}$ | $1.05598 \times 10^{-2}$ | $a_1$ |
| $\lambda_{a22}$ | $-7.38624 \times 10^{-3}$ | $a_{22}$ |
| $\lambda_{a21}$ | $-4.92924 \times 10^{-3}$ | $a_{21}$ |
| $\mu_{a3}$ | $3.20581 \times 10^{-5}$ | $a_3$ |
| $\mu_{a22}$ | $1.58277 \times 10^{-5}$ | $a_{22}$ |
| $\mu_{a21}$ | $5.47693 \times 10^{-6}$ | $a_{21}$ |

![](img/2d1450514bb14a0cdf0eb5048614afab_143_0.png)

Consider a system composed of $n$ components with reliability $R(t)$ at time $t$. We may be interested in quantifying the reliability improvement if a component $i$ is replaced by a perfect component, that is $R_i(t) = 1$. The difference $R(1, \mathbf{X}(t)) - R(\mathbf{X}(t))$ is defined as the **Improvement Potential** (IP) with respect to component $i$, and it is denoted by $IP_i$ [352].

```
$IP_t = R(1_i, \mathbf{X}(t)) - R(\mathbf{X}(t)) \quad (18.9.11)$
```

# 128 Performance, Reliability, and Availability Evaluation of Computational Systems

As $I_i^B = \partial R_s(t) \partial R_i(t)$ (see Equation 18.9.2), it can also be represented by the slope of Figure 18.39, since

```
$$\frac{\partial R_s(t)}{\partial R_i(t)} = \frac{R_s(1_i, \mathbf{X}(t)) - R_s(\mathbf{X}(t))}{1 - R_i(t)}$$
```

Hence

```
$$I_i^B(t) = \frac{R_s(1_i, \mathbf{X}(t)) - R_s(\mathbf{X}(t))}{1 - R_i(t)}$$
```

```
$IP_i(t) = I_i^B(t) \times (1 - R_i(t)). \quad (18.9.12)$$
```

![](img/2d1450514bb14a0cdf0eb5048614afab_144_0.png)

**Figure 18.39** Reliability Importance - Slope.

In practice, it is not possible to improve the reliability of component $i$ to 1. Therefore, let us consider it is possible to improve the component $i$'s reliability from $R_i(t)$ to $R_i'(t)$. The **Credible Improvement Potential** (CIP) of component $i$ at time $t$ is defined by

```
$$CIP_i(t) = R(R_i'(t), \mathbf{X}(t)) - R(\mathbf{X}(t)), \quad (18.9.13)$$
```

$R(R_i'(t), \mathbf{X}(t))$ denotes the system reliability if the component $i$'s reliability at time $t$ is $R_i'(t)$. It is worth noting that these indexes may also be normalized.

# Reliability Block Diagram

**Example 18.9.11.** Let us consider the system depicted in Figure 18.34. The system reliability at $t = 800h$ is $R(800h) = 0.28594$. The improvement potential of each component at $t = 800h$ is shown in $IP_i$ of Table 18.15. Assuming the maximal reliability component can achieve is shown in Table 18.14, the credible improvement potential of each component is presented in $CIP_i$ of Table 18.15.

# Table 18.14 - Maximal Reliability

| Component | $R_i(800h)$ |
|---|---|
| $hw$ | 0.9 |
| $os$ | 0.9 |
| $a_1$ | 0.9 |
| $a_{21}$ | 0.9 |
| $a_{22}$ | 0.9 |
| $a_3$ | 0.9 |

# Table 18.15 - Improvements and Credible Reliability

| Component | $R(1_i, \mathbf{X}(800h))$ | $R(R_i(800h), \mathbf{X}(800h))$ | $IP_i$ | $CIP_i$ |
|---|---|---|---|---|
| $hw$ | 0.24954 | 0.29159 | 0.00860 | 0.00565 |
| $os$ | 0.42657 | 0.38391 | 0.14063 | 0.09779 |
| $a_1$ | 0.48741 | 0.43867 | 0.20147 | 0.15273 |
| $a_{21}$ | 0.31638 | 0.30789 | 0.03044 | 0.02195 |
| $a_{22}$ | 0.32786 | 0.31823 | 0.04192 | 0.03229 |
| $a_3$ | 0.38176 | 0.35741 | 0.09582 | 0.07147 |

Figure 18.40 also presents the reliability improvements (a) and credible reliability improvements (b) of each component at $t = 800h$.

![](img/2d1450514bb14a0cdf0eb5048614afab_145_0.png)

**Risk Achievement Worth (RAW)** is an importance measure that quantifies the ratio of the system unreliability given the component $i$ has failed (or is not present) with the actual system unreliability [352]. The RAW presents a measure that indicates the importance of maintaining the current level of reliability for the component.

$I_{RAW}(t) = \frac{1 - R_i(0,\mathbf{X}(t))}{1 - R_s(t)} \quad (18.9.14)$

where $R_s(t)$ is the system reliability at $t$, and $R_i(0,\mathbf{X}(t))$ is the system reliability given component $i$ has failed (or is not present). It is worth mentioning that the RAW importance measure has also been adapted to consider steady-state availability [352].

**Example 18.9.12.** Consider the system depicted in Figure 18.34. The system reliability at $t = 800h$ is $R(800h) = 0.28594$. The RAW importance measure of each component at $t = 800h$ is shown in column $I^{RAW}$ of Table 18.16.

# Table 18.16 - Risk Achievement Worth - $I^{RAW}$

| Component | $R(0,\mathbf{X}(800h))$ | $I^{RAW}$ |
|---|---|---|
| $hw$ | 0 | 1.40045 |
| $os$ | 0 | 1.40045 |
| $a_1$ | 0 | 1.40045 |
| $a_{21}$ | 0.23155 | 1.07617 |
| $a_{22}$ | 0.23155 | 1.07617 |
| $a_3$ | 0.38176 | 0.86581 |

# Reliability Block Diagram

The Risk Reduction Worth (RRW) importance is the ratio of the actual system unreliability with the system unreliability given component $i$ is replaced by a perfect component $(R_i(t) = 1)$ [352].

```
$I_i^{RRW}(t) = \frac{1 - R_s(t)}{1 - R_s(1_i,\mathbf{X}(t))} \quad (18.9.15)$
```

where $R_s(t)$ is the system reliability at $t$, and $R_s(1_i,\mathbf{X}(t))$ is the system reliability given component $i$.

**Example 18.9.13.** Consider the system in Figure 18.34. The system reliability at $t = 800h$ is $R(800h) = 0.28594$. The RRW importance measure of each component at $t = 800h$ is shown in column $I_i^{RRW}$ of Table 18.17.

# Table 18.17 Risk Reduction Worth - $I^{RRW}$

| Component | $R(1_i,\mathbf{X}(800h))$ | $I_i^{RRW}$ |
|---|---|---|
| $hw$ | 0.29453 | 1.01219 |
| $os$ | 0.42657 | 1.24525 |
| $a_1$ | 0.48741 | 1.39305 |
| $a_{21}$ | 0.31638 | 1.04452 |
| $a_{22}$ | 0.32786 | 1.06237 |
| $a_3$ | 0.38176 | 1.15499 |

![](img/2d1450514bb14a0cdf0eb5048614afab_147_0.png)

There are two definitions of criticality importance of components. One definition considers the system success and the second is specified in terms of the system failure. It is worth noting that a system is critical if a given state $\mathbf{X}$ is $\Phi(1,\mathbf{X}) = 1$ and $\Phi(0,\mathbf{X}) = 0$ (see Section 18.8), and that is equivalent to $\Phi(1,\mathbf{X}) - \Phi(0,\mathbf{X}) = 1$.

The criticality importance of a component may be defined as the probability of component being critical to the system operation (success) and the component $i$ is operational, given the system is operational, then the criticality importance for success is

```
$I_i^{CS} = \frac{R_s(1_i,\mathbf{X}(t)) - R_s(0_i,\mathbf{X}(t))}{R_s(\mathbf{X}(t))} \quad (18.9.15)$
```

# 132 Performance, Reliability, and Availability Evaluation of Computational Systems

Hence

```
$I_i^{CS} = I_i^B \frac{R_i(t)}{R_i(\mathbf{X}(t))} \quad (18.9.17)$
```

The criticality importance of component $i$ in terms of success quantifies the probability that a component $i$ is working and is the one that supports the system operational state. Thus, the higher this index, the higher is the chance of the component $i$ being the one contributes to the system operational state [224].

The criticality importance may also be defined in terms of failure. This definition quantifies the probability that component $i$ has failed and is the one that contributes to the system failure given the system has failed [224].

```
$I_i^{CF} = \frac{UR_s(1_i,\mathbf{X}(t)) - UR_s(0,\mathbf{X}(t))}{UR_s(\mathbf{X}(t))} \quad (18.9.18)$
```

```
$I_i^{CF} = I_i^B \frac{UR_i(t)}{UR_s(\mathbf{X}(t))} \quad (18.9.19)$
```

**Example 18.9.14.** Consider the system depicted in Figure 18.34. The system reliability at $t = 800h$ is $R(800) = 0.28594$. The system reliabilities at $t = 800h$ when each component is operational in column $R_s(1_i,\mathbf{X}(t))$ of Table 18.18. Like, the system reliability at $t = 800h$ when each component has failed are depicted in column $R_s(0_i,\mathbf{X}(t))$. The component reliabilities at $t = 800h$ are presented in column $R_i(t)$.

# Table 18.18 Criticality Importance - $I_i^{CS}$ and $I_i^{CF}$

| Component | $R_1(\mathbf{X}(800h))$ | $R_0(\mathbf{X}(800h))$ | $R_i(800h)$ | $I_i^{CS}$ | $I_i^{CF}$ |
|---|---|---|---|---|
| $hw$ | 0.29454 | 0 | 0.97081 | 1 | 0.01204 |
| $os$ | 0.42657 | 0 | 0.67032 | 1 | 0.19695 |
| $a_1$ | 0.48741 | 0 | 0.58665 | 1 | 0.28215 |
| $a_{21}$ | 0.31638 | 0.23155 | 0.64118 | 0.1921 | 0.04263 |
| $a_{22}$ | 0.32786 | 0.23155 | 0.56472 | 0.1901 | 0.05871 |
| $a_3$ | 0.38176 | 0.38176 | 0.60653 | 0 | 0 |
