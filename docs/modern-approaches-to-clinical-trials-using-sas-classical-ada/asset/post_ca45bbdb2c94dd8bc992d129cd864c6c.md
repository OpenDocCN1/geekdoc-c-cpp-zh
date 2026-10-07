
## 2.4.2 P-value or Haybittle-Peto Boundaries

The P-value or Haybittle-Peto boundaries are used for early rejection of the null hypothesis. It was first proposed by Haybittle [7]. These boundaries are calculated by pre-specifying a fixed rejection boundary value for the p-value or the z-statistic for the first $j-1$ stages. For example, we can specify a small p-value $p_1$ for the first $j-1$ as a stopping criterion. If the first observed p-value in the sequence of the first $j-1$ p-values appears to be smaller than $p_1$, then the trial will be stopped to declare rejection of the null hypothesis. Otherwise, the trial will go to the final stage (i.e. $j$th stage) and a final p-value, $p_2$ is computed in such a way that the overall type I error is controlled at the $\alpha$ level. If we denote the $p$th quantile of the standard normal distribution as $z_p$, then we know $1-\Phi(z_p)=p$. In the one-sided setting, the trial will be stopped at the $j$th interim stage if $Z(t_j) \ge z_{p1}$ or if $(l_j) \ge \sqrt{t_{ij}}p_1$. Otherwise, the trial will be successful at the final stage only if $Z(l_j) \ge z_{p2}$ or if $(l_j) \ge \sqrt{t_{ij}}p_2$. Given the pre-specified $p_1$, the value of $p_2$ needs to preserve the type I error and it can be obtained by solving the following equation:

$$1-P_{\eta=0}(S(l_1) < \sqrt{t_{1j}}p_1 \dots S(l_{j-1}) < \sqrt{t_{(j-1)j}}p_1. S(l_j) < \sqrt{t_{ij}}p_2) = \alpha$$

where $P_{\eta=0}()$ represents the probability evaluated under the null joint distribution, that is, the distribution when $\eta=0$. The solution of $p_2$ can be obtained using a numerical method for recursive integration. Once the value of $p_2$ is determined, the maximum information $l_j$ needed is obtained by invoking the same numerical method to solve for the drift parameter $\eta_1$ in the following equation under the specified target power of $1-\beta:$

$$P_{\eta=\eta_1}(S(l_1) < \sqrt{t_{1j}}p_1 \dots S(l_{j-1}) < \sqrt{t_{(j-1)j}}p_1. S(l_j) < \sqrt{t_{ij}}p_2) = \beta$$

Using this value of drift parameter $\eta_1$, evaluated under alternative hypothesis, we can evaluate $l_j$ using

$$l_j = \left[ \frac{\eta_1}{\theta_1-\theta_0} \right]^2$$

In turn, we can estimate the needed maximum sample size $n_J$ if we are using the normal or binomial endpoint, or the maximum number of events $D(c_J)$. In the two-sided hypothesis testing, there are upper and lower rejection boundary values, thus we can simply replace $S(t)$ in the above equations with its absolute value $|S(t)|$. It can be noted that this p-value method can be generalized to unequal p-values instead of constant $p_1$ at each of the first $J-1$ stages.

## Example: Redesigning the Familial Hypercholesterolemia Trial Using Haybittle-Peto Method

In SAS, the procedure we use to derive the operating characteristics of group sequential design is proc seqdesign and the procedure used to monitor sequential trial is proctest. We will illustrate their applications using the examples discussed in 2.2 Examples of Classical Fixed-Sample Designs. Here, we show a simple use of proc seqdesign to generate a Haybittle-Peto design as a modified design for the pediatric trial.

### Example 2.5 Haybittle-Peto Design for Familial Hypercholesterolemia Trial

```sas
proc seqdesign altref=0.02 errsend stopprob;
hpdsdesignforn: design stages=5 method=peto(z=3) alt=upper-reject
alpha=0.025 beta=0.1;
samplesize model=twomeanample (stddev=0.045);
```

Example Code 2.5 Haybittle-Peto Design for Familial Hypercholesterolemia Trial generates a 5-stage design with a user-created label of hpdsdesignforn. In the design statement, we specify the use of the Haybittle-Peto method on the scale of the $Z$-statistic using method=peto(z=3) to set the boundary constant at 3 for the first four stages. This is the default. Alternatively, for the example discussed earlier, one can specify a fixed p-value using method=peto(pvalue=0.001) to set $\rho_1=0.001$ for the first stages. The number of stages is indicated using nstages=5. The alternative hypothesis is the upper-sided (alt=upper), but if one wants to change it to the two-sided, then alt=twosided. This design allows for stopping early only to reject or modify it or to retain the null hypothesis as indicated in stop=reject which is the default setting. This is early stopping for efficacy only. If one wants to allow the trial to stop early for efficacy or utility (i.e. to reject or retain the null hypothesis), then it can be replaced with stop=both. The type II error allowable is specified by alpha=0.025 while type II error is given by beta=0.1. The alternative mean difference $\theta_1$ is assumed to be 0.02, which is treatment difference from baseline and is specified in alter=0.02. In the samplesize statement, we invoke model=twomeample standard deviation of 0.045. The remaining options are used to request output of expected stopping stages and cumulative stopping probability effect size size from zero to 1.5 under alternative. The errspend statement displays the cumulative error at each stage. The design is fully specified and the SAS output for this program is shown below.

Figure 2.1 Output for Example Code 2.5

#### SEQDESIGN Procedure Design: hpdesignforth

##### Design Information

| Statistic | Normal |
| :--- | :--- |
| Boundary Scale | Standardized Z |
| Alternative Hypothesis | Upper |
| Early Stop | Reject Null |
| Method | Haybittle-Peto |
| Boundary Key | Both |
| Alternative Reference | 0.02 |
| Number of Stages | 5 |
| Alpha | 0.025 |
| Beta | 0.1 |
| Power | 0.9 |
| Max information (Percent of Fixed Sample) | 101.3932 |
| Max Information | 268.54 |
| Null ASN | 101.1638 |
| Alt ASN (Percent of Fixed Sample) | 78.7509 |

##### Expected Cumulative Stopping Probabilities = CRef + (Alt Reference)

| CRef | Expected Stopping Stage | Stopping Probabilities Stage_1 | Stage_2 | Stage_3 | Stage_4 | Stage_5 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 0.0000 | 4.989 | Reject Null | 0.00315 | 0.00246 | 0.00337 | 0.00413 | 0.02500 |
| 0.5000 | 4.814 | Right | 0.01165 | 0.03112 | 0.05645 | 0.08639 | 0.38648 |
| 1.0000 | 3.884 | Right | 0.06515 | 0.19151 | 0.35211 | 0.51070 | 0.90000 |
| 1.5000 | 2.504 | Right | 0.20885 | 0.55755 | 0.80410 | 0.92702 | 0.99820 |

##### Boundary Information (Standardized Z Scale) Null Reference = 0

| Alternative | Boundary Values |
| :--- | :--- |
| Information Level | Upper |
| Reference | Alpha |
| Stage_ | Proportion | Actual | N | Upper | Alpha |
| 1 | 0.2000 | 5326.99 | 43.14795 | 1.45971 | 3.00000 |
| 2 | 0.4000 | 10653.82 | 86.24992 | 2.06435 | 3.00000 |
| 3 | 0.5000 | 15960.73 | 126.4493 | 2.52830 | 3.00000 |
| 4 | 0.8000 | 21307.64 | 172.5818 | 2.91645 | 3.00000 |
| 5 | 1.0000 | 26534.54 | 215.7398 | 3.26402 | 1.99005 |

##### Error Stopping Information

| Cumulative Error Stopping | |
| :--- | :--- |
| Information Level | Upper |
| Stage_ | Proportion | Actual | Alpha |
| 1 | 0.2000 | 0.00000 | 0.00135 |
| 2 | 0.4000 | 0.00000 | 0.00246 |
| 3 | 0.6000 | 0.00000 | 0.00337 |
| 4 | 0.8000 | 0.00000 | 0.00413 |
| 5 | 1.0000 | 0.01000 | 0.02500 |

##### Sample Sizes (N)

##### Two-Sample Z Test for Mean Difference

| Fractional N | Ceiling N |
| :--- | :--- |
| Stage_ | N(Grp 1) | N(Grp 2) | Information | N(Grp 1) | N(Grp 2) | Information |
| 1 | 43.15 | 21.57 | 21.57 | 5326.9 | 44 | 22 | 5432.1 |
| 2 | 86.30 | 43.15 | 43.15 | 10653.8 | 88 | 44 | 10854.2 |
| 3 | 129.44 | 64.72 | 64.72 | 15960.7 | 135 | 65 | 16049.4 |
| 4 | 172.59 | 86.30 | 86.30 | 21307.6 | 174 | 87 | 21481.5 |
| 5 | 215.74 | 107.87 | 107.87 | 26534.5 | 216 | 108 | 26656.7 |
