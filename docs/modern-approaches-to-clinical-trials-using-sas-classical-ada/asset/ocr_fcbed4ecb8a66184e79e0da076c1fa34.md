the MTD of CRM dose. Six dose levels of the drug are considered, and the CRM skeleton is specified as
(p1, p2, p3, p4, p5, p6) = (0.05, 0.10, 0.25, 0.40, 0.55, 0.65). The MTD is defined as the dose that has a toxicity probability closest to the target toxicity %. Suppose the trial treated 5 cohorts with cohort size of 3, and the toxicity outcomes and dose assignments are listed below innToxicity Outcomes and Dose Assignments for First Hypothetical Trial.

# Table 5.1 Toxicity Outcomes and Dose Assignments for First Hypothetical Trial

| Cohort Sequence | Dose Level | Cohort Size | # of DLTs |
|---|---|---|--|
| 1 | 1 | 3 | 0 |
| 2 | 2 | 3 | 1 |
| 3 | 2 | 3 | 0 |
| 4 | 3 | 3 | 2 |
| 5 | 2 | 3 | 0 |

The SAS Macro %CRM in Example Code 5.1 Continual Reassessment Method can be used to analyze the cumulative data and determine the dose assignment under the CRM framework. The input parameters for the %CRM macro are currentdata, skeleton, target, and tostop. The currentdata parameter stores the observed data set based on the treated patients, and each row corresponds to the accumulated information for each cohort, where the three entries in each row represent the number of DLTs observed for each cohort, dose level, and number of patients for that cohort, respectively. The user must also specify the skeleton parameter, which is the specified toxicity denoted as target in the %CRM macro, which is set to be 0.3 as the default. In addition, the user can adjust the toxicity tolerance by changing the value of tostop. %CRM creates a plot that overlays the curves for the initial guess and the posterior estimate of toxicity probability for each dose level. The output variable of %CRM macro is the suggested dose for the next cohort of patients.

# Example Code 5.1 Continual Reassessment Method Macro

```
%macro CRM(currentdata,skeleton,target=0.3,tstop=0.9);
proc iml;
  use &currentdata;
```