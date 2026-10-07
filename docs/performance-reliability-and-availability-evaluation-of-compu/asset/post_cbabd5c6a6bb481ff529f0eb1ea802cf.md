
# 204 Performance Reliability, and Availability Evaluation of Computational Systems

Considering $MP_1$, we get

$P_1 = V_1 = P(MP_1) = p_1p_2$.

The intersections $MP_1^c \cap MP_2$, $MP_1^c \cap MP_2^c \cap MP_3$, and $MP_1^c \cap MP_2^c \cap MP_3^c \cap MP_4$ are represented by

$MP_1^c \cap MP_2 \Rightarrow b_1 \wedge b_2 \wedge b_4 \wedge b_5$,

$MP_1^c \cap MP_2^c \cap MP_3 \Rightarrow b_1 \wedge b_2 \wedge b_3 \wedge b_4 \wedge b_5$,

and

$MP_1^c \cap MP_2^c \cap MP_3^c \cap MP_4 \Rightarrow b_1 \wedge b_2 \wedge b_3 \wedge b_4 \wedge b_5$.

Hence, in the second iteration, we get

$V_2 = P(MP_1^c \cap MP_2^c) = (1 - p_1p_2)p_4p_5$,

and

$P_2 = P_1 + V_2 = P_1 + (1 - p_1p_2)p_4p_5$.

In the third iteration, we obtain

$V_3 = P(MP_1^c \cap MP_2^c \cap MP_3^c) = p_1(1 - p_2)p_3(1 - p_4)p_5$,

and

$P_3 = P_2 + V_3 = P_2 + p_1(1 - p_2)p_3(1 - p_4)p_5$.

In the last iteration, we get

$V_4 = P(MP_1^c \cap MP_2^c \cap MP_3^c \cap MP_4) = (1 - p_1)p_2p_3p_4(1 - p_5)$

and

$P_4 = P_3 + V_4 = P_3 + (1 - p_1)p_2p_3p_4(1 - p_5)$.

Let us consider $p_j = p = 0.9, j \in \{1,2,3,4,5\}$, and compute the bounds $P_j$ for $j \in \{1,2,3,4\}$. Table 20.14 depicts the results.

# Combinatorial Model Analysis

# Table 20.14 Reliability Bounds - SDP

| i | $P_i$ |
|---|---|
| 1 | 0.81 |
| 2 | 0.9639 |
| 3 | 0.97119 |
| 4 | 0.97848 |

# 20.7.3 MIN-MAX BOUND METHOD

Barlow and Proschan proposed a method for estimating success probability (reliability and availability) upper and lower bounds based on minimal path and minimal cuts [346] [224]. For example, assume a system composed of independent components with $l$ minimal path and $m$ minimal cuts, where $\rho_i$ is the probability of the minimal path $MP_i$ is operational, and $\gamma$ is the failure probability of the cut $MC_j$.

As the system is at least reliable as the most reliable minimal path, then we have

$L = \max_{1 \le i \le l}\{\rho_i\}$

On the other hand, the system is at most reliable as the least reliable cuts. Thus,

$U = \min_{1 \le i \le l}\{1 - \gamma_i\}$

Therefore, for the bridge model of Figure 20.10.a, we have

$L = \max\{\rho_1, \rho_2, \rho_3, \rho_4\}$

and

$U = \min\{1 - \gamma_1, 1 - \gamma_2, 1 - \gamma_3, 1 - \gamma_4\}$

where $\rho_1 = p_1p_2$, $\rho_2 = p_4p_5$, $\rho_3 = p_1p_3p_5$, $\rho_4 = p_2p_3p_4$; $\gamma_1 = (1 - p_1)(1 - p_4)$, $\gamma_2 = (1 - p_2)(1 - p_5)$, $\gamma_3 = (1 - p_1)(1 - p_3)(1 - p_5)$, and $\gamma_4 = (1 - p_2)(1 - p_3)(1 - p_4)$. For $p_1 = p_2 = p_3 = p_4 = 0.9$, we have $U = 0.9999$ and $L = 0.9801$.

# 206 Performance, Reliability, and Availability of Computational Systems

# 20.7.4 ESARY-PROCHAN METHOD

This section presents the Esary-Prochan method for estimating probabilities [345] [224]. Assume a system composed of $l$ minimal paths and $m$ minimal cuts. A minimal path is functional if all of its components work; thus, if one component of a minimal path fails, the minimal path fails. Let $\rho_i$ be the success probability (reliability or availability) of minimal path $MP_i$. Consider a parallel system with independent components. In such a system, minimal paths do not share components. As a parallel system, the system only fails if all paths fail; hence failure probability (unavailability) is $Q=\prod_{i=1}^{l}(1-\rho_i)$. For a more general system, however, the failure probability is higher than $\prod_{i=1}^{l}(1-\rho_i)$. Therefore, $U = 1-\prod_{i=1}^{l}(1-\rho_i)$ is a success probability upper bound. Now consider minimal cuts. Applying a similar argument, we obtain success probability (reliability or availability) lower bound: $L = \prod_{j=1}^{m}(1-\gamma_j)$, where $\gamma_j$ is the failure probability of minimal cut $MC_j$.

Let us assume the bridge model shown in Figure 20.10.a. As already seen, this bridge has four minimal paths, $MP_1=\{c_1,c_2\}$, $MP_2=\{c_4,c_5\}$, $MP_3=\{c_1,c_3,c_5\}$, and $MP_4=\{c_2,c_3,c_4\}$, and four minimal cuts, $MC_1=\{c_1,c_4\}$, $MC_2=\{c_2,c_5\}$, $MC_3=\{c_1,c_3,c_5\}$, and $MC_4=\{c_2,c_3,c_4\}$. Here $\rho_1=p_1p_2$, $\rho_2=p_4p_5$, $\rho_3=p_1p_3p_5$, $\rho_4=p_2p_3p_4$; $\gamma_1=(1-p_1)(1-p_4)$, $\gamma_2=(1-p_2)(1-p_5)$, $\gamma_3=(1-p_1)(1-p_3)(1-p_5)$, and $\gamma_4=(1-p_2)(1-p_3)(1-p_4)$. Therefore, $U = (1-\rho_1)(1-\rho_2)(1-\rho_3)(1-\rho_4)$ and $L = (1-\gamma_1)(1-\gamma_2)(1-\gamma_3)(1-\gamma_4)$. For $p_1=p_2=p_3=p_4=p_5=0.9$, we have $U=0.997349$ and $L=0.978141$.

# Combinatorial Model Analysis

# 20.7.5 DECOMPOSITION

The reliability/availability evaluation of a large system is usually performed by decomposing the system into a subsystem. Each subsystem is decomposed into a smaller subsystem. This process stops when the analyst decides the subsystem is simple enough to be evaluated. Then, the smaller subsystems are evaluated and considered one component (reduction) in the higher-level subsystem. As already presented in Section 20.4, such an approach can be applied to obtain exact results or bounds.

To calculate bounds, after decomposing the system into smaller subsystems, the subsystems can be evaluated using any of those methods already introduced here to calculate bounds, and then reducing each subsystem and representing them as one component with the respective bounds obtained at the higher-level.

Consider a system represented by the RBD depicted in Figure 20.13.a. This model is composed of twenty-one blocks, $\{b_i\}, i \in \{1, 2, \dots, 21\}$. This model was decomposed into three subsystems, $S_1, S_2$ and $S_3$, as shown in Figure 20.13. The subsystem $S_1$ has three minimal paths and four minimal cuts. The minimal paths are:

$MP_1^1 \Rightarrow b_1 \wedge b_2$,

$MP_2^1 \Rightarrow b_1 \wedge b_3$,

and

$MP_3^1 \Rightarrow b_4 \wedge b_5$.

The minimal cuts are:

$MC_1^1 \Rightarrow \overline{b_1} \wedge \overline{b_4}$,

$MC_2^1 \Rightarrow \overline{b_1} \wedge \overline{b_5}$,

$MC_3^1 \Rightarrow \overline{b_1} \wedge \overline{b_3} \wedge \overline{b_4}$,

and

$MC_4^1 \Rightarrow \overline{b_1} \wedge \overline{b_3} \wedge \overline{b_5}$.

Let us, for instance, apply the Esary-Prochan method introduced in Section 20.7 to calculate the bounds. Hence, using the minimal paths and minimal cuts, we get $\rho_1^1=p_1p_2$, $\rho_2^1=p_4p_5$, $\rho_3^1=p_1p_3p_5$, $\rho_4^1=p_2p_3p_4$; $\gamma_1^1=(1-p_1)(1-p_4)$, $\gamma_2^1=(1-p_2)(1-p_5)$, $\gamma_3^1=(1-p_1)(1-p_3)(1-p_5)$, and $\gamma_4^1=(1-p_2)(1-p_3)(1-p_4)$. Therefore we obtain the upper and lower bounds for subsystem $S_1$:

$L_1 = (1-\gamma_1^1)(1-\gamma_2^1)(1-\gamma_3^1)(1-\gamma_4^1)$,

and

$U_1 = 1-(1-\rho_1^1)(1-\rho_2^1)(1-\rho_3^1)(1-\rho_4^1)$. For $p_1=p_2=p_3=p_4=p_5=0.9$, we have $L_1=0.98728$ and $U_1=0.99907$.

![img/2d1450f2a8b6.png](img/2d1450f2a8b6.png)
