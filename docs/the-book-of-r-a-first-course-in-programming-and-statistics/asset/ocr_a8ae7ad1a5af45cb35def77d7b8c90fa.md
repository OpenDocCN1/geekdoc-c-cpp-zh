(Section 4.1.3) in conjunction with is.na (Section 6.1.3) and which (Section 4.1.5). You then use length to discover there are 29 missing observation pairs.

```
R incomplete.obs <- which(is.na(survey$Height)|is.na(survey$Wr.Hnd))
R length(incomplete.obs)
[1] 29
```

NOTE Because there are NAs in the vectors supplied to the correlation coefficient function, you must also specify the optional argument use="complete.obs". This means that the calculated statistic takes into account only those observation pairs in the Wr.Hnd and Height vectors where neither element is NA. You can think of this as doing the same thing as na.tm=TRUE in univariate summary statistic functions such as mean and sd.

# 20.2 General Concepts

The purpose of a linear regression model is to come up with a function that estimates the mean of one variable given a particular value of another variable. These variables are known as the response variable (the "outcome" variable whose mean you are attempting to find) and the explanatory variable (the "predictor" variable whose value you already have).

In terms of the student survey example, you might ask something like "What's the expected height of a student if their handspan is 14.5 cm?" Here the response variable is the height, and the explanatory variable is the handspan.

# 20.2.1 Definition of the Model

Assume you're looking to determine the value of response variable Y given the value of an explanatory variable X. The simple linear regression model states that the value of a response is expressed as the following equation:

> $Y|X = \beta_0 + \beta_1 X + \epsilon$

On the left side of Equation (20.1), the notation Y|X reads as "the value of $Y$ conditional upon the value of $X$."

# Residual Assumptions

The validity of the conclusions you can draw based on the model in (20.1) is critically dependent on the assumptions made about $\epsilon$, which are defined as follows:

+   - The value of $\epsilon$ is assumed to be normally distributed such that $\epsilon \sim N(0, \sigma)$.
- $\epsilon$ is centered (that is, has a mean of) zero.
- The variance of $\epsilon$, $\sigma^2$, is constant.