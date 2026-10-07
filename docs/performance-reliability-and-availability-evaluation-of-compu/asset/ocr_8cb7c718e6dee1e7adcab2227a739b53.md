# Modeling Availability, Reliability, and Capacity with SPN

![](bbox=[0.143, 0.126, 0.876, 0.326])

Figure 22.10 Hot-Standby with Imperfect Coverage - Availability (a) and Reliability (b) Models.

the firing of transition $R$. If, on the other hand, when marking $M_1$, $UC$ fires, the server failure is not detected by the system and becomes hidden. The hidden failure may be detected later on, after a detection time $(DT)$ represented in transition $D$, and then be repaired, or the second server may fail before the detection of the first server failure. In such a case, the service becomes unavailable. Observe that the $UC$ becomes disabled ($G(\COK > 0) \rightarrow F$) once a server is in failure because a second server failure is detected since the service is no longer provided. In this example, the time to fail, repair, and detection time are exponentially distributed with rates of $\lambda$, $\mu$, and $eta$, respectively. Hence, $MTTF = 1/\lambda$, $MTTR = 1/\mu$, and $MDT = 1/eta$ (mean detection time).

The instantaneous system availability may be calculated through

$A = P(\{\#COK > 0\}(t).

The steady-state system availability may be calculated through

$A = P(\{\#COK > 0\).

The steady-state availability expressed in the number of nines may be calculated through

#9s = -\log_{10}P(\{\#COK = 0\).

The probability of having a hidden failure is

$PHF = P(\{\#COK > 0)AND(\#HF = 0\).