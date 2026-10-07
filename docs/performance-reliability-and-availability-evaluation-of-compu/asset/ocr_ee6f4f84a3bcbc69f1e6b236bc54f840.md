# Performance, Reliability, and Availability of Computational Systems

# Reliability  #9s

![](bbox=[0.125, 0.116, 0.875, 0.276])

**Figure 18.16** Reliability (a) - Availability in #9s (b).

exactly K out of the N servers are operational, the data center is considered operational. One possible outcome $(X_N)$ of the observation is when servers 1, 2, ..., k are operational, and servers $k+1, k+2, ..., n$ have failed. This outcome is depicted by

$X_N = (x_1, x_2, ..., x_{k-1}, x_k, x_{k+1}, ..., x_n)$.

$X_1 = (1, 1, ..., 1, 0, ..., 0)$.

Let $Y_1 = \sum_{i=1}^K x_i$ be the total number of operational servers observed in the outcome $x_1$.

Therefore, if $P(x_i = 1)$ is the probability of server $i$ being operational, the probability of having exactly $K$ out of the $N$ servers operational is

> $P(Y_1 = K) = \prod_{i=1}^K P(x_i = 1) 	imes \prod_{i=K+1}^n P(x_i = 0)$.

If the mean time to failure of the system's components is i.i.d., then

> $P(Y_1 = K) = P(x = 1)^K 	imes P(x = 0)^{N-K}$.

If $P(x = 1)$ is the component's reliability $(R_c(t))$, and $P(x = 0)$ is the component's unreliability $(UR_c(t))$, then

> $P(Y_1 = K) = R_c(t)^K 	imes UR_c(t)^{N-K}$.

Thus,

> $P(Y_1 = K) = R_c(t)^K 	imes (1 - R_c(t))^{N-K}$.