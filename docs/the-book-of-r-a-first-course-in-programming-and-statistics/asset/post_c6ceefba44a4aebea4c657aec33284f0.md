
step. in this example, define scope as fullest model to be considered—set this to be the overly complex model with a four-way interaction among wt, hp, cyl, and disp (and relevant lower-order interactions and main effects, via the cross-factor operator), as well as main effects for am, gear, drat, vs, qc and carb. The two multilevel categorical variables, cyl and gear, are explicitly converted to factors to avoid them being treated as numeric (ref to Sec-20.5.4).

The potential for interactions in the final model will highlight an especially important (and convenient) feature of add, drop, and step. These functions reflect the hierarchy imposed by interactions and main effects. That is, for add (and step), an interactive term will not be provided in the current fitted model; similarly, for drop (and step), an active term or main effect will not be provided as an option unless relevant lower-order effects are already present unless relevant higher-order effects are already gone from the current fitted model.

The function itself returns a fitted model and by default provides a comprehensive report of each stage of selection. Let's call it now; for first reasons, some of the output has been signed out, so you're encouraged to print this up on your machine.

```
car.step <- step(car.null,scope=".+wt+hp=factor(cyl)=disp+am+factor(gear)=drat+vs+qc+carb)
```

Start: AIC=115.94
mpg ~ 1

| | Df of Sq | RSS | AIC | | |
|---|---|---|---|---|
| + wt | 1 | 847.73 | 278.32 | 73.217 |
| + disp | 1 | 808.89 | 317.16 | 77.397 |
| + factor(cyl) | 2 | 824.78 | 301.26 | 77.752 |
| + hp | 1 | 678.37 | 447.67 | 88.427 |
| + drat | 1 | 522.48 | 603.57 | 98.988 |
| + vs | 1 | 496.53 | 629.52 | 99.335 |
| + factor(gear) | 2 | 483.24 | 642.80 | 102.003 |
| + am | 1 | 405.15 | 720.90 | 103.672 |
| + carb | 1 | 341.78 | 784.27 | 106.369 |
| + qsec | 1 | 197.39 | 928.66 | 111.776 |
| <none> | | | | 1126.05 115.943 |

Step: AIC=73.22
mpg ~ +wt

| | Df of Sq | RSS | AIC | | |
|---|---|---|---|---|
| + factor(cyl) | 2 | 95.26 | 183.06 | 63.810 |
| + hp | 1 | 83.27 | 195.05 | 63.840 |
| + qsec | 1 | 82.86 | 195.46 | 63.908 |
| + vs | 1 | 54.23 | 224.09 | 68.283 |
| + carb | 1 | 44.60 | 233.72 | 69.628 |

![](img/b2cfc85cbb129f60fe595a2bae074fe4_576_0.png)

+ disp 1 31.64 246.68 71.356
+ factor(gear) 2 40.37 237.95 72.202
<none> 2 278.32 73.217
+ drat 1 9.08 269.24 74.156
+ am 1 0.00 278.32 75.217
- wt 1 847.73 1126.05 115.943

Step: AIC=63.81
mpg ~ wt + factor(cyl)

| Df Sum of Sq RSS AIC |
|---|---|---|---|
| + hp 1 22.281 160.78 61.657 |
| + wt:factor(cyl) 2 27.170 155.89 62.669 |
| <none> | 183.06 63.810 |
| + qsec 1 10.949 172.11 63.837 |
| + carb 1 9.244 173.81 64.152 |
| + vs 1 1.842 181.22 65.487 |
| + disp 1 0.110 182.95 65.791 |
| + am 1 0.090 182.97 65.794 |
| + drat 1 0.073 182.99 65.798 |
| + factor(gear) 2 6.682 176.38 66.620 |
| - factor(cyl) 2 95.263 278.32 73.217 |
| - wt 1 118.204 301.26 77.752 |

Step: AIC=61.66
mpg ~ wt + factor(cyl) + hp

--snip--

Step: AIC=55.9
mpg ~ wt + factor(cyl) + hp + wt:hp

--snip--

Step: AIC=52.8
mpg ~ wt + hp + wt:hp

--snip--

Step: AIC=52.57
mpg ~ wt + hp + qsec + wt:hp

| Df Sum of Sq RSS AIC |
|---|---|---|---|
| <none> | | 121.04 52.57 |
| - qsec 1 8.720 129.76 52.799 |
| + factor(gear) 2 9.482 111.56 53.962 |
| + am 1 1.939 119.10 54.056 |
| + carb 1 0.080 120.96 54.551 |
| + drat 1 0.012 121.03 54.570 |
| + vs 1 0.010 121.03 54.570 |
| + disp 1 0.008 121.03 54.571 |
| + factor(cyl) 2 0.164 120.88 56.529 |
| - wt:hp 1 0.651 186.06 64.331 |

Each block of output displays the current model fit, its AIC value, and a table showing the moves (either adding +, or doing <none>). The AIC value that would result from each move is listed, and these potential moves are ranked from smallest to largest value. As the algorithm proceeds, you see this creeping up the table. For example, in the first table, the value of AIC for intercept-only is 115.94. The biggest reduction in AIC would result from adding a effect for wt; that move, and the effect of subsequent moves is reassessed. Also note that the addition of the two-way interaction between wt and factor(cyl) is considered only at the third step, after the mean predictors have been added. That particular two-way interaction never enters again, because the main effect of hp is preferable to that step. In the fourth step, actually deleting the main effect for factor(cyl) reduces the AIC most, and so the tables for the sixth and seventh steps no longer include wt:hp. The sixth step shows that adding the main effect for qsec offers a minor reduction in the AIC, so this is done. The seventh table signals the end of the AIC because doing nothing offers the lowest AIC value and doing anything else would increase the AIC (shown through position). The final model is stored as the object; by summarizing, you'll note that almost 90 percent of the variation in the response is explained by weight, and their interaction, as well as the slightly curious main effect of qsec (which itself is not deemed significant).

```
R> summary(car.step)
```

```
Call:
lm(formula = mpg + hp + qsec + wt:hp, data = mtcars)
```

Residuals:
Min Median Max
-3.8243 -1.3980 0.0303 1.1582 4.3650

Coefficients:
Estimate Std. Error t value Pr(|t|)
(Intercept) 40.31040 7.67887 5.250 1.65e-05 ***

wt -8.681516 1.292525 -6.717 3.28e-07 ***
hp -0.106181 0.022623 -4.043 0.000395 ***
qsec 0.050163 0.036078 1.395
wt:hp 0.027791 0.007298 3.808 0.000733 ***

Signif. codes:
*** 0.001 ** 0.01 * .

Residual error: 2.117 on 27 degrees of freedom
Multiple R-squared: 0.8925, Adjusted R-squared: 0.8766
F-statistic: 56.05 on 4 and 27 DF, p-value: 1.094e-12

From this, it would be worthwhile to investigate this predictor further to establish validity of the fitted model (see Section 22.3), and perhaps to try transformations of the data (such as modeling MPG instead of MPG; see Section 21.3) to see whether this effect persists in subsequent runs of the stepwise algorithm. The algorithm illustrates the fact that the selection of the model wasn't based solely on the significance of predictor contribution but on a criterion-based aim for its own definition of parsimony.

The AIC is sometimes criticized for a tendency to err on the side of more complexity and higher p-values. To balance this, you can increase the penalizing effect of extra predictors by increasing the multiplicative contribution of the (p + 2) in right of Equation (22.3); though the standard multiplicative factor of k is used in the majority of cases (you can use the optional argument k to change this). That said, criterion-based measures are incredibly useful when you have models that aren't nested (ruling out the partial F-test) and you want to compare them for quick identification of the one that, potentially, provides the parsimonious representation of the data.

# Exercise 22.1

In Sections 22.2.2 and 22.3, you used forward and backward selection approaches to find a model for predicting the cost of construction nuclear power plants (based on the nuclear data frame in the boot package).

-   a. Using the same fullest model (in other words, main effects of all present predictors only), use stepwise AIC selection to find a suitable model for the data.

Exercise 21.2 on page 512 detailed Galileo's ball data. Enter these as a data frame in your current R workspace if you haven't already.

-   c. Fit five linear models to these data with distance as the response—an intercept-only model and four separate partial models of increasing order 1 to 4 in height.

-   d. Construct a table of partial F-tests to identify your favored model for distance. Is your selection consistent with Exercise 21.2 (b) and (c)?

You encountered the diabetes data frame in the faraway package in Section 21.5.2, where you modeled the cholesterol. Load the package and inspect the documentation to refresh your memory of the data set.

-e. There are some missing values in diabetes that might interfere with model selection. Define a new version of the diabetes data frame that deletes all rows with any of the following variables: chol, age, gender, height, weight, frame, waist, hip, location. Use extraction or deletion for a data frame. You can create the required vector of row numbers to be extracted or deleted using na, or you can try using the complete function to obtain a logical flag vector—which helps details.

f. Use your data frame (e) to fit two linear models with chol as the response. The null model object, named dia.null, should be an intercept-only model. The full model object, named dia.full, should be the overly complex model with a four-way interaction (and all lower-order terms) among age, gender, weight, and frame; a three-way interaction (and all lower-order terms) among waist, height, and hip; and a main effect for location.

g. Starting from dia.null and using the same terms as in dia.full for scope, perform stepwise selection by AIC to choose a model for mean total cholesterol and then summarize.

h. Use forward selection based on partial F-tests with a conventional significance level of α = 0.05 to choose a model, starting from dia.null. The result here is the same as the model arrived at in (g)?

i. Stepwise selection doesn't have to start from the simplest model. Repeat (g), but by this time, set dia.full to be the starting model (you don't need to supply anything to scope if you're starting from the most complex model). What is the final model selected via AIC if you start from dia.full? Is it different than the final model from (g)? Why is this or is this not the case, do you think?
