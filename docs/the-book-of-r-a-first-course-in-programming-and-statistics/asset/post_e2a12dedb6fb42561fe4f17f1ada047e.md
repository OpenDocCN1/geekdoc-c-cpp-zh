
| Initial height | Distance |
|---|---|
| 1000 | 573 |
| 800 | 534 |
| 600 | 495 |
| 450 | 451 |
| 300 | 395 |
| 200 | 337 |
| 100 | 253 |

- a. Create a data frame in R based on this table and plot the data points with distance on the y-axis.

- b. Galileo believed there was a quadratic relationship between initial height and the distance traveled.
    - i. Fit an order 2 polynomial in height, and the distance as the response.
    - ii. Fit a cubic (order 3) and a quartic (order 4) model for these data. What do they tell you about the nature of the relationship?

- c. Based on your models from (b), choose the one that you think best represents the data and plot the fitted line on the raw data. Add 90 percent confidence bands for mean distance traveled to the plot.

The R package faraway contains a large number of sets that accompany a linear regression textbook by Faraway (2005). Install the package and then call `library(faraway)` to load it. One of the data sets is trees, which provides data on the dimensions of felled trees of a certain type (see, for example, Atkinson, 1985).

- d. Access the data at the prompt and plot volume against girth (the girth along the x-axis).

- e. Fit two models with Volume as the response: one quadratic model in Girth and the other on log transformations of both Volume and Girth. Write down the model equations for each and comment on the similarity (or difference) of the fits in terms of the coefficient of determination and the omnibus F-test.

- f. Use predict to add lines to the plot from (e). Use different lines; add a corresponding legend. Also include 95 percent prediction intervals, with line matching those of the fitted values (note that for the model that log transformation of the response and the predictor, any returned values from predict will be themselves on the log scale; you have to back-transform these to the original scale using exp before the lines for that model can be superimposed. Comment on the respective fits and their estimated prediction intervals.

Lastly, turn your attention back to the mtcars data frame.

- g. Fit and summarize a multiple linear regression model to determine MPG from horsepower, weight, and displacement.

- h. In the spirit of Henderson and Velleman (1981), I use to refer to the model in (g) in terms of GPM = 1/MPG. Which model explains a greater amount of variation in the response?

## 21.5 Interactive Terms

So far, you've looked only at the joint main effects of how predictors affect the outcome variable (and one-to-one transformations thereof). Now you'll look at interactions between covariates. An interactive effect before predictors is an additional change to the response that occurs at particular combinations of the predictors. In other words, an interactive effect is present if, for a given covariate profile, the values of the predictors are such that you produce an effect that augments the stand-alone main effects associated with those predictors.

### 21.5.1 Concept and Motivation

Diagrams as found in Figure 21-7 are often used to help explain the concept of interactive effects. These diagrams show your mean response value, ŷ, on the vertical axis, as usual, and a predictor value for the variable x1 on the horizontal axis. They also show a binary categorical variable x2, which can be zero or one. These hypothetical variables are labeled as in the images.

![](img/b2cfc85cbb129f60fe595a2bae074fe4_547_0.png)

The left diagram shows the limit of the models we've considered so far in this chapter—that both $x_1$ and $x_2$ affect $\hat{y}$ independently of each other. The right diagram, clearly shows that the effect of $x_1$ on $\hat{y}$ completely depending on the value of $x_2$. On the left, only main effects of $x_1$ and $x_2$ are needed to determine $\hat{y}$; on the right, main effects and an interactive effect between $x_1$ and $x_2$ are present.

When estimating regression models, you always have to accompany interactions with the main effects of the relevant predictors, for reasons of interpretability. Since interactions are themselves best understood as an augmentation of the main effects, it makes no sense to remove the latter and leave in the former.

For a good example of an interaction, think about pharmacology. Interactive effects are relatively common, which is why health professionals often ask about other medicines you might be taking. Consider statins—drugs commonly used to reduce cholesterol. Users of statins are told to avoid grapefruit juice because it contains natural chemical compounds that inhibit the efficacy of the enzyme responsible for the correct metabolism of the drug. If an individual is taking and not consuming grapefruit, you would expect a negative relationship between cholesterol level and statistic (think about "statin use" as a continuous or a categorical dosage variable)—as statistic use increases or otherwise, cholesterol level decreases. On the other hand, for an individual with statins who is consuming grapefruit, the nature of the relationship between cholesterol level and statistic use could easily be different—weakened negative, neutral, or even positive. If so, since the effect of the statins on cholesterol changes to the value of another variable—whether or not grapefruit is consumed—this would be considered an interaction between those two predictors.

Interactions can occur between categorical variables, numeric variables, or both. Most common to find interactions between exactly two predictors—which is what you will focus on in Sections 21.5.2 to 21.5.4. Three-way and higher-order interactive effects are technically possible but less common, partly because they are difficult to interpret in a real-world context. You could consider an example of these in Section 21.5.5.

## 21.5.2 One Categorical, One Continuous

Generally, a two-way interaction between a categorical and a continuous predictor should be understood as affecting a change in the slope of the continuous predictor with respect to the nonreference levels of the categorical predictor. In the presence of a term for the continuous variable, a categorical variable with $k$ levels will have $k-1$ main terms, so there will be a further $k-1$ interactive terms between all the alternative levels of the categorical variable and the continuous variable.

The different slopes for $x_1$ by category of $x_2$ for $\hat{y}$ are seen clearly on the right of Figure 21-7. In such a situation, in addition to the main effects for $x_1$ and $x_2$, there would be one interactive term needed to change the slope of $x_1$ by $x_2$ for $x_2 = 1$. This defines the slope of $x_1$ by $x_2$ for $x_2 = 1$. For an example, let's access the diabetes dataset (405 African Americans) detailing cholesterol level (chol-continuous), and body frame (frame-categorical with 3 levels: "small" as the reference level, "medium", and "large"). Total cholesterol is related to both age and body frame. It seems logical to expect that it makes sense to also consider the possibility that the effect of age on cholesterol is different for individuals of body frames. To investigate, let's fit the multiple linear regression and include a two-way interaction between the two variables. In the call to lm, you specify the main effects first, as usual, and then interactive effect of two predictors using a colon (:) between them.

```
R> fit <- lm(chol~age+frame+age:frame,data=diabetes)
R> summary(fit)
```
