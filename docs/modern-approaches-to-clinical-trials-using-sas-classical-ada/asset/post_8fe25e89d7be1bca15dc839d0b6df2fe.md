
To compute the type I error and power in (4.7), we use the algorithm discussed in 4.6.3 Power Calculation. From the code (Example Code 4.3 Calculation of the Type I Error and Power) in the macro, we allow the user to choose the Bayesian credible level (η). The macro also automatically produces the results using Bayesian credible levels, 0.90, 0.95, and 0.975 as a default option. This partial code shows the approach that is used to calculate the type I error and power, which are the proportions in (4.14) under various Bayesian credible levels based on the posterior sample of $\gamma_1$. In the code, the posterior estimates are saved in the data postout and phat is the proportion satisfying exp {(m)<0} calculated from the posterior samples for each simulated data set. From the data outpower, we can accumulate the value of phat across simulated data sets. The data TypeError is used for calculating the type I error in (4.7) using the algorithm discussed in 4.6.3 Power Calculation. The data set BayesianPower in the macro is used to calculate the power.

## Example Code 4.3 Calculation of the Type I Error and Power

```sas
data indicator(keep=proportion);
  set postout;
  proportion=(exp(gamma))<;
run;
proc means data-indicator n mean noprint;
  var proportion;
  output out=outpower mean=pfhat;
run;
data outpower;
  set outpower;
  simid&m;
  keep simid pfhat;
run;
%if &m=1 %then %do;
  data proportion&s;
  set outpower;
run;
%else %do;
  data proportion&s;
  set proportion&s outpower;
run;
%end;
data TypeError;
  set proportion0;
  keep pfhat BP1 BP2 BP3 BP4;
  BP1=0;BP2=0;BP3=0;BP4=0;
  if pfhat>0.90 then BP1=1;
  if pfhat>0.95 then BP2=1;
  if pfhat>0.975 then BP3=1;
  if pfhat>&a0 then BP4=1;
run;
```

### 4.7.2 Illustrative Examples

#### 4.7.2.1 Evaluating Cardiovascular Risk

In this section, we illustrate the considered in the previous section. As an illustrative example, we use the motivating case study for designing a phase II/III development program of a new T2DM therapy. A more detailed setting of this illustrative example can be found in [10,11].

Several authors considered a hypothetical drug development program for treating type 2 diabetes mellitus [10-12]. The program includes eight randomized control efficacy superiority trials and one large randomized CV outcome non-inferiority trial. For those traditional diabetes HbA1c superiority trials, the target subjects are at low or moderate CV risk with an assumed annualized event rate of 1.2%. On the other hand, for the non-inferiority trial, the subjects are at high risk with an assumed annualized event rate of 1.5% as the FDA guidance advocates the inclusion of such a population. A detailed description of the data can be found in [10-12].

In this study, the historical data are available only for the control arm. This is the first type of historical data (control arm only) discussed in 4.2.3 Input Historical Data and the original historical data in [10] are shown in Original Historical Data for the Cardiovascular Risk Study and Historical Data Shown in RTF Output File for the Cardiovascular Risk Study. Also, we output the historical data in Table 4.6.

#### Table 4.5 Original Historical Data for the Cardiovascular Risk Study

| Reference | Number of Subjects | Number of CV Events | Total Patient Years | Annualized Event Rate (%) |
|---|---|---|---|---|
| ACCORD (2008) | 5,123 | 371 | 16,000 | 2.29 |
| ADVANCE (2008) | 5,569 | 590 | 27,845 | 2.10 |
| Saxagliptin (2009) | 1,251 | 17 | 1,289 | 1.31 |
| Liraglutide (2009) | 907 | 4 | 449 | 0.89 |
| Liraglutide (2009) | 1,474 | 13 | 1,038 | 1.24 |

#### Table 4.6 Historical Data Shown in RTF Output File for the Cardiovascular Risk Study

| Trial ID | Total Subject Size | Year Duration | Total Number of Events | Trial Arm |
|---|---|---|---|---|
| 1 | | 16,000 | 371 | 0 |
| 2 | | 27,845 | 590 | 0 |
| 3 | | 1,289 | 17 | 0 |
| 4 | | 449 | 4 | 0 |
| 5 | | 1,038 | 13 | 0 |

For the predetermined design values, the non-inferiority design margin is specified in (4.7), and to ensure that the type I error is controlled under 0.05, we choose $\eta_0=0.96$ as discussed in [6] and recommended by the FDA guidance [14]. We define in advance the proportion in the control arm, annualized event rates, and accrual times as well. Under these settings, we compile the current data in Current Data in the Cardiovascular Risk Study.

#### Table 4.7 Current Data in the Cardiovascular Risk Study

| Trial ID | Total Sample Size | Proportion in Control Arm | Annualized Event Rate | Accrual Time | Trial Duration | Follow-up Time |
|---|---|---|---|---|---|---|
| 1 | 150 | 0.17 | 0.012 | 0 | 0.077 | 0.077 |
| 2 | 350 | 0.40 | 0.012 | 0 | 0.462 | 0.462 |
| 3 | 3,500 | 0.40 | 0.012 | 0 | 2 | 2 |
| 4 | 400 | 0.25 | 0.012 | 0 | 0.462 | 0.462 |
| 5 | 375 | 0.20 | 0.012 | 0 | 0.462 | 0.462 |
| 6 | 740 | 0.25 | 0.012 | 0 | 0.462 | 0.462 |
| 7 | 750 | 0.33 | 0.012 | 0 | 0.462 | 0.462 |
| 8 | 564 | 0.33 | 0.012 | 0 | 0.462 | 0.462 |
| 9 | 8,000 | 0.50 | 0.015 | 2 | 4 | 2 |

Using PROC REPORT in the macro, we reproduce the predetermined design values in the study. Design Values in the Cardiovascular Risk Study shows the predetermined design margin, the discounting parameter ($\theta_0$) for the historical data, and the initial variances of the parameters, $\gamma_0, \gamma_1, \theta_k$ for $k=1, \dots$ and $\theta_k$ for $k=1, \dots$.

#### Table 4.8 Design Values in the Cardiovascular Risk Study

| Design Margin | Discounting Parameter | User-Defined Credible Level | Initial Variance of $\gamma_0$ | Initial Variance of $\gamma_1$ | Initial Variance of $\theta_0$ |
|---|---|---|---|---|---|
| 1.3 | 0.10 | 0.96 | 10 | 10 | 10 |

The type I error and power can be obtained by running the BSMED macro, and are shown in Design Values in the Cardiovascular Risk Study and Type I Error Provided from BSMED. These quantities are calculated from 5000 data sets. As shown in Table 4.9 and Power Provided from BSMED, the Bayesian type I error and power are 0.0506 and 0.8774, respectively. We note that the type I error was not controlled at 5%, but the power was above 0.80 when borrowed ($\alpha_0 = 0.10$) from the historical data.

#### Table 4.9 Type I Error Provided from BSMED

| Type I with Credible Level | Type I with Credible Level | Type I with Credible Level | Type I with User Choice Variance |
|---|---|---|---|
| 0.90 | 0.95 | 0.975 | 0.96 |
| 0.1190 | 0.0614 | 0.0324 | 0.0506 |

#### Table 4.10 Power Provided from BSMED

| Power with Credible Level | Power with Credible Level | Power with Credible Level | Power with User Choice |
|---|---|---|---|
| 0.90 | 0.95 | 0.975 | 0.96 |
| 0.9454 | 0.8994 | 0.8310 | 0.8774 |

#### 4.7.2.2 Evaluating Cardiovascular Risk Study with Artificial Experimental Arm Data

We consider a hypothetical study similar to the one discussed in the previous section but historical data available only for the experimental arm. To this, we artificially generated the total subject duration and the number of CV events using the annualized event rates in the historical study in [Names and Descriptions of Input Variables and Design Values]. From the relationship between the homogeneous Poisson process and the exponential distribution, we generated the total subject year duration of the experimental arm in the historical data, and the total number of events are easily obtained using those annualized event rates. [Artificial Historical Data for the Experimental Arm] shows the artificial historical data for the experimental arm and we see that this is the second type of historical data (experimental arm only) discussed in [4.2.3 Input Historical Data].

#### Table 4.11 Artificial Historical Data for the Experimental Arm

| Trial ID | Trial Subject Year Duration | Total Number of Events | Trial Arm |
|---|---|---|---|
| 1 | 301 | 4 | 1 |
| 2 | 438 | 4 | 1 |
| 3 | 318 | 4 | 1 |
| 4 | 152 | 4 | 1 |
| 5 | 164 | 3 | 1 |
