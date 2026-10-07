
ods output Test-boundaryinfo3; run;

In the first part Example Code 2.12 Conditional and Predictive Power for the Psoriasis Trial, proc seqdesign is updated to remove utility monitoring using stop=reject only. This allows the rejection boundary not be affected by a decision on the utility assessed based on conditional or predictive power. condpower (cref=0.5,1.25) generates the conditional powers for rejecting the null at all future stages (default) under different hypothetical references: cref=0.5, 1, 1.25 times the original reference. The partial output is given in Figure 2.17 Output for Example Code 2.12. A conditional power plot is requested using plotscondpower (Figure 2.18 Conditional Power Plot for the Psoriasis Trial Based on Observed Data). As for the predictive power of the final stage, predpower is used and since only predictive power for the final stage is calculated, no plot for predictive power is generated.

## Figure 2.17 Output for Example Code 2.12

| Stopping Stage | Reference Ref= CRef* (All Reference) | Conditional Power |
| :--- | :--- | :--- |
| MLE | MLE | CRef |
| 1 | 0.37879 | MLE | 1.1478 | 0.96019 |
| 1 | 0.37879 | | 0.5000 | 0.45577 |
| 1 | 0.37879 | Alternative | 1.0000 | 0.90756 |
| 1 | 0.37879 | | 1.2500 | 0.97980 |

| Predictive Power Information | |
| Stopping Stage | MLE | Predictive Power |
| :--- | :--- | :--- |
| | 0.37879 | 0.75409 |

| Test Information (MLE Scale) Null Reference = 0 | |
| Information Level | Alternative Boundary Values | Test |
| _Stage_ | Proportion | Actual | Upper | Alpha | Action |
| 1 | 0.1833 | 18.5617 | 0.3300 | 0.57459 | 0.37879 Continue |
| 2 | 0.3774 | 38.1953 | 0.3300 | 0.39657 | 0.46052 Reject Null |
| 3 | 0.7600 | 75.8511 | 0.3300 | 0.26119 | |
| 4 | 1.0000 | 101.1347 | 0.3300 | 0.23326 | |

| Parameter Estimating Stagewise Ordering | | |
| Stopping Stage | MLE p-value H0:Param=6 Median Estimate Lower 95% CL |
| trt | 0.048519 | 0.0075 | 0.464397 | 0.16385 |

## Figure 2.18 Conditional Power Plot for the Psoriasis Trial Based on Observed Stage 1 Data

## Conditional Power Plot

![](img/f4ec2665c3484c528370923aeb5cb99f_131_0.png)

The conditional power of 96.02% refers to the hypothetical reference when it is the observed MLE. Since the MLE in the first stage is 0.3788, slightly larger than the original reference of 0.4-0.07=0.33, therefore the calculated $c = 0.3788/0.33 = 1.1478$. If the hypothetical reference is $1.25^*=0.33 = 0.4125$, the conditional power is 97.98%. These estimated conditional powers suggest strong evidence of continuing the trial to the next stage. The predictive power of 75.41%, although smaller than the conditional powers, still implies strong evidence to continue. The next table is the same as before, displaying the rejection of the null hypothesis at the second stage and therefore, neither conditional nor predictive power needs to be calculated.

Another important issue that arises from sequential testing is the provision of unbiased estimation of the effect size of an experimental drug. For a fixed-sample design without interim analyses for early termination, it is possible to achieve unbiased quantitative evaluation of treatment difference. However, under sequential design, the usual maximum likelihood estimator for the mean produces over-estimation because of the choice of stopping rules and therefore the sampling distribution of the test statistic is no longer the same as the one from fixed-sample design. Jennison and Turnbull [11] gave a brief exposition of this issue. Methods have been proposed to adjust for this bias and this topic is beyond the scope of this chapter. However, as for median, an unbiased median estimator can be available in SAS. The last table of the output displays the unbiased median estimator of 0.4548 based on default stag ordering. The corresponding p-value of the trial is 0.0075 based on the data collected at the end of the second stage.

Occasionally, some clinical trials will include multiple groups such as multiple doses of an investigational drug. In this case, futility analysis plays an important role to drop doses that do not exhibit clear evidence of efficacy, however, since multiple comparisons are being conducted, measures to control the inflation of type I error must be in place to account for multiplicity. In fact, dropping doses cannot be addressed in a classical group-sequential framework and requires completely different methodology, similar to the one described in Chapter 3, “Sample Size Re-estimation.” The latter extends the distributional theory and methods of preserving type 1 error that we have reviewed to situations when a trial's total maximum information can be adjusted.

## 2.6 Summary

Over the last couple of decades, the theories of group sequential have been well-established, particularly in the context of trials. The US Food and Drug Administration (FDA) released a draft guidance for industry in 2010, stating that adaptive designs are well-understood. This chapter has provided a solid introduction to group sequential methods and monitoring during trial.

## References

- 1. Everitt BS & Palmer CR. (2011). Encyclopaedic Companion to Medical Statistics.
- 2. Armitage P. (1960). Sequential Trials, First Edition. West Sussex: Oxford.
- 3. Armitage P, Pike MC, Rowe J. (1971). Design and analysis of randomized clinical trials. Journal of American Medical, 34: 793-797.
- 4. Kittelson J & Emerson SS. (1999). Discrete sequential boundaries. Biometrics, 55 (3): 874-882.
- 5. Pocock L & Fleming TR. (1979). Group sequential boundaries for clinical trials. Biometrika, 70 (3): 659-663.
- 6. Haybittle S, Cox NE, Armitage P, Breslow J, Mantel N, Peto K, Smith PG. (1976). Repeated assessment of results in cancer. British Journal of Cancer, 34: 585-61.
- 7. Jennison C & Turnbull BW. (2000). Group Sequential Methods with Applications to Clinical Trials. Boca Raton, FL: Chapman & Hall.
- 8. Todd S. (2007). A 25-year review of sequential methodology. Statistics in Medicine, 26: 237-252.
- 9. Whitehead, J., Lan K & DeM. (1983). Multiple testing. Journal of the Royal Statistical, 132: 331-337.
- 10. Wiegman A, Hutten BA, de Groot E, Rodenburg J, Büller HR, Kastelein JJ. (2004). Efficacy and safety of statin therapy in children with familialcholesterolemia. Journal of American Medical, 292 (3): 331-337.
- 11. Jennison C & Turnbull BW. (2011). (Duplicate entry in text)
- 17. U.S. Food and Drug Administration. (2008). Guidance to Industry: Diabetes Mellitus - Evaluating Cardiovascular Risk in New Antidiabetic Therapies to Treat Type 2 Dia- betes. Rockville, MD: US FDA.
