# Chapter 7 Likelihood Models for Overdispersed Multinomial Responses 245

the confidence intervals fall in the zero-one interval, one needs to use the inverse method. If $\hat{L}$ and $\hat{U}$ correspond respectively to the lower and upper bounds of a 95% confidence interval for $\alpha_0$, an approximate 95% confidence interval for $\kappa$ by using the inverse method is given by

```
$$\left\{ \frac{\exp(\hat{L})}{1+\exp(\hat{L})}, \right\}, \left\ \frac{\exp(\\hat{U})}{1+\exp(\\hat{U})} \right\}$
```

The results of confidence intervals using NLMIXED are shown below.

![](bbox=[0.196, 0.269, 0.803, 0.383])

![](bbox=[0.196, 0.413, 0.803, 0.526])

The FREQ and NLMIXED procedures clearly provide very consistent results with one another. Note that the correlated model (7.40) belongs to the family of Generalized Linear Overdispersed Models and allows the use of link functions, as discussed earlier in this chapter, on the vector of probabilities $\pi$ and the overdispersed parameter $ho$ ($\kappa=ho^2$). We would like the reader to note that the methods discussed in the context of GLOM may be applied to model Kappa with covariates.

Landis and Koch (1977) have provided the following guidelines (which are shown in Table 7.8) for interpreting the value of Kappa. These guidelines are not universal and are not necessarily accepted by all statisticians.