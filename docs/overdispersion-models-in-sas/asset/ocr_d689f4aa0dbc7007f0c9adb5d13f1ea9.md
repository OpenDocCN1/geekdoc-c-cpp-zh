# Chapter 1 Overdispersion 3

$$\chi^2 = \sum \frac{(t-m\tilde{\pi})^2}{m\tilde{\pi}(1-\tilde{\pi})}$

Based on theoretical grounds, the value of this statistic by its degrees of freedom (10) is considered a Goodness-of-fit (GOF) statistic for the binomial-type of data. In this illustrative example, the value of the GOF statistic is 5.28. Under the Binomial model its value should be approximately 1. This means that in this case, the estimated variance of $\tilde{\pi}$, previously 0.0027, should be approximately 5.28 times larger than the value expected under the Binomial model. Not 0.0142 divided by 0.0027 is 5.26. Thus, the data in this example exhibit **overdispersion** or extra variation. This phenomenon also occurs over the Multinomial and Poisson distributions. In this example, the correct value of the estimated variance of $\tilde{\pi}$ should be close to (0.0027)(5.28) = 0.014.

#  1.2 Overdispersion

Consider a study where experimental units are clusters, and where each element unit within the cluster is classified into two mutually exclusive categories. If we assume elemental units are independent with a common probability of success, the Binomial model is appropriate for analyzing the data. Clustering creates a lack of independence among elemental units. The probability of success may vary from one element unit to another within a cluster. Consequently, the data usually exhibit larger variances than the variance permitted by the Binomial model. This phenomenon, as previously stated, is known as **overdispersion or extra variation.**

Overdispersion might be caused by other factors. Omitted variables in the model can cause overdispersion. That is, the response probability is in fact a function of several covariates, the model contains a subset of them. This lack of fit manifests itself as overdispersion. Some of the diagnostic plots presented later are迫 by this overdispersion.

Overdispersion is also observed on multinomial responses (on count data) analyzed under a Multinomial (Poisson) model may be greater than what can be attributed to the sampling variation assumed by the model. McCullough and Nelder (1989, pp. 124-125) point out

> "Overdispersion is not uncommon in practice. In fact, some would maintain that overdispersion is the norm in practice and normal dispersion"

The phenomenon of **underdispersion** occurs less frequently. Cox and Snell (1988, p. 107) point out that "underdispersion is sometimes observed, although this is uncommon." It might take place when there is a competition for a positive response. In a case where a person is tasting sweet drinks, he or may feel the second drink is not so sweet—even if it is indeed. While overdispersion occurs here, this phenomenon will not be treated here.

As discussed in Stigler (1986), examples of overdispersion arising from a clustered population can be traced in the literature as far back as 1986. Examples of Multinomial models with overdispersion may arise (in a teratological study of a genetic trait which is passed with a certain probability to offspring of the same mother); in reproductive

Morel, Jorge, and Nagaraj Neelcher. Overdispersion Models in SAS. Copyright ©2011; SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. For additional resources, visit.sas.com/publishing.