
# CHAPTER 10: ANALYZING COUNTS AND TABLES

| Italian | 33 |
| Chinese | 38 |
| ; | |

Using this as a starting point, perform a goodness-of-fit test using PROC FREQ. Hint: Use the Hands-on-Example discussed earlier in this chapter as a template for the analysis. Use the statements:

```
PROC FREQ ORDER=DATA; WEIGHT NUMBER;
```

and

```
TESTP=(4,.2,.2,.2);
```

in your SAS program to perform the appropriate goodness-of-fit test.

## 10.2 Perform a contingency table analysis.

Historical data used to research the relationship between smoking and cancer yields the following data.

| Smoking Habit/Cancer | Cancer | No Cancer | Total |
| :--- | :--- | :--- | :--- |
| None to slight | 56 | 956 | 1012 |
| Moderate to excessive | 269 | 1646 | 1915 |
| Total | 325 | 2602 | 2927 |

- a. Using the contingency table example as a template for your SAS program (PROC FREQ), perform a chi-square test on these data using PROC FREQ and state your conclusions.
- b. What is the hypothesis tested in this example?

## 10.3 Going deeper: calculate risk.

- a. Using the code in FREQ, change the TABLES statement to
```
TABLES cancer /RISK;
```
Run the program and observe that OR = 1.36 representing the risk of getting cancer when using 1 versus 2.

- b. Change the table to calculate the risk of 2 versus 1. By default, SAS orders them in numerical order (1 and 2). To change this, create a formatted value for cancer and use the ORDER=FORMAT option to put the categories in the desired order. Enter this code at the top of the program:

```
PROC FORMAT;
VALUE $FIN "1"="YES" "2"="NO";
```

Moreover, change the PROC FREQ statement to read and add a FORMAT statement after the TITLE statement and before RUN.

```
RUN
```

Run the revised program. The order of cancer should be changed according to the formatted values, and OR reported is the reciprocal of 1.36, or 0.74.

- c. What does OR=0.74 mean?

## 10.4 Going deeper: calculate kappa.

Suppose a researcher is examining the reliability of a method for interpreting X-rays displayed on photographic film. Two raters examine a series of images and classify the severity of a fracture using a 1, 2, 3 system with 1 indicating a minor fracture and 3 indicating a severe fracture. The data are:

| | Rater 1 | Rater 2 |
| :--- | :--- | :--- |
| 1 | 7 | 7 |
| 2 | 9 | 5 |
| 3 | 4 | 8 |

- a. Which is the appropriate kappa statistic to use for this analysis (kappa or weighted kappa)? Do the raters seem to be in agreement? (Assess agreement visually before calculating any statistics.)
- b. Write a SAS program to read the data and calculate the appropriate kappa statistic.
- c. What is the value of the kappa statistic? According to the Landis and Koch criteria, how would you characterize the strength of this result?

# 11 COMPARING MEANS USING T-TESTS

### LEARNING OBJECTIVES

- To understand the use of the one-sample t-test using PROC UNIVARIATE and PROC TTEST
- To understand the use of the two-sample t-test using PROC TTEST
- To understand the use of the paired t-test using PROC MEANS AND PROC TTEST

Experiments where outcome measures are quantitative variables are often analyzed by comparing means. The Student's t-test is the most commonly used statistical test for comparing two means or for comparing an observed mean with a known value. If more than two groups are observed, an analysis of variance (ANOVA) is used to compare means across groups (discussed in Chapter 13).

## 11.1 PERFORMING ONE-SAMPLE T-TEST

A one-sample t-test is often used to compare an observed mean with a known or "gold standard" value. For example, in a quality control setting, you may be interested in comparing a sample of data to an expected outcome, such as the observed calories of liquid in baby formula against the claim on the label. The purpose of the one-sample t-test, in this case, is to determine if there is enough evidence to dispute the claim. In general, for a one-sample t-test you obtain a random sample from some population and compare the observed mean to some fixed value. The typical hypotheses for a one-sample t-test are as follows:

$H_0: \mu = \mu_0$: The population mean is equal to a hypothesized value, $\mu_0$.
$H_1: \mu \neq \mu_0$: The population mean is not equal to $\mu_0$.

The key assumption underlying the one-sample t-test is that the population from which the random sample is selected is non-normal. If the data are non-normal, then nonparametric tests such as the sign test and the signed rank test are available (Chapter 15). However, because of the central limit theorem, whenever the sample size is sufficiently large, the distribution of the sample mean is approximately normal even when the population is non-normal. A variety of rules of thumb have been recommended to help you determine whether to go and trust the results of a one-sample t-test when your data are non-normal. The following are general guidelines (see Moore, McCabe, and Craig, 2014).

* Small sample size ($N < 15$): You should not use the one-sample t-test if the data are clearly skewed or have outliers present.
* Moderate sample size ($N > 15$): the one-sample t-test can be safely used except when there are outliers.
* Large sample size ($N > 40$): the one-sample t-test can be safely used without regard to skewness or outliers.

## 11.1 Performing the One-Sample t-Test

In SAS there are at least two ways to perform a one-sample t-test. Using PROC VARIATE, you can specify the value of $\mu_0$ for the test.

```
PROC VARIATE DATA=ONESAMPLE;
VAR LENGTH;
RUN;
```

The second method is to use PROC TTEST. For the one-sample t-test of the hypothesis that $\mu_0 = 4$, the following SAS code is:

```
PROC TTEST DATA=ONESAMPLE;
VAR LENGTH;
RUN;
```

### HANDS-ON EXAMPLE

In this example, you will learn how to perform a one-sample t-test using SAS commands. The component is the most important. To test the manufacturer's claim, the following SAS code is used:

```
DATA ONESAMPLE;
INPUT LENGTH @@
DATALINES;
4 3.95
4 4.01
4 3.95
4 4.00
4 3.98
4 4.02
4 3.99
4 4.00
4 3.97
4 4.01
4 3.98
4 4.02
4 3.99
4 4.00
4 3.96
4 4.01
;
```

Wait, a researcher is examining the reliability of a method for interpreting X-rays displayed on photographic film. Two raters examine a series of images and classify the severity of a fracture using a 1, 2, 3 system with 1 indicating a minor fracture and 3 indicating a severe fracture. The data are:

| | Rater 1 | Rater 2 |
| :--- | :--- | :--- |
| 1 | 7 | 7 |
| 2 | 9 | 5 |
| 3 | 4 | 8 |

- a. Which is the appropriate kappa statistic to use for this analysis (kappa or weighted kappa)? Do the raters seem to be in agreement? (Assess agreement visually before calculating any statistics.)
- b. Write a SAS program to read the data and calculate the appropriate kappa statistic.
- c. What is the value of the kappa statistic? According to the Landis and Koch criteria, how would you characterize the strength of this result?

### 11.1 Performing the One-Sample t-Test (continued)

| Tests for Location: PROC UNIVATE |
| :--- | :--- |
| Test | Statistic | Pr |
| Student's t | -1.41 | 0.1759 |
| Sign | -1.50 | 0.6291 |
| Signed Rank | -1.40 | 0.2240 |

| Tests for Location: PROC TTEST |
| :--- | :--- |
| Test | Statistic | Pr |
| Student's t | -1.41 | 0.1759 |
| Sign | -1.50 | 0.6291 |
| Signed Rank | -1.40 | 0.2240 |

ODS GRAPHICS ON;

> Note that the t-test is performed twice: once using PROC VARIATE and again using PROC TTEST.

> Note that depending on version of SAS you are running (older versions), you may need to add the statement to get the graphs mentioned in this example.
