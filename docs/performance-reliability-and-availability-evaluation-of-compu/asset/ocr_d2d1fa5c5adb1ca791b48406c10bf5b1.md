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