there were no significant noise factors, and no significant interactions between the control and noise factors. Therefore, variability in percent shrinkage could not be accomplished by reducing or nullifying the effect of the suspected noise factors used in the experiment. However, there are obviously other unknown or lurking noise factors that are causing variability in the response. By identifying a dispersion effect and choosing the level which minimizes the variability, one actually reduces the effects of the unknown noise factors resulting in a more consistent response.

Box and Meyer (1986b) described a more formal method of detecting dispersion effects. They propose to first fit a model to the response (for this example A, B, and A x B) and calculate the residuals from the model. Next, they calculate the dispersion statistic for each factor as the natural log of the ratio of the sample variances of the residuals at the high and low levels with the formula

```
\( E_i' = \ln \frac{S^2(i^+)}{S^2(i^-)} \) (12.5)
```

where \( S^2(i^+) \) is the sample variance of the residuals at the high level of factor \( i \) and \( S^2(i^-) \) is the sample variance of the residuals at the low level of factor \( i \). They show that these statistics are approximately normally distributed with mean zero and standard deviation 1.

# 12.6 Joint Modeling of Mean and Dispersion Effects

# 12.6.1 Joint Modeling

One of the assumptions that justifies fitting a linear model by least squares is constancy of the variance of the experimental error across all levels of the factors in the model. If there is a dispersion effect, this assumption will obviously be violated. Therefore, the accuracy of the coefficients in the model for the average response will be reduced because too much weight will be given to minimizing errors in prediction in regions where the variance is larger. Nelder and Lee (1998) and Lee and Nelder (2003) have suggested an iterative weighted least squares approach to estimation. This consists of:

+   1. Fitting a model

```
\( \hat{\beta} = (X'X)^{-1}X'y \) (12.6)
```

which includes all terms that affect the mean response, and calculating and storing the residuals from this model.

+   2. Fitting a model

```
\( \hat{\gamma} = (X'X)^{-1}X'z \) (12.7)
```

which includes all dispersion effects is fit, using \( z_i = \ln r_i^2 \) as the response, where \( r_i \) are the residuals from the model fit in Section 12.6. The predicted values from this model, \( \hat{z}_i \) are calculated and stored.