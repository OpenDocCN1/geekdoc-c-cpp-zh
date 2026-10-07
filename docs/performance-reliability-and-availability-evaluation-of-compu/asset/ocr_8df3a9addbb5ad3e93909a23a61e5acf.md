# Performance Reliability, and Availability Evaluation of Computational Systems

If $\lambda_{s1} = \lambda_{s2} = \lambda_s$, then

```
$R(t)_{hw} = (1 - (1 - e^{-\lambda_s t})^2) \times \prod_{i\in{MB,NC,VC,DC,D\}} e^{-\lambda_i t}$.
```

![](bbox=[0.124, 0.209, 0.876, 0.396])

**Figure 18.15** Computer System – RBD.

Assuming the failure rates shown in Table 18.6, the hardware mean to failure can be computed by $MTTF_{hw} = \int_0^\infty R(t)_{hw} dt$.

```
$MTTF_{hw} = \frac{2}{\lambda_{d} + \lambda_{dc} + \lambda_{mb} + \lambda_{nc} + \lambda_{s} + \lambda_{vc}} = \frac{1}{\lambda_{d} + \lambda_{dc} + \lambda_{mb} + \lambda_{nc} + 2\lambda_{s} + \lambda_{vc}}$
```

The mean time to failure is $MTTF_{hw} = 2712.934h$. The hardware reliability is depicted in Figure 18.16.a.

The steady-state availability is computed by

```
$A_{cs} = A_{hw} \times A_{os} \times A_{a1} \times (1 - ((1 - A_{a3}) \times (1 - A_{a21} \times A_{a22})))$
```

Now assume the time to repair the hardware, and the software components are exponentially distributed with the parameters presented in Table 18.7. The steady-state system availability is $A = 0.99694$, the mean time to failure is $MTTF = 638.7h$, the system mean to restore is $MTTR = 1.963h$, and the downward-time in hours is $DT = 26.85724h$.

Assuming the mean time to repair each program application ($MTT_a$) module is equal, Figure 18.16.b shows the system availability (number of nines) for $MTT_a = \{0.1, 0.2, 0.3, 0.4, 0.5\}$.