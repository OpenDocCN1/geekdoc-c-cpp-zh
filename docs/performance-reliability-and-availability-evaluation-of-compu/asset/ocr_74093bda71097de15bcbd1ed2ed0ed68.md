# Combinatorial Model Analysis

![](bbox=[0.198, 0.13, 0.802, 0.568])

**Figure 20.2** Two Servers and Two Storage Devices and FT.

Table 20.4 shows the respective structure variables and the structure function evaluation. Here, it is important to remember that a Boolean variable $b_i$ implies $x_i = 0$, and $b_i$ corresponds to $x_i = 1$ (see rules presented in Table 18.3).

Assume the MTTFs and the MTTRs of each component are depicted in Table 20.5. The steady-state availability of each component is calculated by $A_i = MTTF_i/(MTTF_i+MTTR_i)$. Table 20.6 shows the events that evaluates the structure function $\Phi(X)$ to one, and the respective availability or unavailability of component in each specific event (state).

Consider we are interested in the system steady-state availability. For each state in which $\Phi(X) = 1$, we multiply the probability – (un)availability of each component. If the state of a component $j \in \{S_1, S_2, NAS_1, NAS_2\}$ is $x_j = 0$, we consider the