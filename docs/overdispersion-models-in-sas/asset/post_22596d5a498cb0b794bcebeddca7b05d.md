
## Chapter 9 Generalized Estimating Equations Techniques for Marginal Models

### 9.9 A Shoulder Pain Patient Example

Lumley (1996) and Luo (2000) analyzed data from a randomized clinical trial of abdominal suction to reduce shoulder pain after laparoscopic surgery. The data were originally analyzed in Jorgensen et al. (1995). Inflation of the abdomen during surgery separates the liver from the diaphragm and places strain on the attachments that connect both. This strain is felt as referred pain in the shoulder. Removal of residual fascia may reduce shoulder strain. There were 22 subjects in the active group (with abdominal suction) and 19 subjects in the control group (without abdominal suction). After laparoscopic surgery, patients were asked to rate their shoulder pain on a visual analog scale and for three days after the operation (a total of six different times). Since there were too many zeros, the scale was reduced into ordered categories where a pain score of “1” indicated “low pain,” and a score of “5” reflected “high pain.” In addition to the treatment variable, there were three covariates, namely Age, Gender and Time. Covariates were subject- and time-specific. The data on shoulder pain after laparoscopic cholecystectomy (removal of the gallbladder) are shown on Table 9.5.

Let $y_{ijt}$ represent the response of the $j$-th subject in the $i$-th treatment group at $t$-th time, $i=1, 2,\dots,n$ ($n=22, t=1,2,\dots,6$). The number of categories for response vector is, thus $d=4$. The space of the $y_{ijt}$ is:

$$y_{ijt} \in \begin{pmatrix} 0 & 0 & 0 & 0 \\ 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 1 & 0 \end{pmatrix}$$

with

$$E(y_{ijt}) = \begin{pmatrix} \pi_{1ijt} \\ \pi_{2ijt} \\ \pi_{3ijt} \\ \pi_{4ijt} \end{pmatrix}$$

As customary $\pi_{5ijt} = 1 - \sum_{k=1}^4 \pi_{kij}$. We will fit a GEE Cumulative Logit model (Marginal Model) with "sandwich" estimator (9.24) and mean-

$$\ln \left( \pi_{ijt} / (\pi_{2ijt} + \pi_{3ijt} + \pi_{4ijt} + \pi_{5ijt}) \right) = \alpha_1 + \beta_1 X_{1ijt} + \beta_2 X_{2ijt} + \beta_3 X_{3ijt} + \beta_4 t_t$$
$$\ln \left( \pi_{ijt} / (\pi_{2ijt} + \pi_{3ijt} + \pi_{4ijt} + \pi_{5ijt}) \right) = \alpha_2 + \beta_1 X_{1ijt} + \beta_2 X_{2ijt} + \beta_3 X_{3ijt} + \beta_4 t_t, \quad (9.25)$$
$$\ln \left( \pi_{ijt} / (\pi_{3ijt} + \pi_{4ijt} + \pi_{5ijt}) \right) = \alpha_3 + \beta_1 X_{1ijt} + \beta_2 X_{2ijt} + \beta_3 X_{3ijt} + \beta_4 t_t$$
$$\ln \left( \pi_{ijt} / (\pi_{4ijt} + \pi_{5ijt}) \right) = \alpha_4 + \beta_1 X_{1ijt} + \beta_2 X_{2ijt} + \beta_3 X_{3ijt} + \beta_4 t_t$$

where $X_{19}$ and $X_{20}$ are properly coded classification variables representing, respectively, the treatment group and the gender; $X_{30}$ represents the subject's age. The model fitting will be done using the SURVEYLOGISTIC procedure.

Table 9.5: Data on Shoulder Tip Pain after Laparoscopic Cholecystectomy

| Treatment Group | Gender | Age (Years) | Time 1 | Time 2 | Time 3 | Time 4 | Time 5 | Time 6 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Y | F | 64 | 1 | 1 | | 1 | 1 | 1 |
| Y | M | 41 | 3 | 2 | | 1 | 1 | 1 |
| Y | F | 77 | 3 | 2 | 2 | 1 | 1 | 1 |
| Y | F | 54 | 1 | 1 | | 1 | 1 | 1 |
| Y | F | 66 | 1 | 1 | 1 | 1 | 1 | 1 |
| Y | M | 56 | 1 | 2 | | 1 | 1 | 1 |
| Y | M | 81 | 1 | 3 | 2 | | 1 | 1 |
| Y | F | 24 | 2 | 2 | | 1 | 1 | 1 |
| Y | F | 56 | 1 | 1 | | 1 | 1 | 1 |
| Y | F | 29 | 3 | 1 | | 1 | 1 | 1 |
| Y | M | 65 | 1 | | | 1 | 1 | 1 |
| Y | F | 68 | 2 | 1 | | 1 | 1 | 2 |
| Y | F | 77 | 1 | 1 | 2 | 2 | 2 | 2 |
| Y | M | 35 | 3 | 1 | 1 | | 3 | 3 |
| Y | F | 66 | 2 | 1 | | 1 | 1 | 1 |
| Y | F | 70 | 1 | 1 | | 1 | 1 | 1 |
| Y | F | 79 | 1 | 1 | | 1 | 1 | 1 |
| Y | F | 65 | 2 | 1 | | 1 | 1 | 1 |
| Y | F | 61 | 4 | 4 | 2 | | 2 | 2 |
| Y | F | 67 | 4 | 4 | 4 | 2 | | 1 |
| Y | F | 32 | 1 | 1 | | 2 | 1 | 1 |
| Y | F | 33 | 1 | 1 | 1 | 2 | | 2 |
| N | F | 20 | 5 | 2 | 3 | 5 | 5 | 4 |
| N | F | 50 | 1 | 5 | 3 | 4 | 5 | 3 |
| N | F | 40 | 4 | 4 | 4 | 4 | 1 | 3 |
| N | M | 54 | 4 | 4 | 4 | 4 | 4 | 3 |
| N | M | 34 | 2 | 3 | 4 | 3 | 3 | 2 |
| N | F | 34 | 3 | 4 | 4 | 3 | 3 | 2 |
| N | M | 56 | 3 | 3 | 4 | 4 | 4 | 3 |
| N | F | 82 | 1 | 1 | | 1 | 1 | 1 |
| N | M | 56 | 1 | 1 | 1 | 1 | 1 | 1 |
| N | M | 52 | 1 | 5 | 5 | 4 | 3 | 3 |
| N | F | 65 | 1 | 3 | 2 | 2 | 1 | 1 |
| N | F | 53 | 2 | 2 | 3 | 4 | 2 | 2 |
| N | F | 40 | 2 | 2 | 1 | 3 | 3 | 3 |
| N | M | 58 | 1 | 1 | 1 | 1 | 1 | 1 |
| N | F | 63 | 1 | 1 | 1 | 1 | 1 | 1 |
| N | M | 41 | 5 | 5 | 4 | 3 | 3 | 3 |
| N | M | 72 | 3 | 3 | 3 | 1 | 1 | 1 |
| N | F | 60 | 5 | 4 | 4 | 2 | 2 | 2 |
| N | M | 61 | 1 | 3 | 3 | 2 | 2 | 1 |

Program 9.6 provides the programming statements for reading the data of Table 9.5, and for fitting the GEE Logit model previously discussed.

Program 9.6: Fitting a GEE Logit Model to the Shoulder Tip Data

```sas
Reference: Lumley, T. (1996) "Generalized Estimating Equations for Ordinal Data: A Note on Working Structures." Biometrics 52, 354-363
data Shoulder_tip_pain;
  input trt $ gender $ age t1-t6;
  subject_id = _n;
  array tt t1-t6;
  do tt;
    y = tt;
    time = _i;
    output;
  end;
  datalines;
  y f 64 1 1 1 1 1
  y m 41 3 2 2 1 1
  y f 77 3 2 2 1 1
  y m 54 1 1 1 1 1
  y f 66 1 1 1 1 1
  y m 56 2 1 1 1 1
  y f 81 3 2 1 1 1
  y m 24 2 2 1 1 1
  y f 56 1 1 1 1 1
  y m 29 3 1 1 1 1
  y f 65 1 1 1 1 1
  y m 68 2 1 1 1 2
  y f 77 1 1 2 2 2
  y m 35 3 1 1 3 3
  y f 66 2 1 1 1 1
  y m 70 1 1 1 1 1
  y f 79 1 1 1 1 1
  y m 65 2 1 4 2 2
  y f 61 4 4 2 2 1
  y m 67 4 4 2 1 1
  y f 32 1 1 2 1 2
  y m 33 1 1 2 1 2
  y f 20 5 2 3 5 4
  y m 50 1 5 3 4 3
  y f 40 4 4 4 4 1
  y m 54 4 4 4 4 3
  y m 34 2 3 4 3 3
  y f 34 3 4 3 3 2
  y m 56 3 3 4 4 3
  y f 82 1 1 1 1 1
  y m 52 1 5 5 4 3
  y f 65 1 3 2 2 1
  y m 53 2 2 3 4 2
  y f 40 2 2 1 3 3
  y m 58 1 1 1 1 1
  y f 63 1 1 1 1 1
  y m 41 5 5 4 3 3
  y m 72 3 3 3 1 1
  y f 60 5 4 4 2 2
  y m 61 1 3 3 2 1
;;
```

Selected results are shown in logarithm of the odds-ratios 9.6. Note that the Wald Chi-square for testing the significance of results from comparing the active (abdominal section) versus the placebo (no abdominal suction) is 14.52. This statistic is highly significant (P-value=0.0001). The corresponding odds-ratio is 6.7 with an associated 95% confidence interval of (2.53,18.09). These results strongly support the observation that subjects in the active group experience less pain after surgery. This corresponds to an approximate six-fold reduction in pain. Observe also that the beta estimate related to the variable time is highly significant (P<0.01). The odds-ratio corresponding to a unit increase in time turned out to be 1.22 with an associated 95% confidence interval of (1.05,1.44). By default, SURVEYLOGISTIC models the probability of the lower end of the pain scale. Therefore, time odds ratio being greater than one indicates a lessening of pain with time.
