# Table 22.5

$A = P\{Koo20} \geq K\} \times K \in \{10, 11, 12, \dots, 20\}$

| K | P(Koo20") |
|---|---|
| 10 | 0.999865 |
| 11 | 0.999864 |
| 12 | 0.99986 |
| 13 | 0.994462 |
| 14 | 0.994453 |
| 15 | 0.994439 |
| 16 | 0.994325 |
| 17 | 0.885118 |
| 18 | 0.885027 |

composed of two places, $UP$ and $DW$, two transitions, $F_s$ and $R_s$, and their arcs. The server semantics of both transitions is $iss$ since it is assumed that the number of-pair facilities is equal to the number of failed servers. The number of tokens in place $UP$ represents the number of servers available, whereas the number of tokens in $DW$ denotes the number of servers in failure. $PiSA$ is obtained through the expression

> $PiSA = P\{#UP = i\}$; (22.8.1)

which denotes the probability of having $i$ servers available in steady-state. Figure 22.26.b presets a lower-level model. This model is represented by two places, $UP_v$ and $DW_v$, two transitions, $F$ and $R_$, and their arcs. The server semantics of both transitions is $iss$ since it is assumed that the server may restart its virtual machines concurrently. The number of tokens in place $UP_v$ represents the number of virtual machines available, whereas the number of tokens in $DW_v$ denotes the number of virtual machines in failure. This SPN allows computing the probability of having $j$ virtual machines alive, for a given number of servers, $j \in \{0, 1, 2, \dots, M_i\}$, where $M_i$ is the maximum number of virtual machines for a given number of servers $i$.

The SPN shown in Figure 22.26.a generates the CTMC depicted in Figure 21.45.a, whereas the SPN presented in Figure 22.26.b produces the other CTMCs of the Figure 21.45. The probability of having $j$ virtual machines alive, considering $i$ servers are operational, is obtained through

> $PJVMAi = P\{#UP_c = j\ \times P\{#UP = i\}$; (22.8.2)