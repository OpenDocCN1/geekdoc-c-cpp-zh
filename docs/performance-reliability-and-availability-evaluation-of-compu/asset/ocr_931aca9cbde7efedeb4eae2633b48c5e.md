# 194 Performance, Reliability, and Availability Evaluation of Computational Systems

$P(MC_4) = q_{m_1}q_{m_2}q_{m_3},$

$P(MC_1 \cap MC_2) = q_{p_1}q_{p_2}q_{m_2}q_{m_3},$

$P(MC_1 \cap MC_3) = q_{p_1}q_{p_2}q_{m_1}q_{m_3},$

$P(MC_1 \cap MC_4) = q_{p_1}q_{p_2}q_{m_1}q_{m_2}q_{m_3},$

$P(MC_2 \cap MC_3) = q_{p_1}q_{p_2}q_{m_1}q_{m_2}q_{m_3},$

$P(MC_2 \cap MC_4) = q_{p_1}q_{p_2}q_{m_1}q_{m_2}q_{m_3},$

$P(MC_3 \cap MC_4) = q_{p_2}q_{m_1}q_{m_2}q_{m_3},$

$P(MC_1 \cap MC_2 \cap MC_3) = q_{p_1}q_{p_2}q_{m_1}q_{m_2}q_{m_3},$

$P(MC_1 \cap MC_2 \cap MC_4) = q_{p_1}q_{p_2}q_{m_1}q_{m_2}q_{m_3},$

$P(MC_1 \cap MC_3 \cap MC_4) = q_{p_1}q_{p_2}q_{m_1}q_{m_2}q_{m_3},$

$P(MC_2 \cap MC_3 \cap MC_4) = q_{p_1}q_{p_2}q_{m_1}q_{m_2}q_{m_3},$

and

$P(MC_1 \cap MC_2 \cap MC_3 \cap MC_4) = q_{p_1}q_{p_2}q_{m_1}q_{m_2}q_{m_3},$

Assume the MTTF and the MTTR of each component is specified in Table 19.3. Consider $q_i = MTTR/(MTTF+MTTR)$; then the failure probability of each term is calculated. The respective values are presented in Table 20.11.

Therefore, the failure probability (unavailability) is $P(\cup_{i=1}^4 MC_i) = 8.72407 	imes 10^{-5}$. Hence, as $A = 1 - P(\cup_{i=1}^4 MC_i) = 0.999913^5$.

> $5$ Also see the result shown in Example 19.3.3.