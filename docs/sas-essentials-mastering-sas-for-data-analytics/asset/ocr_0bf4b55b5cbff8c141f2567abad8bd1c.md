# HANDS-ON EXAMPLE

This example performs an ANCOVA to compare three methods of teaching a fifth-grade math concept.

+   1. Open the program file AGLM ANCOVA.SAS.

```
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
n* IF SLOPES ARE PARALLEL, DROP THE INTERACTION TERM;
PROC GLM;
CLASS METHOD;
MODEL FINAL=EXAM METHOD;
LSMEANS METHOD/STERR PDIFF ADJUST=SCHEFFE;
RUN;
QUIT;
```

Note that PROC GLM is run twice. The first instance is to test that the slopes are parallel. This is tested with the following MODEL statement:

MODEL FINAL=EXAM METHOD*METHOD;

The EXAM*METHOD factor in the interaction is not significant (or parallel slopes) factor. The test for this factor is not significant, it suggests that the slopes among types of METHOD can be treated as parallel.

+   2. Run the program. As mentioned in Chapter 13, we recommend using the Type III sums-of-squares. Observe these sums-of-squares in the output given in Table 14.2. The row for the interaction term (EXAM*METHOD) is nonsignificant (p=0.6835). This provides evidence that the slopes can be treated as parallel and that the ANCOVA is an appropriate analysis.

+   3. Because the slopes are not significantly parallel, the second PROC GLM analysis is appropriate. Note that the interaction term has been removed from the MODEL statement.

(continued)