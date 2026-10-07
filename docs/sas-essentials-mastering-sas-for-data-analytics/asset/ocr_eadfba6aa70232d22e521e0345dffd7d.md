# HANDS-ON EXAMPLE

This example (adapted from data 404 in Hand, Doly, McConway, Lunn, and Ostrowski [1994]) concerns a study on weight loss for those meeting about dieting. A variable called CONDITION indicates whether the patient received a weight loss (CONDITION=1) or not (CONDITION=2). The STATUS variable indicates whether the patient had already been trying to lose weight before the series of meetings (STATUS=1) or not (STATUS=2).

Both factors are assumed to be fixed effects for this example, and there are an unequal number of subjects in each category. For this case, PROC GLM can be used.

Open the program file AGLM 2FACTOR. SAS.

```
DATA SLIM;
INPUT CONDITION STATUS RESPONSE;
DATALINES;
1 -13.67 1 -12.85 1 1 -9.55 5 1 -17.03 1 13.61
2 -9.91 2 2.48 1 2.84 1 2.6 1 2 20.2 2 -73
2 -30.05 1 -5.68 1 -3.44 1 -7.18 2 -3.40 1 -74
1 -23.29 1 -4 2 -2.31 1 -3.42 1 -7.49 1 -13.62
1 -73.54 1 -1.91 2 -4.2 2 -12.01 2 1 -8.35
2 5.94 2 -1.91 2 -4.0 2 -5.19 2 0 2 2 -2.8

RUN;
TITLE "Two-Way ANOVA Example";
PROC GLM;
CLASS CONDITION STATUS;
MODEL RESPONSE=CONDITION STATUS CONDITION*;
MEANS CONDITION STATUS CONDITION*;

RUN;
QUIT;
```

Recall that in the MODEL statement, the dependent variable (RESPONSE) appears to the left of the equal sign and the independent variables (CONDITION and STATUS) appear to the right. The CONDITION*STATUS component of the model statement is the interaction term. The two factors, CONDITION and STATUS, are listed in the CLASS statement because they are categorical variables.

2. Run this program and observe the output, partially illustrated in Table 14.5. This is output from the first PROC GLM statement in the code. Note that the overall model is significant (p=0.04), indicating the presence of some differences in means. Note also that because of the unequal number of observations per cell, the Type I III sums-of-squares (SS) give different results. It is recommended that Type III SS be used, and only that SS table is given in Table 14.5.

3. For this analysis, first examine the interaction effect (the CONDITION*STATUS row) in the Type III ANOVA table. Because p=0.7872, there is no evidence of interaction. As mentioned previously:

+   If there is no interaction, examine the main effects tests in the ANOVA table by comparing marginal means.

(continued)