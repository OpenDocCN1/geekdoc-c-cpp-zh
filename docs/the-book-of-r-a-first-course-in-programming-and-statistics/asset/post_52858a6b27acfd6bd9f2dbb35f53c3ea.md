
![](img/b2cfc85cbb129f60fe595a2bae074fe4_482_0.png)

In R, a Kruskal-Wallis test is performed using kruskal.test.

```
kruskal.test(Age~Smoke,data=survey)
```

# Kruskal-Wallis rank sum test

data: Age by Smoke
kruskal-Wallis chi-squared = 3.9262, df = 3, p-value = 0.2695

The syntax for this test is the same as for aov. as you might suspect from Figure 19-3, the large p-value suggests there's no evidence against the null hypothesis that states that the medians are all equal. In other words, there doesn't seem to be an overall age difference between the students in the four smoking categories.

# Exercise 19.2

- Bring up the quakes data frame again, which describes the locations, magnitudes, depths, and number of observation stations detected 10 seismic events off the coast of Fiji.
- a. Use cut (section 4.3.3) to create a new factor vector defining the depths of each event according to the following three categories: (0,200], (200,400], and (400,680).
- b. Decide whether the one-way ANOVA or a Kruskal-Wallis test is more appropriate to use compare the distributions of the number of detecting stations, split according to the three categories in (a).
- c. Perform your choice of test in (b) (assume a $\alpha=0.01$ level of significance) and conclude.

Load the MASS package with a call to library("MASS") if you haven't already done so in the current R session. This package includes the ready-to-use Cars93 data frame, which contains detailed data on 93 cars for sale in the United States 1993 (Lock, 1993; Venables and Ripley, 2002).

- d. Use aggregate to compute the mean length of 93 cars, by two categorical variables: AirBags (type of airbags available—levels are Driver & Passenger, Driver only, and None), and Man.trans.avail (whether the car comes in a manual transmission—levels are Yes and No).
- e. Produce an interaction plot using the results in (d). Does appear to be an interactive effect of AirBags with Man.trans.avail on the mean length of these cars (if you consider only these variables)?
- f. Fit a full two-way ANOVA model for the mean lengths according to the two grouping variables (assume satisfaction of all relevant assumptions). Is the interactive effect statistically significant? Is there evidence of any main effects?

# Important Code in this Chapter

| Function/operator | Brief description | First occurrence |
|---|---|---|
| aov | Produce ANOVA table | Section 19.1.3, p. 440 |
| aggregate | Stacked statistics by factor | Section 19.2.1, p. 444 |
| interaction.plot | Two-factor interaction plot | Section 19.2.2, p. 446 |
| kruskal.test | Kruskal-Wallis test | Section 19.3, p. 449 |

# 20
# SIMPLE LINEAR REGRESSION

![](img/b2cfc85cbb129f60fe595a2bae074fe4_484_0.png)

Though straightforward comparative tests of individual statistics are useful in their own right, you'll often want to learn more from your data. In this chapter, you'll look at linear regression models: a suite of methods used to evaluate precisely how variables relate to each other.

Simple linear regression models describe the effect that a particular variable, called the explanatory variable, might have on the value of a continuous outcome variable, called the response variable. The explanatory variable may be continuous, discrete, or categorical, but to introduce the key concepts, I'll concentrate on continuous explanatory variables for the first several sections in this chapter. Then, I'll cover how the representation of the model changes if the explanatory variable is categorical.

## 20.1 An Example of a Linear Relationship

As an example to start with, let's continue with the data used in Section 19.3 and look at the student survey data (the survey data frame in the package MASS) a little more closely. If you haven't already done so, with the required package loaded (call library("MASS")), you can read the help file ?survey for details on the variables presented.

Plot the student heights on the y-axis and their handpans (of their writing hand) on the x-axis.

```
R> plot(survey$Height,survey$Wr.Hnd,xlab="Writing handspan (cm)",nyylab="Height (cm)")
```

Figure 20-1 shows the result.

![](img/b2cfc85cbb129f60fe595a2bae074fe4_485_0.png)

Figure 20-1: Ascatterplot of height against writing handspan for a sample of first-year statistics students

Note that the call to use formula notation (also referred as symbolic notation) to specify "height on handspan." You can produce the same scatterplot using the coordinate vector form of (x, y), that is, plot(survey$Wr.Hnd,survey$Height,...), but I'm using the symbolic notation because it nicely reflects how you'll fit the linear model in a moment.

As you expect, there's a positive association between a student's handspan and their height. That relationship appears to be linear in nature. To assess the strength of the linear relationship (refer to Section 13.2.5), you can find the estimated correlation coefficient.

```
R> cor(survey$Wr.Hnd,survey$Height,use="complete.obs")n[1] 0.6009909
```

Though there are 237 records in the data frame, the plot doesn't actually show 237 points. This is because there are missing observations (coded NA; see Section 6.1.3). By default, R removes any "incomplete" pairs when producing a plot like this. To find out how many observations have been deleted, you can use the short-form logical operator | (Section 4.1.3) in conjunction with is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) and is.na (Section 6.1.3) to the. there are 29.

```
R> is.na(survey$Heightnd)








 29
```

## 2.2 General Concepts

The purpose of linear regression is to use your data to estimate the parameters, yielding the estimates $\hat{8eta}_0$ and $\hat{8eta}_1$; this is referred to as *fitting* the linear model. In this,, the data contains $n$ pairs of observations. The fitted model of interest concerns the mean response, denoted $\hat{y}$, for a specific value of the predictor, $x$, and is written as follows:

```
$\hat{y} = \hat{8eta}_0 + \hat{8eta}_1x$
```

Sometimes, alternative notation such as $E[Y]$ or $E[Y|X=x]$ is used on the left side of (20.2) to emphasize that the model means (that is, the *expected value*) of the response. For compactness, simply use $\hat{y}$, as shown above.

Let your $n$ observed data pairs be denoted $x_i$ and $y_i$ for the predictor and response variables; $i = 1, \dots, n$. Then, the parameter estimates for the simple linear function

```
$\hat{8eta}_1 = \rho_{XY} \frac{s_Y}{s_X} \quad \hat{8eta}_0 = \hat{y} - \hat{8eta}_1\bar{x}$
```

where

+   - $\bar{x}$ and $\bar{y}$ are the sample means of the $x_is$ and $y_is$.
- $s_x$ and $s_y$ are the sample standard deviations of the $x_is$ and $y_is$.
- $\rho_{XY}$ is the estimate of correlation between $X$ and $Y$ based on the data (see Section 13.2.5).

### 2.2.1 Definition of the Model

The linear regression model states that the response $Y$ given $X$ is expressed as:

$Y = \beta_0 + \beta_1 X + \epsilon$

The validity of the conclusions you draw based on (20.1) is critically dependent on the assumptions made about $\epsilon$, which are:

- The $\epsilon$ is assumed to be normally distributed such that $\epsilon \sim N(0, \sigma^2)$.
- The variance of $\epsilon$, $\sigma^2$, is constant.

### 2.2.2 Estimating the Parameters

The goal is to use your data to estimate the regression parameters, yielding the estimates $\hat{\beta}_0$ and $\hat{\beta}_1$; this is referred to as *fitting* the linear model. In this case, the data contains $n$ pairs of observations. The fitted model of interest concerns the mean response, denoted $\hat{y}$, for a specific value of the predictor, $x$, and is written as follows:

```
$\hat{y} = \hat{\beta}_0 + \hat{\beta}_1x$
```

Sometimes, alternative notation such as $E[Y]$ or $E[Y|X=x]$ is used on the left side of (20.2) to emphasize that the model means (that is, the *expected value*) of the response. For compactness, simply use $\hat{y}$, as shown above.

## Parameters

- The Intercept, $\beta_0$, is interpreted as the expected value of the response when the predictor is zero.
- Generally, the slope, $\beta_1$, is the focus of interest. This is interpreted as the change in mean response for each one-unit increase in the predictor. When the slope is positive, the line increases from left to right (when the slope is negative, the line decreases from left to right). The more extreme the value of $\beta_1$ (away from zero), the steeper the line. This implies that the predictor has an effect on the response.

## Residual Assumptions

The validity of the conclusions you draw based on (20.1) is critically dependent on the assumptions made about $\epsilon$, which are:

- The $\epsilon$ is assumed to be normally distributed such that $\epsilon \sim N(0, \sigma^2)$.
- The variance of $\epsilon$, $\sigma^2$, is constant.
