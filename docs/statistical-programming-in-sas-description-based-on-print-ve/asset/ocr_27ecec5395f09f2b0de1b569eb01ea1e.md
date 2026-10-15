Output Added:
-------------
Name:      ConfLimits
Label:     Confidence Limits
Template:  Stat.TTest.ConfLimits
Path:      Ttest.ByGroup1.Y.ConfLimits
-------------

| group | Method | Mean | 95% CL Mean | Std Dev | 95% CL Std Dev |
|---|---|---|---|---|---|
| 1 |  | -0.2653 | -1.3092 | 0.7786 | 1.4593 | 1.0038 | 2.6641 |
| 2 |  | 0.4281 | -0.1818 | 1.0380 | 0.8525 | 0.5864 | 1.5564 |
| Diff (1-2) | Pooled | -0.6934 | -1.8162 | 0.4294 | 1.1951 | 0.9030 | 1.7673 |
| Diff (1-2) | Satterthwaite | -0.6934 | -1.8360 | 0.4492 |  |  |  |

Output Added:
-------------
Name:      TTests
Label:     T-Tests
Template:  Stat.TTest.TTests
Path:      Ttest.ByGroup1.Y.TTests
-------------

| Method | Variances | DF | t Value | Pr > |t| |
|---|---|---|---|---|
| Pooled | Equal | 18 | -1.30 | 0.2109 |
| Satterthwaite | Unequal | 14.503 | -1.30 | 0.2148 |

Output Added:
-------------
Name:      Equality
Label:     Equality of Variances
Template:  Stat.TTest.Equality
Path:      Ttest.ByGroup1.Y.Equality
-------------

| Equality of Variances |
|---|---|---|---|---|
| Method | Num DF | Den DF | F Value | Pr > F |
| Folded F | 9 | 9 | 2.93 | 0.1251 |