where $n$ is the size of the sample, and $x_i$ and $y_i$ are the values of $X$ and $Y$ for the $i$th item in the sample. An example follows.

**Example 11.1** This example is taken from [Aczel and Sounderpandian, 2002]. American Express suspected that charges on American Express cards increased with the number of miles traveled by the card holder. To investigate this matter, a research firm randomly selected 25 card holders and obtained the data shown in Table 11.1. Figure 11.1 shows a scatterplot of the data. We see that it appears that a linear relationship holds between Dollars ($Y$) and Miles ($X$).

The values of $b_0$ and $b_1$ that minimize the MSE are our estimates of $\beta_0$ and $\beta_1$. We do not review how to find the minimizing values here. Any statistics package such as MINITAB, SAS, or SPSS has a linear regression module. If we use one such package to do a linear regression analysis based on the data in Table 11.1, we obtain that

$b_0 = 274.8 \qquad b_1 = 1.26.$

So the linear relationship is estimated to be

$y = b_0 + b_1 x = 274.8 + 1.26 x. \quad (11.2)$

Other information provided by a statistics package, when used to do the linear regression analysis in Example 11.1, includes the following:

| Predictor | Coefficient | SE Coefficient | T | P |
|---|---|---|---|---|
| Constant | $b_0 = 274.8$ | 170.3 | 1.61 | .12 |
| $x$ | $b_1 = 1.255$ | .0497 | 25.25 | 0 |

Briefly, we discuss what each of these quantities means.

+   1. SE coefficient: This quantity, called the **standard error of the coefficient**, enables us to compute our confidence in how close our approximations are to the true values of $\beta_0$ and $\beta_1$ (assuming a linear relationship exists). Recall that for the normal density function, 95% of the mass falls in an interval whose endpoints are the mean $\pm$ 1.96 times the standard deviation. So if $\sigma_0$ is the SE coefficient for $b_0$, we can be 95% confident that

$\beta_0 \in (b_0 - 1.96\sigma_0, b_0 + 1.96\sigma_0).$

In Example 11.1, we can be 95% confident that

$\beta_0 \in (274.8 - 1.96 \times 170.3, 274.8 + 1.96 \times 170.3) = (-58.988, 608.588)$

$\beta_1 \in (1.255 - 1.96 \times .0497, 1.255 + 1.96 \times .0497) = (1.158, 1.352).$

Note that we can be much more confident in the estimate of $\beta_1$.