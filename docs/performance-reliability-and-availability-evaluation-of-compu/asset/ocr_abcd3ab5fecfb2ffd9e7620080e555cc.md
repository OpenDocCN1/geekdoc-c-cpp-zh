# 128 Performance, Reliability, and Availability Evaluation of Computational Systems

As $I_i^B = \partial R_s(t) \partial R_i(t)$ (see Equation 18.9.2), it can also be represented by the slope of Figure 18.39, since

```
$$\frac{\partial R_s(t)}{\partial R_i(t)} = \frac{R_s(1_i, \mathbf{X}(t)) - R_s(\mathbf{X}(t))}{1 - R_i(t)}$$$
```

Hence

```
$$I_i^B(t) = \frac{R_s(1_i, \mathbf{X}(t)) - R_s(\mathbf{X}(t))}{1 - R_i(t)}$$$
```

```
$IP_i(t) = I_i^B(t) \times (1 - R_i(t)). \quad (18.9.12)$$
```

![](bbox=[0.121, 0.373, 0.878, 0.613])

**Figure 18.39** Reliability Importance - Slope.

In practice, it is not possible to improve the reliability of component $i$ to 1. Therefore, let us consider it is possible to improve the component $i$'s reliability from $R_i(t)$ to $R_i'(t)$. The **Credible Improvement Potential** (CIP) of component $i$ at time $t$ is defined by

```
$$CIP_i(t) = R(R_i'(t), \mathbf{X}(t)) - R(\mathbf{X}(t)), \quad (18.9.13)$$
```

$R(R_i'(t), \mathbf{X}(t))$ denotes the system reliability if the component $i$'s reliability at time $t$ is $R_i'(t)$. It is worth noting that these indexes may also be normalized.