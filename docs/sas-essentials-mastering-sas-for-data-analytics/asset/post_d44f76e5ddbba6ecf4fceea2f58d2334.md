
```
DATALINES;
A 88
A 89
...etc...
; PROC TTEST DATA=TEMP;
CLASS ; VAR ;
...etc...
RUN;
```

c. What is your conclusion?

## 11.2 Perform a t-test on pre- and postdata.

To test if memory technique was effective, a researcher provided five people with a list of 10 objects for 45 seconds then tested them to see how many they remembered (pretest). He taught them a memory technique and presented them with a list of 10 different (although similar) objects and administered a similar test (posttest). The results follow:

| Subject | Pretest | Posttest |
|---|---|---|
| AD | 6 | 10 |
| GE | 7 | 7 |
| KL | 9 | 10 |
| MM | 4 | 7 |
| OU | 7 | 9 |

- a. Assuming that the differenced data are approximately normally distributed, analysis is appropriate to test the hypothesis that training subjects on a memory technique would improve their ability to remember a list of 10 objects?

- b. Using code similar to that in the paired t-test Hands-on Example, write a SAS program to perform the appropriate test for this analysis. Here is some code to get started:

```
DATA MEMORY;
INPUT PRETEST
DATALINES;
6 10
...etc...
; PROC TTEST DATA=MEMORY;
...etc...
RUN;
```

- c. What are your conclusions?

## 12

## CORRELATION AND REGRESSION

## LEARNING OBJECTIVES

- To be able to use SAS® procedures to calculate Pearson and Spearman correlations
- To be able to use SAS procedures to produce a matrix of scatterplots
- To be able to use SAS procedures to perform simple linear regression
- To be able to use SAS procedures to perform multiple linear regression
- To be able to use SAS procedures to calculate predictions using a model
- To be able to use SAS procedures to perform residual analysis

Correlation measures the association between two quantitative variables, and the closely related regression analysis uses the relationship between independent and dependent variables (response or outcome) for predicting the dependent (predictor or explanatory) variables using one or more independent-dependent variables. In simple linear regression, there is a single dependent variable and a single independent variable, while in multiple linear regression (MLR) there are two or more independent variables. In this chapter, we discuss the use of SAS to perform correlation and regression analyses.

## 12.1 CORRELATION ANALYSIS USING PROC CORR

Before proceeding to the use of SAS to perform correlation analysis, we first provide a brief discussion of the basics of correlation analysis.

## CHAPTER 12: CORRELATION AND REGRESSION

## 12.1.1 Correlation Analysis Basics

The correlation coefficient is a measure of the linear relationship between two quantitative variables measured on the same subject (entity). For example, you might study the relationship between height and weight for a sample of teenage boys. For two variables of interest, say X and Y, $\rho$ measures the extent to which a scatterplot of the bivariate distribution of X and Y tends to fall along a line. The correlation $\rho$ is a unitless quantity (i.e. it does not depend on the units of measurement) that ranges from -1 to +1 when $\rho=-1$ and $\rho=+1$ correspond to perfect negative and positive linear relationships, respectively and $\rho=0$ indicates no linear relationship.

In practice, it is of interest to test the hypotheses:

- $H_0: \rho = 0$: There is no linear relationship between the two variables.
- $H_1: \rho \neq 0$: There is a linear relationship between the two variables.

The correlation coefficient $\rho$ is typically estimated from data using the Pearson correlation coefficient, usually denoted as $r$. PROC CORR in SAS provides a test of the hypotheses designed to determine whether the estimated correlation, $r$, is significantly different from zero. This test assumes that the data represent a random sample from some bivariate normal distribution. If normality is not a good assumption, nonparametric estimates are available, the most popular of which is Spearman's $\rho$, which PROC CORR provides.

> To examine the nature of the relationship between two variables, it is always a good practice to look at scatterplots of the variables.

## 12.1.2 Using SAS PROC CORR for Correlation Analysis

The SAS procedure most used to calculate correlations is PROC CORR. The syntax for this procedure is as follows:

```
PROC CORR <options>; <statements>;
```

Table 12.1 lists common options and statements used with PROC CORR

| Option | Explanation |
| --- | --- |
| DATA = dataset-name | Specifies which data set to use |
| PEARSON | Requests Pearson correlation (default). |
| SPEARMAN | Requests Spearman rank correlations |
| NOSIMPLE | Suppresses display of descriptive statistics |
| NOPB | Suppresses the display of p-values |
| PLOTS= | PLOTS=MATRIX requests individual scatterplots. PLOTS=MATRIX (HISTOGRAM) statement requests a scatterplot matrix with embedded histograms |
| OTP= | Specifies an output data set continuing Pearson correlations |

(continued)

## CORRELATION ANALYSIS USING PROC CORR 285

## TABLE 12.1 (Continued)

| Option | Explanation |
|---|---|
| Common statements for PROC CORR | |
| VAR variable list | All possible pairwise correlations are calculated for the variables listed and displayed in a table |
| WITH variable(s); | All possible correlations are obtained between the variables in the VAR list and variables in the WITH list |
| MODEL | Specifies the dependent and independent variables for the analysis. More specifically, it takes the form MODEL dependent=independentvar(s); More explanation |
| BY, FORMAT, WHERE | These statements are common to most procedures and may be used here |

## HANDS-ON EXAMPLE

This example illustrates how to calculate Pearson correlations on several variables in a data set.

- 1. Open the program file ACORR1.SAS.

```
PROC CORR DATA="C:\SASDATA\SOMEDATA";
VAR AGE TIME1;
TITLE "Example correlations using PROC CORR";
RUN;
```

- 2. Run the program and observe the results in Table 12.2. Table 12.1 contains pairwise Pearson correlations between each of the three variables listed in the VAR statement. For example, the correlation between AGE; TIME1 is r=0.50088, and the p-value associated with the test of $H_0$: $\rho$ is 0 is p=0.0002.

## TABLE 12.2 Output from PROC CORR

| Pearson Correlation Coefficients, N = 50 | |
| Prob > |r| under H0: Rho=0 | |
|---|---|---|
| AGE | TIME1 | TIME2 |
| Age on Jan 1, 2000 | 1.00000 0.50088 0.38082 | |
| | 0.0002 0.0064 | | |
| TIME1 | 0.50088 1.00000 0.76396 | | |
| Baseline | 0.0002 <.0001 | | |
| TIME2 | 0.38082 0.76396 1.00000 | | |
| 6 Months | 0.0064 <.0001 | | |

(continued)

(continued)

- 3. If normality is questionable, you may want to request that the rank correlations (Spearman) be calculated (either by themselves or in combination with the Pearson correlations). Use the following PROC CORR statement to request both Pearson and Spearman correlations:

```
PROC CORR DATA="C:\SASDATA\SOMEDATA" PEARSON SPEARMAN;
```

Rerun the program and observe that a second table is the output containing Spearman and the associated $p$-values.

- 4. To simplify the output by suppressing the $p$-values and descriptive univariate statistics, change the PROC CORR statement to

```
PROC CORR DATA="C:\SASDATA\SOMEDATA"
PEARSON SPEARMAN NOPROB NOSIMPLE;
```

Rerun the program and observe the output.

## 12.1.3 Producing a Matrix of Scatterplots

As indicated earlier, it is important to examine a scatterplot of the relationship between two variables to determine the nature of the relationship (e.g., is it linear?). Use of the ODS GRAPHICS mode provides a method for displaying a matrix of the scatterplots associated with correlation estimates. This is illustrated in the following Hands-on Example.

> HANDS-ON EXAMPLE
This example illustrates how to create a matrix of scatterplots.

- 1. Open the program file ACORR2.SAS.

```
PROC CORR DATA="C:\SASDATA\SOMEDATA" PLOTS=MATRIX;
VAR TIME1 TIME;
TITLE 'Example correlations using PROC CORR';
RUN;
```

Note the option PLOTS=MATRIX. This option tells PROC CORR to include a graph that is a matrix of correlations in the output.

- 2. Run the program and observe the matrix of scatterplots illustrated in Figure 12.1. Note two scatterplots are produced for each pair of variables, so you need to examine only the upper or lower half of the table.

- 3. To add more information to the plot, change the PLOTS statement to
