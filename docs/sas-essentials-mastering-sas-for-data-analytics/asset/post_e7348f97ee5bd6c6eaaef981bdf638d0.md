
## HANDS-ON EXAMPLE

This example performs an ANCOVA to compare three methods of teaching a fifth-grade math concept.

- 1. Open the program file AGLM ANCOVA.SAS.

```sas
DATA ANCOVA;
INPUT METHOD EXAM FINAL @@;
DATALINES;
1 36 38 1 37 39 1 35 41
1 43 47 1 32 33 1 33 37
2 42 41 2 30 30 2 39 45
2 26 28 2 22 25 2 37 39
3 23 30 3 40 49 3 34 43
3 30 38 3 25 32 3 31 37
RUN;
PROC GLM;
CLASS METHOD;
MODEL FINAL=EXAM METHOD*METHOD;
TITLE 'Analysis of Covariance Example';
/* IF SLOPES ARE PARALLEL, DROP THE INTERACTION TERM; */
PROC GLM;
CLASS METHOD;
MODEL FINAL=EXAM METHOD;
LSMEANS METHOD/STERR PDIFF ADJUST=SCHEFFE;
RUN;
QUIT;
```

Note that PROC GLM is run twice. The first instance is to test that the slopes are parallel. This is tested with the following MODEL statement:

`MODEL FINAL=EXAM METHOD*METHOD;`

The EXAM*METHOD factor in the interaction is not significant (or parallel slopes) factor. The test for this factor is not significant; it suggests that the slopes among types of METHOD can be treated as parallel.

- 2. Run the program. As mentioned in Chapter 13, we recommend using the Type III sums-of-squares. Observe these sums-of-squares in the output given in Table 14.2. The row for the interaction term (EXAM*METHOD) is nonsignificant (p=0.6835). This provides evidence that the slopes can be treated as parallel and that the ANCOVA is an appropriate analysis.

- 3. Because the slopes are not significantly parallel, the second PROC GLM analysis is appropriate. Note that the interaction term has been removed from the MODEL statement.

## CHAPTER 14: ANALYSIS OF VARIANCE, PART II

TABLE 14.2 Test of Slopes for Analysis of Covariance
| Source | DF | Type III SS | Mean Square | F Value | Pr > F |
| --- | --- | --- | --- | --- | --- |
| EXAM | 1 | 476.4504266 | 476.4504266 | 114.76 | < 0001 |
| METHOD | 2 | 0.8199072 | 0.4099536 | 0.10 | 0.9067 |
| EXAM*METHOD | 2 | 3.2623239 | 1.6311619 | 0.39 | 0.6835 |

TABLE 14.3 Analysis of Covariance of Main Effects

| Source | DF | Type III SS | Mean Square | F Value | Pr > F |
| --- | --- | --- | --- | --- | --- |
| EXAM | 1 | 627.916352 | 627.916352 | 165.60 | < 0001 |
| METHOD | 2 | 105.9908664 | 52.9904332 | 13.98 | 0.0005 |

```sas
FINAL=EXAM METHOD;
forcing the model to assume equal regression lines
```

Table 14.3 shows the Type III SS output table for the second PROC GLM. The factor of interest in this table is METHOD, and the corresponding F is a statistical test comparing the three methods for adjusting EXAM. Because p=0.0005, we reject the null hypothesis that the adjusted means are equal and conclude that at least one pair of adjusted means are different from each other.

- 4. Because we found a difference in adjusted means, pairwise comparisons can be used to identify which adjusted means are different from each other. The statement that provides comparison is

`LSMEANS METHOD/STERR PDIFF ADJUST=SCHEFFE;`

In this case, we have chosen to use the Scheffe multiple comparisons, and the results are given in Table 14.4. (Ignore the Pr > F column, it is testing that the method is different from zero, which is of no interest in this analysis).

The Scheffe provides p-values for each pairwise comparison. In this, the comparisons of METHODS 1 and 3 (p=0.0056) and 2 and 3 (p=0.0007) indicate significant differences. METHODS 1 and 2 are not significantly different (p=0.68).

Because a FINAL score is the goal, there is evidence to support the contention that the adjusted mean of 40.82 for METHOD 3 is a significantly higher score than METHODS 1 and 2, and thus that METHOD 3 is the preferred method.

- 5. Along with the tabled output, SAS includes several graphs. For the first PROC GLM (that included the interaction term) you get the plot shown in Figure 14.1. It shows the three regression lines by METHOD. Note that the lines are near parallel, which confirms the findings in the first PROC GLM procedure. (We show these plots as created using the ODS STYLE=JOURNAL option. See Chapter 8 for more on ODS. Your plots may appear in color.)

## TABLE 14.4 FINAL Scheffe Multiple Comparisons for ANCOVA

| METHOD | FINAL | LSMEAN | Standard Error | Pr > |t| | LSMEAN Number |
|---|---|---|---|---|---|---|
| 1 | | 36.094608 | 0.8300185 | <0001 | | 1 |
| 2 | | 35.072410 | 0.7955731 | <0001 | | 2 |
| 3 | | 40.832982 | 0.8211505 | <0001 | | 3 |

| Least Squares Means for effect METHOD
Pr > H0: LSMean(i)=LSMean(j)
Dependent Variable: FINAL
| | 1 | 2 | 3 |
|---|---|---|---|
| 1 | | 0.6837 | 0.0056 |
| 2 | 0.6837 | | 0.0007 |
| 3 | | 0.0056 | |
