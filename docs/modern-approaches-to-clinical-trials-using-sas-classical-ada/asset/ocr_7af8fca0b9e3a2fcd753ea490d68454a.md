# 4.2.3 Input Historical Data

Suppose that the historical data are available for the control and experimental arms from $K_0$ previous studies, where $K_0 \ge 1$. For the historical data, we define

```
$x_{0k} = \begin{cases} x_{01k}, & & x_{01k} = x_{02k} \ (x_{01k}, x_{02k}), & x_{01k} < x_{02k} \end{cases}$
```

where $x_{0jk} = 0$ for control or 1 for experimental for $j=1,2$ and $x_{01k} \le x_{02k}$. If $x_{0k}$ for $k=1,...,K_0$, then the historical data are available only for the control arm, if $x_{0k}$ is the vector $(x_{01k}, x_{02k})$, for all $k=1,...,K_0$, then the historical data are available for both arms. For example, if $x_{0k}=0$ for $k=1,...,K_0$, this indicates that the historical data are available only for the control arm. If $x_{0k}$ is the vector $\{0,1\}$. Under this setting, we let $y_{0k} = \{y_{0jk}:x_{0jk} \le j-1 \le x_{02k}\}$ denote the total subject year duration and denote $n_{0k} = \{n_{0jk}:n_{0jk} \le j-1 \le x_{02k}\}$ to be the total number of events for $k=1,...,K_0$. Suppose that the trial-level aggregate data $D_0 = \{y_{0k}, n_{0k}, k=1,...,K_0\}$ are available for the historical studies. Types of Single-Arm Historical Data and Types of Multi-Arm Historical Data show the four types of historical data $D_0$.

| TID | Type I (Control arm only) | | | $y_{0k}$ | $n_{0k}$ | $x_{0k}$ | Type II (Experimental arm only) | | | $y_{0k}$ | $n_{0k}$ | $x_{0k}$ |
|---|---|---|---|---|---|---||
| 1 | $y_{011}$ | $n_{011}$ | 0 | $y_{021}$ | $n_{021}$ | 1 |
| 2 | $y_{012}$ | $n_{012}$ | 0 | $y_{022}$ | $n_{022}$ | 1 |
| ... | ... | ... | ... | ... | ... | ... |
| $K_0$ | $y_{01K_0}$ | $n_{01K_0}$ | $K_0$ | $y_{02K_0}$ | $n_{02K_0}$ | 1 |

Table 4.2 Types of Single-Arm Historical Data

| Type III (Both arms) | | | | Type IV (Both arms mixed) | | | |
|---|---|---|---|---|---|---||
| TID | $y_{0k}$ | $n_{0k}$ | $x_{0k}$ | $y_{0k}$ | $n_{0k}$ | $x_{0k}$ |

Table 4.3 Types of Multi-Arm Historical Data