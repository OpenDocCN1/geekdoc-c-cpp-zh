coefficients for the random intercepts model are all larger in magnitude than the coefficients for the GEE model. That’s to be expected because mixed model coefficients correct for heterogeneity shrinkage but GEE coefficients do not. The greater the variance of α, the bigger the difference you will find between mixed model and GEE coefficients.

So if you really want subject-specific estimates of the coefficients, mixed models are the way to go. But mixed models can be much more computationally intensive than GEE because of the need for numerical integration. And not infrequently, they break down completely for reasons that are not always apparent. If your main goal is to get accurate p-values, GEE may do perfectly well.

Mixed models can be elaborated in several different ways, one of which is to allow the coefficients themselves to vary randomly across persons. This is sometimes called a random slopes model. Let’s try it for the PTSD data. Suppose we think that SEVENT (the number of stressful events) has different effects for different people. To allow for this, we can modify the model by putting an i subscript on the coefficient vector.

log( p_it / (1 - p_it) ) = α_i + β_i x_it . (8.3)

This equation would allow all the coefficients to vary across persons, but we want to focus on the special case where just one of them is allowed to vary. We’ll assume that the SEVENT coefficient is normally distributed, with a mean and variance that we shall estimate. We’ll also assume that the random coefficient is independent of everything else on the right-hand side of the equation. Here’s the GLIMMIX code for implementing that model:

```
PROC GLIMMIX DATA=ptsd METHOD=QUAD;
    CLASS subjid time;
    MODEL ptsd = control problems sevent cohes time / D=B S;
    RANDOM INTERCEPT sevent/ SUBJECT=subjid;
    COVTEST 0 .;
    COVTEST . 0;
RUN;
```

To make a coefficient random, we merely put the variable name on the RANDOM statement. This can only be done for variables that vary within subject. We could not, for example, put COHES on the RANDOM statement because it was only measured once and does not change