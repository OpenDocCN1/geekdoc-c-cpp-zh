# 102 Performance, Reliability, and Availability of Computational Systems

![](bbox=[0.118, 0.103, 0.881, 0.235])

# ## 18.23 Reliability (a) - Density Function (b) - Hazard Function (c) - Bridge Structure.

The median time to failure can be obtained by finding $t$ such that $R(t) = 0.5$. The median time to failure is $MeTTF = 6931.47h$, as mode time to failure is the time that maximizes the density function. In this example, $ModeTTF = 4558.75h$.

If $p_i$ in Expression 18.5.43 is the component $i$'s availability, then the system availability is

$A = A_3 \times ((1 - ((1 - A_1) \times (1 - A_4))) \times (1 - ((1 - A_2) \times (1 - A_5)))) + (1 - A_3) \times (1 - ((1 - A_{12}) \times (1 - A_{45})))),$ (18.5.52)

where $A_i = MeTTF / (MeTTF + MTTR_i)$.

If the time to repair and the availability of each block are exponentially distributed with rates $\mu$ and $\lambda$; then the availability of each block is $A_i = \mu / (\lambda + \mu)$. Hence, system availability is

$A = \frac{\mu}{\lambda + \mu} \times (1 - (1 - \frac{\mu}{\lambda + \mu})^2) + (1 - \frac{\mu}{\lambda + \mu}) \times (1 - (\frac{\mu}{\lambda + \mu})^2)),$ (18.5.53)

which leads to

$A = \frac{\mu^2(2\lambda^3 + 8\lambda^2\mu + 5\lambda\mu^2 + \mu^3)}{(\lambda + \mu)^5}}$ ($18.5.54)

**Figure 18.5.8.** Figure 18.24 shows the availability in number of nines of the bridge structure with five similar blocks. The time to failure and the time to repair of each block are exponentially distributed with parameters $\lambda = 10^{-4}f/h$ and $\mu \in \{5 \times 10^{-2}r/h, 7.5 \times 10^{-2}r/h, 10^{-1}r/h\}$, respectively.