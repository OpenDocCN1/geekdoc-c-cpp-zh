# CORRELATION ANALYSIS USING PROC CORR 285

# TABLE 12.1 (Continued)

| Option | Explanation |
|---|---|
| Common statements for PROC CORR | |
| VAR variable list | All possible pairwise correlations are calculated for the variables listed and displayed in a table |
| WITH variable(s); | All possible correlations are obtained between the variables in the VAR list and variables in the WITH list |
| MODEL | Specifies the dependent and independent variables for the analysis. More specifically, it takes the form MODEL dependent=independentvar(s); More explanation |
| BY, FORMAT, WHERE | These statements are common to most procedures and may be used here |

# HANDS-ON EXAMPLE

This example illustrates how to calculate Pearson correlations on several variables in a data set.

+   1. Open the program file ACORR1.SAS.

PROC CORR DATA="C:\SASDATA\SOMEDATA";
VAR AGE TIME1;
TITLE "Example correlations using PROC CORR";
RUN;

+   2. Run the program and observe the results in Table 12.2. Table 12.1 contains pairwise Pearson correlations between each of the three variables listed in the VAR statement. For example, the correlation between AGE; TIME1 is r=0.50088, and the p-value associated with the test of $H_0$: $ho$ is 0 is p=0.0002.

# TABLE 12.2 Output from PROC CORR

| Pearson Correlation Coefficients, N = 50 |
| Prob > |r| under H0: Rho=0 |
|---|---|---||
| AGE | TIME1 | TIME2 |
| Age on Jan 1, 2000 | 1.00000 0.50088 0.38082 |
| | 0.0002 0.0064 |
| TIME1 | 0.50088 1.00000 0.76396 |
| Baseline | 0.0002 <.0001 |
| TIME2 | 0.38082 0.76396 1.00000 |
| 6 Months | 0.0064 <.0001 |

(continued)