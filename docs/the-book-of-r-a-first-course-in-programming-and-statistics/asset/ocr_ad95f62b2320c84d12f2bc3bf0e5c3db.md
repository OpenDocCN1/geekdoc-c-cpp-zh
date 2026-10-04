As noted earlier, it’s important that you interpret these results—indeed based on a k-level categorical variable in regression—in a collective fashion. You can claim that there is no discernible effect of smoking on height because all the p-values for the binary dummy coefficients are nonsign. If one of the levels was in fact highly significant (through a small p-value), it would imply that the smoking factor as defined here, as a whole, has a statistically detectable effect on the response (even if the two levels were still associated with very high p-values). This will be discussed further in several more examples in Chapter 21.

# 20.5.3 Changing the Reference Level

Sometimes you might decide to change the automatically selected reference level, compared to which the effects of taking any one of the others are estimated. Changing the baseline will result in the estimation of different coefficients, making individual p-values subject to change, but the overall result (in terms of global significance of the factor) will not be affected. Because of this, altering the reference level is only done for intuitive baseline of the predictor (for example, “Placebo” versus “Drug A” and “Drug B” as a treatment variable in the analysis of some clinical trial) from which you want to estimate deviation in the mean response with respect to the other possible categories.

Redefining the reference level can be achieved quickly using the built-in function in R. This function allows you to choose which level comes first in the definition of a given factor vector object and will therefore be designated as the reference level in subsequent model fitting. In the current example, let’s say you have the nonsmok as the reference level.

```
R SmokeReordered <- relevel(survey$smoke,ref="Never")
R levels(SmokeReordered)
[1] "Never" "Heavy" "Occas" "Regul"
```

The function has moved the Category into the first position in the new factor vector. If you go ahead fit the model using SmokeReordered instead of the original Smoke column of survey, it’ll provide estimates of coefficients associated with the three different levels of smokers.
It’s worth noting the differences in the treatment of unordered versus ordered factor vectors in regression applications. It might seem sensible to formally order the smoking variable by, for example, when increasing the frequency of smoking when creating a new factor vector. However, when an ordered factor vector is supplied in a call to lm, R returns in a different way—it doesn’t perform the relatively simple dummy coding here, where an effect is associated with each optional level to the baseline (technically referred as orthogonal contrasts). Instead, the default behavior is to fit the model based on called polynomial contrasts, with the effect of the ordered categorical variable on the response is defined in a more complicated functional form. That discussion is the scope of this text,