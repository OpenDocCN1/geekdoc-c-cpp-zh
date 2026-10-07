# CHAPTER 9: EVALUATING QUANTITATIVE DATA

(continued)

+   (c) After HISTOGRAM/, add the option

NORMAL (COLOR=BROWN W=3)

to superimpose a normal plot on each histogram.
(d) Run the revised program and observe the revised program.

# 9.4 SUMMARY

In this chapter, you learned how to use PROC MEANS AND PROC UNIVARIATE to calculate basic statistics and graphics for describing the characteristics of a set of data.

# EXERCISES

+   9.1 Create histograms.
Use the WOUND data set (C:\SASDATA\WOUND) as in this chapter’s Hands-on Examples and create the following:
a. Create a matrix of histograms with RACE_CAT (three categories) using the pattern M3XO and CFILL=RED.
b. Place the key on the upper left corner (NW).
c. Add mean (MEAN='MEAN: (4.1)) to the list of statistics reported and standard deviation.
d. Put your name in a TITLE statement.
e. Redo the plot using solid blue bars.
f. For this exercise, capture the output using ODS RTF.

(Note: If color options do not work in this exercise, please the command ODS GRAPHICS OFF; at the beginning of your code. This is needed for some versions of SAS.)

# 9.2 Produce normal probability plots using PROC UNIVARIATE.

Using the WOUND data set from Exercise 9.1, use PROC UNIVARIATE with the statement

```
PROBLOT SBP/NORMAL (COLOR=BLUE W=5) ROWS=3;
```

to produce a normal probability plot by RACE_CATEGORY.

# 9.3 Assess normality using a Q–Q plot.

Open the file AUNI1.SAS. After VAR AGE and before the RUN; command, enter the statement

```
QQPLOT AGE;
```