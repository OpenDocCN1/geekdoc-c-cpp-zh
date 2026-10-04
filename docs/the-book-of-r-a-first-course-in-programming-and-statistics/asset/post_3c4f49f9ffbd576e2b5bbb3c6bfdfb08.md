
Suppose $X$ is a variable that can take any of the $k = 4$ values 1, 2, 3, or 4, and you've made six observations of this variable: 1, 2, 2, 1, 4, 3. Table 20-1 shows these observations and their dummy-coded equivalents $X_{(1)}, X_{(2)}, X_{(3)},$ and $X_{(4)}$.

## Table 20-1: Illustrative Example of Dummy Coding for Six Observations of a Categorical Variable with $k = 4$ Groups

| X | $X_{(1)}$ | $X_{(2)}$ | $X_{(3)}$ | $X_{(4)}$ |
|---|---|---|---|---|
| 1 | 1 | 0 | 0 | 0 |
| 2 | 0 | 1 | 0 | 0 |
| 2 | 0 | 1 | 0 | 0 |
| 1 | 1 | 0 | 0 | 0 |
| 4 | 0 | 0 | 0 | 1 |
| 3 | 0 | 0 | 1 | 0 |

In fitting the subsequent model, you usually use $k - 1$ of the dummy binary variables—one of the variables acts as a *reference* or *baseline* level, and it's incorporated into the overall intercept of the model. In practice, you would end up with an estimated model like:

$\hat{y} = \beta_0 + \beta_1X_{(2)} + \beta_2X_{(3)} + \dots + \beta_{k-1}X_{(k)}$ \quad (20.8)

assuming $\beta_0$ is the reference level. As you can see, in addition to the overall intercept term $\hat{\beta}_0$, you have $k-1$ estimated intercept terms that modify the baseline coefficient $\hat{\beta}_0$, depending on which of the original categories an observation takes on. For example, in light of the code imposed in (20.8), if an observation has $X_{(3)} = 1$ and all other binary values are zero (so that observation would have had a value of $X = 3$ for the original category), the predicted mean value of the response would be $\hat{y} = \hat{\beta}_0 + \hat{\beta}_2$. On the other hand, because the reference level is defined for all the binary variables, it implies the observation originally had $X = 1$, and the prediction would be simply $\hat{y} = \hat{\beta}_0$.

The reason it's necessary to dummy code for categorical variables of this nature is that, in general, categories cannot be related to each other in the same numeric sense as continuous variables. It's often not appropriate to think that an observation in category 4 is "twice as" as in category 2, which is what the estimation methods would assume. Binary/absence variables are valid, and can be easily incorporated into the modeling framework. Choosing the reference level is generally of secondary importance—the specific values of the estimated coefficients will change accordingly, but any overall interpretations you make based on the fitted model will be the same regardless.

NOTE Implementing dummy-coding approach is technically a form of multiple regression since you're now including several binary variables in the model. It's important, however, to be aware of the somewhat artificial nature of dummy coding—you should still think of the multiple coefficients as representing a single categorical variable since the binary variables $X_{(1)},\dots, X_{(K)}$ are not independent of one another. This is why I've chosen to define these models in this chapter; multiple regression will be formally discussed in Chapter 21.

## Regression Model of Multilevel Variables

R works with categorical predictors in this way quite simple since it automatically dummy codes for any explanatory variable when you call lm. There are two things you should check before fitting your model, though.

- 1. The categorical variable of interest should be stored as a (formally unordered) factor.
- 2. You should check that you're happy with the category assigned as the reference level (for interpretive purposes—see Section 20.5.3).

You must also be happy with the validity of the familiar assumptions of normality and independence of $\epsilon$.
To demonstrate all these definitions and ideas, let's return to the student data from the MASS package and keep "student height" as the response variable of interest. Among the data is the data Smoke. This variable describes the kind of smoker each student reports themselves as, defined by frequency and split into four categories: "heavy", "never", "occasional", and "regular."

```
R is.factor(survey$Smoke)
[1] TRUE
R table(survey$Smoke)
```

```
Heavy Never Occas
11 189 19 17
R levels(survey$Smoke)
[1] "Heavy" "Never" "Occas" "Regul"
```

Here, the result from is.factor(survey$Smoke) indicates that you do indeed have a factor vector at hand, the call to table yields the number of students in each of the four categories, and as per Chapter 5, you can explicitly request the levels attribute of any factor.
Let's ask whether there statistical evidence to support a difference in mean height according to smoking frequency. You can create a set of boxplots of these data with the following two lines; Figure 20-5 shows the result.

```
boxplot(Height~Smoke,data=survey)
R points(1:4,tapply(survey$Height,survey$Smoke,mean,na.rm=TRUE),pch=4)
```

![](img/b2cfc85cbb129f60fe595a2bae074fe4_508_0.png)

Note from earlier R output that unless not explicitly defined at creation, the levels of a factor appearing in alphabetical order by default—is the case for Smoke—and R will automatically select the first one (as shown in the output of a call to levels) as the reference level when that factor is used as a predictor in subsequent model fitting. Fitting the linear model in using lm, you can see from a subsequent call to summary that indeed the first level of Smoke, for "heavy", has been used as the reference:

```
R survfit3 <- lm(Height~Smoke,data=survey)
R> summary(survfit3)
```

Call:
lm(formula = Height ~ Smoke, data = survey)

Residuals:
Min 1Q Median 3Q Max
-25.02 -6.82 -1.64 8.18 28.18

Coefficients:
Estimate Std. Error t value Pr(>|t|)
(Intercept) 173.7720 3.1028 56.005 <2e-16 ***
SmokeNever -1.9520 3.1933 -0.611 0.542
SmokeOccas -0.7433 3.9553 -0.188 0.851
SmokeRegul 3.6451 4.0625 0.897 0.371

Signif. codes: 0 *** 0.001 ** 0.01 * 0.05 ' ' 0.1 ' ' 1

Residual standard error: 9.812 on 205 degrees of freedom (28 observations deleted due to missingness)

Multiple R-squared: 0.02153, Adjusted R-squared: 0.007214
F-statistic: 1.504 on 3 and 205 DF, p-value: 0.2147

As outlined in Equation (20.8), you get estimates of coefficients corresponding to the dummy binary variables for three of the four possible categories in this example—the three nonreference values. The observation in the reference category Heavy is represented solely by $\beta_0$, designated first the overall (Intercept), but the other coefficients providing the effects associated with an observation in one of the other categories.

## Predictions from a Multilevel Categorical Variable

You find estimates through prediction, as usual.

```
R one.of.each <- factor(levels(survey$Smoke))
R one.of.each
[1] Heavy Never Occas Regul
Levels: Heavy Never Occas Regul
R predict(survfit3,newdata=data.frame(Smoke=one.of.each),
interval="confidence",level=0.95)
fit      lr      upr
1 173.770 167.645 179.889
2 171.820 170.339 173.301
3 173.028 172.194 177.8651
4 177.417 172.2469 182.5874
```

Here, I created the object one.of.each for illustrative purposes; it represents one observation in each of the four categories, stored as an object matching the class (and levels) of the original Smoke data. A student in the Occas category, for example, is predicted to have a mean height of 173.772 – 0.7433 = 173.0287.

The output from the model summary earlier, however, shows that none of the dummy binary variables are considered significant from zero (because the p-values are too large). The results indicate, as you might have suspected, that there's no evidence smoking frequency (or more specifically, having a smoking frequency that's different from the reference level) affects mean height based on this sample of individuals. As is common, the baseline coefficient $\beta_0$ is significant—but only that the overall intercept isn't zero. (Because your response variable is a measurement of height and clearly not centered near 0, that makes sense.) The confidence intervals are calculated in the t-based fashion.

The small R-squared reinforces this conclusion, indicating that barely any of the variation in the response can be explained by changing the category of smoking frequency. Furthermore, the overall F-test p-value is large rather around 0.215, suggesting an overall nonsignificant of the predictor for the response; you'll look at this in more detail in a moment in Section 20.5.5 and later on in Section 21.3.5.
