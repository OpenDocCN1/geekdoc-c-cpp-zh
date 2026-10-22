# Time versus error

![](bbox=[0.15, 0.14, 0.8, 0.45])

Figure 1.22 Time (in seconds) versus per cent RMNSE when 6 p233 and 22 c366 are used.

| t(s) | e (RMNSE %) | Runs |
|---|---|---|
| 0.3 | 3.43025 | 126 |
| 0.4 | 3.41711 | 92 |
| 0.5 | 3.40668 | 55 |
| 0.75 | 3.38288 | 83 |
| 1.0 | 3.34983 | 199 |
| 1.5 | 3.30783 | 360 |
| 2.0 | 3.28336 | 524 |
| 4.0 | 3.19867 | 758 |

Table 1.12 Average error and number of runs required versus simulation time when all PEs are used

from 1 to 40.54.

Let us run PARGEFREX using p p233 and c c366. Let us suppose the use of CT termination error with the simulation time fixed to t'_{p,c}. Let us indicate with e_{p,c} the average per cent error (RMNSE) obtained in the same way as above: at least 50 runs and as many runs as needed to reach an average error with a confidence level of 0.01 once the best 20% and the worst 20% of runs are discarded. Let us introduce the quantity S_{p,c} as follows: