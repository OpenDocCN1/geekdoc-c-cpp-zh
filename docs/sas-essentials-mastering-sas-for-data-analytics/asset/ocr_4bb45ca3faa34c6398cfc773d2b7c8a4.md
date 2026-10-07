# CHAPTER 12: CORRELATION AND REGRESSION

# 12.1.1 Correlation Analysis Basics

The correlation coefficient is a measure of the linear relationship between two quantitative variables measured on the same subject (entity). For example, you might study the relationship between height and weight for a sample of teenage boys. For two variables of interest, say X and Y, $ho$ measures the extent to which a scatterplot of the bivariate distribution of X and Y tends to fall along a line. The correlation $ho$ is a unitless quantity (i.e. it does not depend on the units of measurement) that ranges from -1 to +1 when $ho=-1$ and $ho=+1$ correspond to perfect negative and positive linear relationships, respectively and $ho=0$ indicates no linear relationship.

In practice, it is of interest to test the hypotheses:

+   $H_0: \rho = 0$: There is no linear relationship between the two variables.
$H_1: \rho \neq 0$: There is a linear relationship between the two variables.

The correlation coefficient $ho$ is typically estimated from data using the Pearson correlation coefficient, usually denoted as $r$. PROC CORR in SAS provides a test of the hypotheses designed to determine whether the estimated correlation, $r$, is significantly different from zero. This test assumes that the data represent a random sample from some bivariate normal distribution. If normality is not a good assumption, nonparametric estimates are available, the most popular of which Spearman's $ho$, which PROC CORR provides.

> To examine the nature of the relationship between two variables, it is always a good practice to look at scatterplots of the variables.

# 12.1.2 Using SAS PROC CORR for Correlation Analysis

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