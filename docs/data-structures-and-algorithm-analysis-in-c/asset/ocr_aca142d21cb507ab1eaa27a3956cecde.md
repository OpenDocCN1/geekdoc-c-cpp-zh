| v | known | dv | pv |
|---|---|---|---|
| v1 | T | 0 | 0 |
| v2 | F | 2 | v1 |
| v3 | F | 2 | v4 |
| v4 | T | 1 | v1 |
| v5 | F | 7 | v4 |
| v6 | F | 8 | v4 |
| v7 | F | 4 | v4 |

Figure 9.54 The table after v4 is declared known

selected is v4. Every vertex is adjacent to v4. v1 is not examined, because it is known. v2 is unchanged, because it has dv = 2 and the edge cost from v4 to v2 is 3; all the rest are updated. Figure 9.54 shows the resulting table. The next vertex chosen is v2 (arbitrarily breaking a tie). This does not affect any distances. Then v3 is chosen, which affects the distance in v6, producing Figure 9.55. Figure 9.56 results from the selection of v7, which forces v6 and v5 to be adjusted. v6 and then v5 are selected, completing the algorithm.

| v | known | dv | pv |
|---|---|---|---|
| v1 | T | 0 | 0 |
| v2 | T | 2 | v1 |
| v3 | T | 2 | v4 |
| v4 | T | 1 | v1 |
| v5 | F | 7 | v4 |
| v6 | F | 5 | v3 |
| v7 | F | 4 | v4 |

Figure 9.55 The table after v2 and then v3 are declared known

| v | known | dv | pv |
|---|---|---|---|
| v1 | T | 0 | 0 |
| v2 | T | 2 | v1 |
| v3 | T | 2 | v4 |
| v4 | T | 1 | v1 |
| v5 | F | 6 | v7 |
| v6 | F | 1 | v7 |
| v7 | T | 4 | v4 |

Figure 9.56 The table after v7 is declared known