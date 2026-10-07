# 8.2 Statistical Model for Bayesian Dose-Response

In this chapter we will only provide examples of a Bayesian hyperbolic model (Chapter 6). The sigmoid model or other non-linear models are out of scope [3,4]. It may be noted though that the sigmoid model can easily be implemented by adding a h parameter to the hyperbolic model. From Section 6.4.1, the Bayesian hyperbolic model is written as

```
$y_i = E_0 + E_{max} \tilde{A} - \frac{D_i}{ED_{50} + D_i} + I_i \mu_i$
```

where

+   1. $i$ is the subject ID

+   2. $y_i$ is the observed continuous response variable for the $i$th patient

+   3. $E_0$ is the basal effect, the response when the dose is 0mg

+   4. is the maximum effect attributable to the drug

+   5. $ED_{50}$ is the dose that produces half the effect of

+   6. $D_i$ is the dose level for the $i$th patient

+   7. $\epsilon_i$ is the random error for the $i$th patient. A standard assumption, adopted here, is that the $\epsilon_i$ terms are independent and identically distributed with a mean of 0 and variance $\sigma^2$. An additional standard assumption is that the error terms are normally distributed.

Further, assume that $y_i\sim N(\mu_i, \tau)$, where $\tau=1/\sigma^2$ is the precision. For the Bayesian analysis, prior assumptions are made around the distribution of the parameters of the hyperbolic model, i.e., by assuming some distributions around the parameters of the model (i.e., $E_0, ED_{50}$, and the precision parameter $\tau$).

For a binary outcome, the model can be readily revised to be a