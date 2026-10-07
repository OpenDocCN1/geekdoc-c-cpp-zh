# 6.4.1 Brief Introduction to the Emax Model

This section describes two simulated practical examples for continuous and binary endpoints. The simulated data assume that there are 5 dose groups, 0mg (placebo), 2.5mg, 5mg, 10mg, and 20mg, in a phase II dose ranging trial. The sample size in each dose group is 60. The mixed procedure is used to fit 4-parameter models to analyze the data. Note that proc nlin in SAS could be used to fit the 4-parameter model as well, which is dedicated to the nonlinear regression model. Both procedures produce very similar estimates and results. In addition, code for trend tests for PoC, using the contrast (generated with the polyorth macro) accounting for equal or unequal dose spacing, are included for practical purpose for readers on both the continuous and binary endpoint cases.

The model is one of the commonly used nonlinear endpoint in dose response studies [24]. The model is shown below,

```
$y_i = E_0 + E_{max} \tilde{A} - \frac{D_i^h}{ED_{50}^h + D_i^h} + I\mu_i$,
```

where

+   1. $i$ is the subject ID
2. $y_i$ is the observed continuous response variable for the $th$ patient
3. $E_0$ is the basal effect, i.e., the response when the dose is 0 mg
4. is the maximum effect attributable to the drug
5. $ED_{50}$ is the dose that produces half of
6. $h$ is the hill parameter, or slope, which measures the sensitivity of the response to the dose range of the drug, determining the steepness of the dose–response curve $(N > 0)$