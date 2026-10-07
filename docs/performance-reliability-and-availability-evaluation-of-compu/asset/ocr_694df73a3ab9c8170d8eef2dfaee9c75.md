# Performance, Reliability, and Availability Evaluation of Computational Systems

![](bbox=[0.277, 0.103, 0.722, 0.345])

Figure 22.19 Warm-Standby - Availability Model.

or by

$A(t) = P(\{#S1U + \#S2U\} > 0\}(t).

The downtime in a period T may, then, be estimated through

$DT = 1 - (P(\{#S1U + \#S2U\} > 0)) \times T$

or by

$DT = 1 - (P(\{#S1U = 1\}OR(\#S2U = 1\})) \times T$.

The reliability model of the warm-standby configuration is the SPN adopted for calculating the reliability of the cold-standby configuration (see Figure 22.15.c). Therefore, the reliability at t may be calculated through

$R(t) = P{\#S1U\}(t).

**Example 22.6.1.** The system depicted in Figure 22.18. Consider the servers' $MTTF_{HW} = 16000h$, $MTTF_{OS} = 3000h$, $MTTF_{WS} = 1800h$, and $MTTF_{DB} = 1500h, i \in \{1, 2\}$. As the $TTTF_j, j \in \{HW, OS, WS, DB\}$ are exponentially distributed, then the servers' mean time to failure when in active mode is

$MTTF_{S_i} = \frac{1}{MTTF_{HW_i}} + \frac{1}{MTTF_{OS_i}} + \frac{1}{MTTF_{WS_i}} + \frac{1}{MTTF_{DB_i}} = 618h$,

whereas the S2 mean time to failure when in standby mode is

$MTTF_{S_2,O} = \frac{1}{MTTF_{HW_2}} + \frac{1}{MTTF_{OS_2}} = 2526h$.