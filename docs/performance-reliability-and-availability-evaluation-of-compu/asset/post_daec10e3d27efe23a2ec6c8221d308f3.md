
## 290 Performance, Reliability, and Availability Evaluation of Computational Systems

the spare server, and the transition $O_2$ firing events are activation of switching off the spare server. All transitions $O_2$ are exponentially distributed. $O_2$ is an immediate transition. All transitions have semantic meaning and have the same priority level. Transition $R_2$ has a guard expression: $\#S_D=0$; that is, $R_2$ may only fire if place $S_D$ is unmarked. This was adopted to give precedence to the main server ($S_1$) or its spare server ($S_2$) since only one repair facility is available. If this guard expression is not active, it is assumed that the number of repair facilities is equal to the number of servers. The arc connecting $S_U$ to transition $D$ is an inhibitor arc. This was adopted to represent the switching on when the main server ($S_1$) is down. When the spare server is available ($\#S_2S_U=1$), the main server is also available ($\#S_U=1$); it is worth noting the inhibitor between place $S_D$ and transition $O_2$ - the spare server is switched off. This is depicted by firing $O_2$. The initial marking shows that $S_1$ is operational ($\#S_U=1$) and $S_2$ is turned off ($\#S_2=0$). Operating system is depicted by its hardware, operating system, web-server, and database-server. If one of these components fails, the respective server ($S_1$ or $S_2$) becomes unavailable. The RBD in Figure 22.15.a may represent a sub-system. This RBD is a series of components, the reliability, is calculated by

```
$R_S(t) = \prod_{j\in(HW,OS,WS,DB)} e^{-\lambda_j t} = e^{-\sum_{j\in(HW,OS,WS,DB)}\lambda_j t}$
```

where $\lambda_S = \sum_{j\in(HW,OS,WS,DB)}\lambda_j$; hence $MTTF_S=1/\lambda_S$. These MTTFs are assigned to transitions $F_1$ and $F_2$.

The MTTF is defined by the repairing facility time or in a service agreement (SLA) are assigned to transitions $R_1$ and $R_2$. The mean time required to switch on (MTTSO starting all required pieces of software to make the service available, is assigned to transition $D$. The steady-state system availability is calculated through

```
$A = P(\{\#S_1U+\#S_2U > 0\}$
```

and the downtime of period $T$ is

```
$DT = (1 - P(\{\#S_1U+\#S_2U > 0\})) \times T$.
```

The reliability SPN of such a system is shown in Figure 22.15.c and is equivalent to the SPN of the single-component (see Figure 22.2) since once $S_1$ fails, the service steps are being delivered. The reliability may differ if a specified downtime is agreed upon between the partners. Therefore, the reliability at $t$ is calculated through transient analysis and the expression:

```
$R(t) = P{\{\S_1U\}(t)$
```

**Example 22.5.1.** Assume the system depicted in Figure 22.14. Consider the servers' $MTTF_{HW}=16000h, MTTF_{OS}=3000h, MTTF_{WS}=1800h$, and $MTTF_{DB}=$

## Modeling Availability, Reliability, and Capacity with SPN

![](img/2d1450514bb14a0cdf0eb5048614afab_307_0.png)

Figure 22.15 Cold-Standby System – Availability and Reliability Models.

1500h. As the $TTTF_j, j \in \{HW, OS, WS, DB\}$ are exponentially distributed, then

$MTTF_{S_i} = \frac{1}{MTTF_{HW}} + \frac{1}{MTTF_{OS}} + \frac{1}{MTTF_{DB}} = 618h.$

Consider the $MTTR_{S_i} = 20h,$ and $MTTSO_{S_i} = 0.0667h.$ The steady-state availability is

$A = P{\{#S1U + #S2U\ > 0\} = 0.998886.$

The yearly downtime in hours is

$DT = 9.76h.$

Figure 22.16.a and Figure 22.16.b, respectively, present the system availability (in number of nines) and the yearly downtime against $MTTSO \in (0.05h, 0.2h).$ The system reliability at $t = 500h$ is $R(500) = 0.4454068.$ Figure 22.17 shows the system reliability in the interval $t \in (0, 2000h).

## Performance, Reliability, Availability Evaluation of Computational Systems

![](img/2d1450514bb14a0cdf0eb5048614afab_308_0.png)

**Figure 22.16** Availability and Downtime × MTTSO.

![](img/2d1450514bb14a0cdf0eb5048614afab_308_1.png)

**Figure 22.17** $R(t) \times t$.

## 22.6 WARM STANDBY REDUNDANCY

This section presents SPN models for calculating the availability and reliability of systems configured in warm-standby redundancy. This system discussed in this section is similar to the one described in the previous section. The spare server ($S_2$), however, is not switched off. It is operational, but not fully operational; running its system, the web-server and database-server are not in execution (see Figure 22.18.a). As both $S_1$ and $S_2$, are executing their systems, both may fail. However, as $S_2$ has fewer components in execution, it is reasonable to assume its failure rate is lower than the failure rate of the primary server ($S_1$). It is worth mentioning that both servers (hardware, operating systems, etc.) are assumed to be equivalent.

## Modeling Availability, Reliability, and Capacity with SPN

![](img/2d1450514bb14a0cdf0eb5048614afab_309_0.png)

**Figure 22.18** Warm-Standby System.

If $S_1$ is processing the workload and $S_2$ fails, it is lost, since $S_2$ is not processing the transactions (see Figure 22.18.d). Hence, it may be repaired and return to standby mode. Nevertheless, while $S_1$ is processing the workload, so the web-server and database-server should be started (see Figure 22.18.b). This process takes a while, but the delay is shorter than the time required to start a cold-standby server depicted in the previous section (see Figure 22.18.c). The availability model depicted in Figure 22.15 is somewhat similar to the cold-standby model depicted by places $S_O$ and $S_D$, transitions $F_2$ and $R_2$, and their respective arcs. The other features are equal to the cold-standby model represented in Figure 22.15. The steady-state system availability is estimated through

```
$A = P(\#S1U = 1 \cup #S2U = 1) (22.6.1)
```

This expression is equivalent to

```
$A = P(\#S1U + #S2U > 0) (22.6.2)
```

which was presented in the previous example. The instantaneous availability is computed through $A(t) = P(\#S1U = 1 \cup #S2U = 1\}(t)$.

## Performance, Reliability, and Availability Evaluation of Computational Systems

![](img/2d1450514bb14a0cdf0eb5048614afab_310_0.png)

**Figure 22.19** Warm-Standby - Availability Model.

or by $A(t) = P(\{\#S1U + \#S2U > 0\}(t).

The downtime in a period $T$ may, then, be estimated through

$DT = (1 - P(\{\#S1U + \#S2U > 0\})) \times T$

or by

$DT = (1 - P(\{\#S1U = 1 \cup \#S2U = 1\})) \times T$.

The reliability model of the warm-standby configuration is the SPN adopted for calculating the reliability of the cold-standby configuration (see Figure 22.15.c). Therefore, the reliability at $t$ may be calculated through $R(t) = P{\{\#S1U = 1\}(t)$.

**Example 22.6.1.** The system depicted in Figure 22.18. Consider the servers' $MTTF_{HW}=16000h, MTTF_{OS}=3000h, MTTF_{WS}=1800h$, and $MTTF_{DB}=1500h, i \in \{1, 2\}$. As the $TTTF_j, j \in \{HW, OS, WS, DB\}$ are exponentially distributed, then the servers' mean time to failure when in active mode is

$MTTF_{S_i} = \frac{1}{MTTF_{HW_i}} + \frac{1}{MTTF_{OS_i}} + \frac{1}{MTTF_{WS_i}} + \frac{1}{MTTF_{DB_i}} = 618h$,

whereas the $S_2$ mean time to failure in standby mode is

$MTTF_{S_2,O} = \frac{1}{MTTF_{HW_2}} + \frac{1}{MTTF_{OS_2}} = 2526h$.

## Modeling Availability, Reliability, and Capacity with SPN

Consider the $MTTR_s = 20h,$ and $MTTS_s = 0.017h.$ The steady-state availability is

$A = P\{\#S1U + \#S2U\} > 0\} = 0.99872.$

The yearly downtime in hours is

$DT = 11.19h.$

It is worth noting that in this particular case, the availability is smaller than that obtained from the respective cold-standby redundancy. Likewise, the yearly downtime is higher. Figure 22.20 shows the availability and yearly downtime (in hours) for both the warm-standby and cold-standby (discussed in the previous section) against the $MTTR \in (4h, 20h)$. The warm-standby configuration provides higher availability (and shorter downtime) than the cold-standby configuration for $MTTRs$ shorter than $12h.$

![](img/2d1450514bb14a0cdf0eb5048614afab_311_0.png)

**Figure 22.20** Warm-Standby vs Cold-Standby $\times MTTR$- Availability (#9s) and Downtime.

## 22.7 ACTIVE-ACTIVE REDUNDANCY

Suppose we have the system shown in Figure 21.29. As described in Section 21.7, the servers share the workload processing. It means servers are active and processing transactions. The system is available if at least one server is processing. Nevertheless, if both servers are active, the processing capacity is higher than if only one server is operational. The basic SPN availability and reliability models are the same SPNs proposed to represent the hot-standby redundancy depicted in Figure 22.7.
