# Modeling Availability, Reliability, and Capacity with CTMC

267

![](bbox=[0.213, 0.098, 0.786, 0.337])

Figure 21.53 Two Web-Servers and One Database Server – Availability Model.

considering the two-state CTMC is represented by

$A = \frac{\mu_{eq}}{\lambda_{eq} + \mu_{eq}}$

where the equivalent failure rate, $\lambda_{eq}$, is defined by

$$\lambda_{eq} = \frac{\sum_{i\in S_U} \pi_i \times \lambda_{id}}{\sum_{j\in S_U} \pi_j}$ $(21.11.1)$

$S_U$ is the set of states (in the multi-state model) in which the system is operational, $S_{U/D}$ is the set of states of the multi-state CTMC in which the system is operational, and there is one leaving arrow to a downgrade. The state assigned to such an arrow is named $\lambda_{ed}$, and $\pi_e$ and $\pi_j$ are state probabilities. Finally, it is worth noting that the equivalent failure rate $(\lambda_{eq})$ is an output rate conditioned to the system having in an operational state.