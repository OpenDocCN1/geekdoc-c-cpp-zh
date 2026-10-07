# PERFORMING A TWO-SAMPLE T-TEST 277

| | |
|---||
| A | 20.00 |
| A | 23.00 |
| A | 32.00 |
| A | 24.00 |
| A | 25.00 |
| A | 28.00 |
| A | 27.50 |
| A | 25.00 |
| B | 46.00 |
| B | 56.00 |
| B | 45.00 |
| B | 46.00 |
| B | 51.00 |
| B | 34.00 |
| B | 47.50 |

```
; PROC TTEST;
CLASS BRAND;
VAR HEIGHT;
Title 'Independent Group t-Test Example';
RUN;
```

+   2. Run this program and observe the output for PROC TTEST, given in Table 11.4.

# TABLE 11.4 Two-Sample t-Test Output from PROC TTEST

| BRAND | N | Mean | Std Dev | Std Err | Minimum | Maximum |
|---|---|---|---|---|---|--|
| A | 7 | 25.6429 | 3.9021 | 1.4748 | 20.0000 | 32.0000 |
| B | 8 | 43.8125 | 9.8196 | 3.4717 | 25.0000 | 56.0000 |
| Diff (1-2) | | -18.1696 | 7.6778 | 3.9736 | | |

| Method | Mean | 95% CL Mean | Std Dev | 95% CL | Std Dev |
|---|---|---|---|---|---|--|
| A | | 25.6429 | 22.0340 | 29.2517 | 2.5145 | 8.5926 |
| B | | 43.8125 | 35.6031 | 52.0219 | 9.8196 | 6.4925 | 19.9865 |
| Diff (1-2) Pooled | -18.1696 | -26.7541 | -9.5882 | 7.6778 | 5.5660 | 12.3692 |
| Diff (1-2) Satterthwaite | -18.1696 | -26.6479 | -9.6914 | | |

| Method | Variances | DF | Value | Pr > [t] |
|---|---|---|---|--|
| Pooled Equal | 13 | -4.57 | 0.0005 |
| Satterthwaite Unequal | 9.3974 | -4.82 | 0.0008 |

Equality of Variances

| Method | Num DF | Den DF | F Value | Pr > F |
|---|---|---|---|--|
| Folded F | 7 | 6 | 6.33 | 0.0388 |

(continued)