# GOING DEEPER: REPEATED MEASURES WITH A GROUPING FACTOR 343

(We include SUBJECT here though we are not generally interested in a SUBJECT effect, in order to fully define the model.) The MODEL statement indicates that OUTCOME is the dependent variable and GENDER, TIME, and the interaction term GENDER*TIME are independent variables used to predict outcome.

The REPEATED statement indicates the TYPE of covariance structure to use in the analysis. The TYPE of covariance structures is the only difference among the three calls to PROC MIXED. SUB=SUBJECT indicates the name of the subject variable.

+   Run the program. A lot of output is created by SAS for this analysis, much of it dealing with the iterations to fit the model. This output will not be discussed here. Note the value of AIC (Akaike Information Criterion) in the Fit Statistics output. This is a measure of the fit of the model, with smaller AIC values considered. (There are other criteria you could also use, like BIC and AICC, but we'll limit our discussion to AIC).

You can fit any number of covariance structures to the data with the TYPE=statement and then select the best-fitting model. In this example, based on the AIC criterion, the AR(1) specification fits the data. For these three models, the AIC results from the Fit Statistics table associated with each covariance structure considered as follows:

+   * AIC(unstructured)= 71.0
* AIC(compound symmetry)= 77.6
* AIC(autoregressive)= 70.2

The primary tests for this model are found in the table titled "Type 3 Test of Fixed Effects." Because the AIC for the AR(1) model is lower, we will examine the results in that table, as shown in Table 14.12.

TABLE 14.12 Results from PROC MIXED for AR(1)

| Type 3 Tests of Fixed Effects |
| Effect | Num DF | Den DF | F Value | Pr > F |
| GENDER | 1 | 5 | 5.22 | 0.0710 |
| TIME | 3 | 14 | 29.67 | <.0001 |
| GENDER*TIME | 3 | 14 | 1.48 | 0.2637 |

In this case, the results indicate that there is no interaction (GENDER*TIME, p=0.26) effect. In the presence of no interaction, it is appropriate to examine the main tests for TIME and GENDER. For these results, there is a significant TIME (p <0.0001) effect and a nonsingular (but marginal) GENDER (p=0.071) effect.

The other models (unstructured and compound symmetry) report a significant GENDER effect (both p<0.05). Thus, the structure selected can affect the outcome of the statistical tests.

(continued)