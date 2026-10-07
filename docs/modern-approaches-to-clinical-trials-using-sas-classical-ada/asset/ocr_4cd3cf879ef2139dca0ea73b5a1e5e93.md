# The SEGESIGN Procedure
Design: stage 1power

| Design Information | |
|---|---|
| Statistical Distribution | Normal |
| Boundary Scale | MLE |
| Alternative Hypothesis | Two-Sided |
| Early Stop | Reject Null |
| Method | Error Spending |
| Boundary Key | Both |
| Alternative Reference | 0.587787 |
| Number of Stages | 3 |
| Alpha | 0.05 |
| Beta | 0.1 |
| Power | 0.9 |
| Max Information (Percent of Fixed Sample) | 102.4384 |
| Max Information | 31.15446 |
| Null RefASN (Percent of Fixed Sample) | 101.7382 |
| Alt RefASN (Percent of Fixed Sample) | 75.98825 |

| Expected Cumulative Spending Probabilities |
| Reference = CRef * (Alt Reference) | Stopping Probabilities |
| CRef | Stopping Stage | Source | Stage_1 | Stage_2 | Stage_3 |
|---|---|---|---|---|--|
| 0.0000 | 2.973 | Null | 0.00625 | 0.02109 | 0.05000 |
| 0.5000 | 2.759 | Null | 0.05774 | 0.18281 | 0.36479 |
| 1.0000 | 1.987 | Null | 0.23938 | 0.59357 | 0.90000 |
| 1.5000 | 1.265 | Null | 0.77200 | 0.97285 | 0.99882 |

| Boundary Information (MLE Scale) |
| Null Reference = 0 |
| Information Level | Alternative | Boundary Values |
| Stage_ | Proportion | Actual | Events | Lower | Upper | Alpha | Alpha |
|---|---|---|---|---|---|---|--|
| 1 | 0.5000 | 15.57723 | 82.30892 | -0.58779 | -0.69281 | 0.69281 | |
| 2 | 0.7500 | 23.36585 | 93.48539 | -0.58779 | -0.48757 | 0.48757 | |
| 3 | 1.0000 | 31.15446 | 124.6178 | -0.58779 | -0.38343 | 0.38343 | |

| Error Spending Information |
| Information Level | Cumulative Error Spending |
| Lower | Upper |
| Stage_ | Proportion | Alpha | Beta | Beta | Alpha |
|---|---|---|---|---|--|
| 1 | 0.5000 | 0.00313 | 0.00000 | 0.00000 | 0.00313 |
| 2 | 0.7500 | 0.01065 | 0.00000 | 0.00000 | 0.01065 |
| 3 | 1.0000 | 0.02500 | 0.01000 | 0.01000 | 0.02500 |

| Numbers of Events (D) |
| Two-Sample Log-Rank Test |
| Stage_ | D | Information |
|---|---|--|
| 1 | 82.31 | 15.5772 |
| 2 | 93.46 | 23.3658 |
| 3 | 124.62 | 31.1545 |

From the partial output in Figure 2.15 Output for Stage 1 of Example Code 2.11, we can determine that the maximum number of events for the trial has increased to 125, a relatively minor increase for the added