284 Performance, Reliability, and Availability Evaluation of Computational Systems

![](bbox=[0.158, 0.098, 0.821, 0.363])

**Figure 22.9 Hot-Standby Configuration – $R(t) 	imes t$.**

# 22.4 IMPERFECT COVERAGE

Consider the system depicted in Figure 22.7.a. Now, however, assume the failure coverage is imperfect; that is, the system is configured in hot-standby, and one server may fail, and this failure may not be detected (a hidden failure). Such a failure may be later detected, or the second server available may also fail, and the service becomes unavailable. This aspect was already discussed in Section 21.4, and a CTMC model presented.

This section provides an availability and reliability models specified in SPN (see Figure 22.10). The availability model is shown in Figure 22.10a. It is composed of sets of places $P = \{COK, CF, CF, HF\}$, a set of transitions $T = \{F, R, C, U, D\}$, and their arcs (see $G(UC) := \#COK > 0 ightarrow \{T, F\}$). The server semantics of $F$ and $R$ are $iss$ and $sss$, respectively since only repair facility is considered in this. The weights assigned to $C$ and $UC$ are $1-c$, respectively. Their priorities are equal to 1. The initial marking states that both servers are available, that is $M_0 = (m_{COK}, m_{CF}, m_{CF}, m_{HF}) = (2,0,0,0)$.

As servers available, the only possible event is a server failure. It is worth mentioning that the server semantics of $F$ is $iss$. One server failure is depicted by firing $F$, removing one token from $COK$, and storing one token in $CF$. The new marking is $M_1 = (1,1,0,0)$, which is a vanishing marking. In this marking, $C$ fires with probability $c$ and $UC$ fires with probability $1-c$. If $C$ fires, one token is removed from $CF$, and one token is stored in $CFS$. In this new marking, the system is aware of the server failure and demands its repair. The repair is represented by