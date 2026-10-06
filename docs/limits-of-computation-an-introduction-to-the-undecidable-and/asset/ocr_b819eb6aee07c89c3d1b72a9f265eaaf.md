# 94 Limits of Computation

| | B | B | 0 | 1 | 1 | 0 | B | B | . |
|---|---|---|---|---|---|---|---|---||
| | | | | | | | Working tape (begins as copy of input tape) |
| | B | B | 0 | 1 | 1 | 0 | B | B | . |
| | B | B | 3 | 1 | 3 | 2 | B | B | . |

Input tape (never changes)

Path tape (which chooses to make) --but this path is not possible; rejects

| State | Read | New State | Write | Move | Paths in Order: |
|---|---|---|---|---||
| 1st | $q_0$ | $q_0$ | R | 1 |
| 2nd | $q_0$ | $q_1$ | R | 2 (no such move) |
| 3rd | $q_0$ | $q_{reject}$ | R | 3 (no such move) |
| 1st | $q_0$ | $q_0$ | R | 11 (still in $q_0$) |
| 1st | $q_1$ | $q_{reject}$ | R | 12 (now in $q_1$) |
| 1st | $q_1$ | $q_{accept}$ | R | 13 (now in $q_{reject}$) |
| Table for $\delta$ function | | | | |

FIGURE 5.9 Emulating NDTM of Figure 5.8 using three tapes.

![](bbox=[0.147, 0.513, 0.852, 0.787])

| State | Read | New State | Write | Move |
|---|---|---|---|---||
| 1st | $q_0$ | $q_0$ | 1 | R |
| 2nd | $q_0$ | $q_1$ | 1 | R |
| 3rd | $q_0$ | $q_{reject}$ | 1 | R |
| 1st | $q_0$ | $q_0$ | 0 | R |
| 1st | $q_1$ | $q_{reject}$ | 0 | R |
| 1st | $q_1$ | $q_{accept}$ | 1 | R |
| Table for $\delta$ function |

FIGURE 5.10 Emulating NDTM of Figure 5.8.