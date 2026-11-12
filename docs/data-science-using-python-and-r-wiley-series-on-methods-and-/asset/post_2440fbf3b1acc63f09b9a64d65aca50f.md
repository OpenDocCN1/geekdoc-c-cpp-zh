
- 6. Miss the Bigger Picture. Further, analysts should try to keep an eye on the big picture, and analysis solely at the variable level might miss the fundamentals underlying relationships among the predictors. Instead, several predictors might fall naturally into a single group (a factor or component), which addresses a single aspect of the data. For example, the variables savings account balance, checking account balance, home equity, stock portfolio value, and 401k balance might all fall together under the single component, assets.

In summary, dimension reduction methods use the correlation structure among the predictor variables to accomplish the following:

- 1. Reduce the number of predictor items.
- 2. Help ensure that these predictor items are uncorrelated.
- 3. Provide a framework for interpretability of the results.

## 12.2 MULTICOLLINEARITY

Data scientists need to guard against multicollinearity, a condition where some of the predictor variables are correlated with each other. Multicollinearity leads to instability in the solution space, leading, for example, to regression coefficients you cannot trust, because the coefficient variability is so large. Multicollinearity is an occupational hazard for data scientists, because many of the data sets have dozens if not hundreds of predictors, some of which are often correlated.

Consider Figures 12.1 and 12.2. Figure 12.1 illustrates a situation where the predictors $x_1$ and $x_2$ are not correlated with each other; that is, they are orthogonal, or independent. In such a case, the predictors form a solid basis, upon which the response surface $y$ may rest sturdily, thereby providing stable coefficient estimates $b_1$ and $b_2$ each with small variability. On the other hand, Figure 12.2 illustrates a multicollinear situation where the predictors $x_1$ and $x_2$ are correlated with each other, so that as one of them increases, so does the other. In this case, the predictors no longer form a solid basis upon which the response surface may firmly rest. Instead, when the predictors are correlated, the response surface is unstable, providing highly variable coefficient estimates $b_1$ and $b_2$.

![](img/fbc96b887811576a0dc93355dce68ae3_178_0.png)

Figure 12.1 When the predictors $x_1$ and $x_2$ are uncorrelated, the response surface $y$ rests on a solid basis, providing stable coefficient estimates.

![](img/fbc96b887811576a0dc93355dce68ae3_179_0.png)

Figure 12.2 Multicollinearity: when the predictors are correlated, the response surface is unstable, resulting in dubious and highly variable coefficient estimates.

The high variability associated with the estimates means that different samples may produce coefficient estimates with widely different values. For example, one sample may produce a positive coefficient estimate for $x_1$, while a second sample may produce a negative coefficient estimate. This situation is unacceptable when the analytic task calls for an explanation of the relationship between the response and the predictors, individually.

Let us look at a toy example to help us understand the problem. Consider the tiny population in Table 12.1.

Clearly, $x_1$ and $x_2$ are correlated, with $r = 0.938$, $p$-value about 0. Now, split into two samples, as shown in Tables 12.2 and 12.3. The regression equation for sample 1 is:

```
$$ \hat{y} = -0.542 + 2.552 x_1 - 0.206 x_2 $$
```

The regression equation for sample 2 is:

```
$$ \hat{y} = -1.08 + 0.547 x_1 + 1.759 x_2 $$
```

Note that the coefficient for $x_1$ is negative in sample 1 and positive in sample 2. This represents unstable behavior in the regression coefficients, caused by the correlation between the predictors. Essentially, we cannot trust the values, or even the signs, of the regression coefficients. So, interpreting the regression coefficients for our clients

### TABLE 12.1 Tiny population for our toy example

| x1 | x2 | Target, y |
|---|---|---|
| 1 | 1 | 2.0693 |
| 1 | 2 | 2.6392 |
| 2 | 2 | 3.7501 |
| 2 | 3 | 5.6432 |
| 3 | 3 | 5.8925 |
| 3 | 4 | 6.4308 |
| 4 | 4 | 8.3950 |
| 4 | 5 | 8.4947 |
| 5 | 5 | 11.3236 |
| 5 | 5 | 10.1562 |

### TABLE 12.2 Sample 1 from our tiny population

| x1 | x2 | Target, y |
|---|---|---|
| 1 | 1 | 2.0693 |
| 2 | 2 | 3.7501 |
| 3 | 4 | 6.4308 |
| 4 | 5 | 8.4947 |
| 5 | 5 | 11.3236 |

### TABLE 12.3 Sample 2 from our tiny population

| x1 | x2 | Target, y |
|---|---|---|
| 1 | 2 | 2.6392 |
| 2 | 3 | 5.6432 |
| 3 | 3 | 5.8925 |
| 4 | 4 | 8.3950 |
| 5 | 5 | 10.1562 |

is probably not a good idea. The values and signs might change from sample to sample, so that interpreting the coefficients from just one sample may cost your client big bucks. This is why we need methods for dealing with this multicollinearity.

We shall use a subset of the Cereals data set, where we estimate the nutrition rating of breakfast cereals, using fiber, potassium, and sugar. Our regression equation is as follows:

```
rating = b0 + b1 · fiber + b2 · potassium + b3 · sugars
```

![](img/fbc96b887811576a0dc93355dce68ae3_181_0.png)

Figure 12.3 Matrix plot of the predictors from Python. Fiber and potassium are correlated.

To be aware of possible multicollinearity, the analyst should investigate the correlation structure among the predictor variables. Figure 12.3 provides the matrix plot of the predictors. Clearly, potassium and fiber are positively correlated. In fact, their correlation coefficient is r = 0.912 (not shown). This strong correlation will inflate the variability of the regression coefficients, making our regression model unstable.

## 12.3 IDENTIFYING MULTICOLLINEARITY USING VARIANCE INFLATION FACTORS

However, suppose we did not check for the presence of correlation among our predictors, and went ahead and performed the regression anyway. Is there some way that the regression results can warn us of the presence of multicollinearity? The answer is yes: We may ask for the variance inflation factors (VIFs) to be reported.

The VIF for the ith predictor is given by:

```
VIF_i = \frac{1}{1 - R_i^2}
```

```
> vif(model03)
Fiber Potass Sugars
6.850050 6.693982 1.158761
```

Figure 12.4 Regression results, with variance inflation factors from R indicating a multicollinearity problem.

where $R_i^2$ represents the $R_i^2$ value obtained by regressing $x_i$ on the other predictor variables. Note that $R_i^2$ will be large when $x_i$ is highly correlated with the other predictors, thus making VIF large.

A rough rule of thumb for interpreting the value of the VIF is to consider $VIF \ge 5$ to be an indicator of moderate multicollinearity, and to consider $VIF \ge 10$ to be an indicator of severe multicollinearity. A VIF of five corresponds to $R_i^2 = 0.80$, while $VIF = 10$ corresponds to $R_i^2 = 0.90$.

For the regression of nutritional rating on fiber, potassium, and sugars, we have the output provided in Figure 12.4. The VIF for fiber is 6.85 and the VIF for potassium is 6.69, with both values indicating moderate-to-strong multicollinearity.

### 12.3.1 How to Identify Multicollinearity Using Python

First, we load the required packages and read in the cereals data set under the name cereals.

```
import pandas as pd
import statsmodels.api as sm
import statsmodels.stats.outliers_influence as inf
cereals = pd.read_csv("C:/.../cereals.csv")
```

Once the data set is in Python, pull out the three predictor variables and put them in their own data frame. Call the data frame X.

```
X = pd.DataFrame(cereals[['Sugars', 'Fiber', 'Potass']])
```

Now that we have the predictor variables all together, use the scatter_matrix() command with X as the input to create a scatterplot matrix.

```
pd.plotting.scatter_matrix(X)
```

The result of the scatter_matrix() command is shown in Figure 12.3 above. Notice that the command creates both scatterplots and histograms.

To obtain the VIF values, we need to do a little data cleaning first. Use the dropna() command on the X data frame to remove any records with missing values.

```
X = X.dropna()
```

Then, make sure you add the constant term in the X data frame.

```
X = sm.add_constant(X)
```
