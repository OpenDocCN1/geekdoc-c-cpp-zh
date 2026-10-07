ods output Test-boundaryinfo3; run;

In the first part Example Code 2.12 Conditional and Predictive Power for the Psoriasis Trial, proc seqdesign is updated to remove utility monitoring using stop=reject only. This allows the rejection boundary not be affected by a decision on the utility assessed based on conditional or predictive power. condpower (cref=0.5,1.25) generates the conditional powers for rejecting the null at all future stages (default) under different hypothetical references: cref=0.5, 1,1.25 times the original reference. The partial output is given in Figure 2.17 Output for Example Code 2.12. A conditional power plot is requested using plotscondpower (Figure 2.18 Conditional Power Plot for the Psoriasis Trial Based on Observed Data). As for the predictive power of the final stage, predpower is used and since only predictive power for the final stage is calculated, no plot for predictive power is generated.

# Figure 2.17 Output for Example Code 2.12

| Stopping Stage | Reference Ref= CRef* (All Reference) | Conditional Power |
| MLE | MLE | CRef | |
|---|---|---||
| 1 | 0.37879 | MLE | 1.1478 | 0.96019 |
| 1 | 0.37879 | | 0.5000 | 0.45577 |
| 1 | 0.37879 | Alternative | 1.0000 | 0.90756 |
| 1 | 0.37879 | | 1.2500 | 0.97980 |

| Predictive Power Information |
| Stopping Stage | MLE | Predictive Power |
|---|---||
| | 0.37879 | 0.75409 |

| Test Information (MLE Scale) Null Reference = 0 |
| Information Level | Alternative Boundary Values | Test |
| _Stage_ | Proportion | Actual | Upper | Alpha | Action |
|---|---|---|---|---||
| 1 | 0.1833 | 18.5617 | 0.3300 | 0.57459 | 0.37879 Continue |
| 2 | 0.3774 | 38.1953 | 0.3300 | 0.39657 | 0.46052 Reject Null |
| 3 | 0.7600 | 75.8511 | 0.3300 | 0.26119 | |
| 4 | 1.0000 | 101.1347 | 0.3300 | 0.23326 | |

| Parameter Estimating Stagewise Ordering |
| Stopping Stage | MLE p-value H0:Param=6 Median Estimate Lower 95% CL |
|---|---|---|---|---||
| trt | 0.048519 | 0.0075 | 0.464397 | 0.16385 |

131

*