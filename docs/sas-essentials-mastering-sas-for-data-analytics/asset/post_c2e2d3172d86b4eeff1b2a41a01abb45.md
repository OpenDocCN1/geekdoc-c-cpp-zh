
# CORRELATION ANALYSIS USING PROC CORR

## Scatter plot matrix

![](img/6113440fee6085d6edba5f406f541c12_298_0.png)

Figure 12.1 Matrix of scatterplots

```
PLOTS=MATRIX (HISTOGRAM) ;
```

Resubmit the code and observe the results (see Figure 12.2). This time, a histogram is displayed for each variable on the horizontal axis to show the distribution of the data for that variable.

- To look at scatterplots in more detail, change the PLOTS statement to

```
PLOTS=SCATTER;
```

Resubmit the code and observe the results (see Figure 12.3). This option produces a scatterplot for each pair of variables. It also displays a 95% prediction ellipse. A number of other suboptions are available for the PLOTS= option (see SAS documentation for more information).

(continued)

(continued)

| AGE | Scatter plot matrix |
|---|---|
| | TIME1 TIME2 |
| TIME1 | | |
| TIME2 | | |

**Figure 12.2** Scatterplots with histogram. Scatter plot with 95% prediction ellipse.

| Baseline | 24 Observations 50 Correlation 0.5009 |
|---|---|
| 22 | |
| 20 | |
| 18 | |
| Age on Jan 1, 2000: 5.0 7.5 10.0 12.5 15.0 |

**Figure 12.3** Scatterplots with prediction ellipse.

## 12.1.4 Calculating Correlations Using the WITH Statement

In the following Hands-on Example, all pairwise correlations were calculated from the list of variables. At times you may want to produce a list of correlations of one or more variables (possibly outcome variables) with several other variables. Use the WITH statement to produce the abbreviated list of correlations, as illustrated in the following Hands-on Example.

## HANDS-ON EXAMPLE

This example illustrates how to calculate correlations using a WITH statement.

- 1. Open the program file ACCOR3.SAS.

```
PROC CORR DATA="C:\SASDATA\SOMEDATA"
  VAR TIME1-TIME4;
  WITH AGE;
TITLE "Example correlation calculations using a WITH statement"
RUN;
```

Note that the VAR statement contains TIME1-TIME4, and a WITH statement is included that requests correlations between AGE and the four variables in the VAR statement.

- 2. Run this example and observe the output given in Table 12.3. Note that the output includes only correlations between AGE and the other variables.

- 3. Note that a table of simple statistics was included in the output. Put the option NOSIMPLE as an option in the PROC CORR statement (before the semicolon). Resubmit the program and observe the difference.

- 4. Add the option PLOTS=MATRIX to the PROC CORR statement. Resubmit the program and observe that a single row of scatterplot matrices are displayed.

## Table 12.3 Correlations Using a WITH Statement

| | TIME1 | TIME2 | TIME3 | TIME4 |
|---|---|---|---|---|
| Pearson Correlation Coefficients, N = 50 | | | | |
| Prob > |r| under H0: Rho=0 | | | | |
| AGE | 0.50088 | 0.38082 | 0.44952 | 0.48846 |
| Age on Jan 1, 2000 | 0.0002 | 0.0064 | 0.0011 | 0.0003 |

## 12.2 SIMPLE LINEAR REGRESSION

Simple regression is used to predict the value of a dependent variable from the value of an independent variable. For example, in a study of factory workers, you could use simple linear regression to predict a pulmonary measure, forced vital capacity (FVC), from asbestos exposure (ABS). That is, you could determine whether increased exposure to asbestos is

## CHAPTER 12: CORRELATION AND REGRESSION

predictive of diminished FVC. The following SAS PROC REG code produces the simple linear regression equation for this analysis:

```
PROC REG;
MODEL FVC=ASB;
RUN;
```

Note that the MODEL statement is used to tell SAS which variables to use in the analysis. As in the ANOVA procedure, which will be discussed in Chapter 13, the MODEL statement has the following form:

```
MODEL dependentvar = independentvar;
```

where the dependent variable (dependentvar) is the measure you are trying to predict and the independent variable (independentvar) is your predictor.

### 12.2.1 The Simple Linear Regression Model

The regression line that SAS calculates from the data is an estimate of a theoretical line describing the relationship between the independent variable (X) and the dependent variable (Y). The theoretical line is

```
Y = α + \betaX + ε
```

where $a$ is the $y$-intercept, $\beta$ the slope, and $\epsilon$ an error term that is normally distributed with zero mean and constant variance. It should be noted that $b=0$ indicates that there is no linear relationship between $X$ and $Y$. A simple linear regression analysis is used to develop an equation (a linear regression) for predicting the dependent variable given a value ($x$) of the independent variable. The regression line calculated by SAS is given

```
Y = a + bx
```

where $a$ and $b$ are the least squares estimates of $a$ and $b$. The null hypothesis states that there is no linear relationship between $X$ and $Y$. Because $\beta=0$ indicates there is no linear relationship between $X$ and $Y$, a low $p$-value for slope (say, $<0.05$) indicates significant evidence to conclude that the slope is not zero ($H_1: \beta \neq 0$) for this analysis.

### 12.2.2 Using SAS for Simple Linear Regression

The general syntax for PROC REG is as follows:

```
PROC REG <options>;
<statements>;
```

Table 12.4 Common Options for PROC REG

| Option | Explanation |
|---|---|
| DATA = datame | Specifies which data set to use |
| SIMPLE | Displays descriptive statistics |
| CORR | Displays a correlation matrix for variables |
| PLOTS=option | Requests graphs. Otherwise, several graphs are produced |
| ALPHA=p | Sets significance levels for confidence and prediction intervals |
| NONE | Suppresses output when you want to capture results but not display them |
| NOPINT | Suppresses output |
| WHERE | Filters the data |
| FORMAT, | Applies formats to variables |
| COOKD, LCL, UCL, LCLM, UCLM, | See SAS documentation for others |
| RESIDUAL | Creates the YHAT for residual values |

The MODEL statement in PROC REG is used to specify which variable to be predicted (dependentvar) from the predictor (independentvar). For example,

```
MODEL TASK=CREATE;
```

indicates that you want to predict TASK (the dependent variable).

## HANDS-ON EXAMPLE

In example, a random sample of 14 elementary school students is selected from a school, and each student is measured on a new testing instrument and on a creativity score (X) by a task score (Y) standard instrument. The task score is the mean time taken to perform several hand–eye coordination tasks. Because administering the creativity test is much cheaper, the researchers want to know if the CREATE score is a good substitute for the more expensive TASK score (i.e., whether the TASK score can be well predicted by the CREATE score).

- 1. Open the program file AREG1.SAS.

```
DATA ART;
INPUT SUBJECT $ CREATE TASK;
DATALINES;
AE 28 4.5
FR 35 3.9
HT 37 3.9
IO 50 6.1
DP 69 4.3
YR 84 8.8
QD 40 2.1
SW 65 5.5
DF 29 5.7
ER 42 3.0
RR 51 7.1
TG 45 7.3
EF 31 3.3
TJ 40 5.2
;
```

![](img/6113440fee6085d6edba5f406f541c12_303_0.png)

**Figure 12.4** The SAS statement
