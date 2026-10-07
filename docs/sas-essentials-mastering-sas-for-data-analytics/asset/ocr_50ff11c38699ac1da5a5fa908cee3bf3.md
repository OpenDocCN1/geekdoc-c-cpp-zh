# CHAPTER 16: LOGISTIC REGRESSION

The Hosmer and Lemeshow test is requested using the LACKFIT option in the MODEL statement. Another measure used to assess the fit is a receiver operating characteristic curve (ROC), which provides a measure of how well the model predicts outcomes.

# HANDS-ON EXAMPLE

This example illustrates the Hosmer and Lemeshow test and an ROC curve.

+   1. Open the program file ALOG4.SAS.

```
PROC LOGISTIC DATA="C:\SADATA\ACCIDENTS" DESCENDING;
CLASS GENDER RACE;
MODEL DEATH = PENETRATE ISS AGE GCS
/ EXPB
  LACKFIT
  RISKLIMITS
  CTABLE
  OUTROC=ROC;
TITLE 'Assess models predictive ability';
RUN;
QUIT;
```

+   * The LACKFIT option requests a Hosmer and Lemeshow analysis.
* CTABLE requests predictions for various probability cutoff points.
* The OUTROC=1 statement along with the ODS GRAPHICS ON and ODS GRAPHICS statements produces an ROC curve.

+   2. Run the program. Observe the Hosmer and Lemeshow tables in Table 16.7. SAS computes a chi-square from observed and expected frequencies in the table.

Large-square values (and correspondingly small p-values) indicate a lack of fit for the model. In this case, we see that the Hosmer and Lemeshow chi-square test for the final model yields a p-value of 0.2532, suggesting a model with satisfactory predictive value. Note that the Hosmer and Lemeshow chi-square test is not a test of importance of specific model parameters. It is a separate post test to evaluate an entire model.

+   3. Examine the Classification table (partially) in Table 16.8. As mentioned earlier, it is a common practice to use 0.5 for the cutoff for predicting occurrence. To predict nonoccurrence of the event of interest whether p<0.5 and to predict occurrence if p≥0.5. The Classification table indicates how many correct and incorrect predictions would be made for a wide range of probability cutoff points used for the model. In this case, 98% of the cases are correctly classified using the 0.5 cutoff point.

Note that at the 0.50 cutoff point, there is 38.8% sensitivity and 99.7% specificity. With the outcome of interest, and specificity is the probability of a correct prediction among subjects who do not exhibit the outcome.) If you desire to gain sensitivity, you can move the cutoff point to a lower probability level (at the sacrifice of specificity). Similarly, you can increase specificity by raising the cutoff probability. (For more information about selecting a cutoff point, see Cohen, Cohen, West and Aiken (2002), p. 516 or Hosmer and Lemeshow (2000), p. 160.)