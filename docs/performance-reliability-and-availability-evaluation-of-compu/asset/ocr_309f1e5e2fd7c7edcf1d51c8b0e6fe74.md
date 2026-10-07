# 248 Performance, Reliability, and Availability Evaluation of Computational Systems

![](bbox=[0.193, 0.097, 0.806, 0.344])

Failure Detected and Successful Switchover - 100% of the Workload Being.

# ### Figure 21.33 Active-Active Servers – One Server Available.

failed server may be repaired; thus taking the system back to state $S_0$ with a rate of $\mu$. Thus, the second server may fail; thus reaching state $S_7$ with a rate of $\lambda$. The third event is the successful manual switchover, which takes the system to state $S_2$ with a rate of $m 	imes \alpha$. The last event is the unsuccessful switchover, which transitions the system to state $S_3$ with a rate of $(1 - m) 	imes \alpha$. In state $S_5$, the system only handles 50% of the HTTP requests. In state $S_0$, two events are possible: first, the failed server may be repaired. This events the system back to state $S_0$ with a rate of $\mu$. The other possible event is the second server failure, which turns the system unavailable by reaching state $S_7$ with a rate of $\lambda$. It is assumed there is only one repair facility. Therefore, a repair takes the system from state $S_7$ to state $S_2$.

The system availability is estimated from

> $A = 1 - \pi_{S_7},$$

which leads to

> $A = \frac{\mu(\mu((3-2c)\lambda + \delta) + 2\lambda(\delta + \lambda))}{\mu^2((3-2c)\lambda + \delta) + 2\lambda\mu((c-2)\lambda) + 2\lambda^2(\delta + \lambda))} \quad (21.7.7)$

The capacity ordered is calculated using

> $COA = \frac{2 	imes \pi_{S_0} + \pi_{S_2} + 0.5 	imes \sum_{i \in \{1,3,4,5,6\}} \pi_{S_i}}{2}, \quad (21.7.8)$