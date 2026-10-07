# Performance, Reliability, and Availability of Computational Systems

![](bbox=[0.196, 0.097, 0.803, 0.517])

Figure 21.23 Router Infrastructure – Hardware and OS.

which is

$R(t) = R_{MB}(t) \times R_{IC_1}(t) \times R_{IC_2}(t) \times R_{PS}(t) \times R_{OS}(t).$

As $R_i(t) = e^{-\lambda_it}, i \in \{MB, IC_1, IC_2, PS\}$, then $R(t) = e^{-\sum_{i\in \{MB, IC_1, IC_2, PS\}} \lambda_it}$. Therefore the router failure rate is

$$\lambda_R = \sum_{i\in \{MB, IC_1, IC_2, PS\}} \lambda_i,$$

and the mean time to failure is

$MTTF_R = 1/\lambda_R.$

Table 21.2 shows the failure rates of each component. Considering these rates, router failure rates are $\lambda_R = 3.54 \times 10^{-4} f ph$, and $MTTF_R = 2822.58h$.