# Performance, Reliability, and Availability Evaluation of Computational Systems

![](bbox=[0.118, 0.098, 0.881, 0.365])

**Figure 16.6** Hazard Rate: (a) Decreasing, (b) Constant, (c) Increasing, (d) Bathtub curve.

Thus

> $MTTF = \int_{0}^{\infty} R(t)dt,$ (16.2.11)

and

> $MTTF = \int_{0}^{\infty} (1 - F_T(t))dt,$ (16.2.12)

which is often easier to compute using 16.2.10.

Another central tendency reliability measure is the **median time to failure (MedTTF)**, defined by the time instant, $t$, when $R(t) = 0.5$. The $MedTTF$ divides the failure into two halves, where 50% of failures occur before MedTTF and the other 50% after (see Figure 16.5).

**Example 16.2.1.** Assume the CDF of the time failure of the computational system is represented by

> $F_T(t) = 1 - \frac{1}{30 	imes 10^{-6}t^2 + 1}$

where $t$ is the time in hours. Compute (a) $F_T(720h)$, **(b)** the reliability at $t=720h$, **(c)** $\lambda(t)$ at 720h, and **(d)** **MTTF**.

> $F_T(720h) = 1 - \frac{1}{30 	imes 10^{-6} 	imes 720^2 + 1} = 0.9396$.