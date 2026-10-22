kinds of errors. Failing to detect a disease might be regarded as a substantially more costly error than diagnosing someone with the disease who doesn’t really have it.

Now we are finally ready to talk about ROC curves. The ROC curve gives us a way of graphically summarizing the information in Output 3.17. It also provides the basis for calculating a single statistic that assesses the predictive power of the model and does not depend on the cutpoint value. The ROC curve is simply a graph with sensitivity on the vertical axis and 1 minus specificity on the horizontal axis, both of which increase as the cutpoint decreases from 1 to 0. PROC LOGISTIC can produce the curve with the following code:

```
PROC LOGISTIC DATA=penalty PLOTS(ONLY)=ROC;
    MODEL death(EVENT='1')=blackd whitvic culp ;
RUN;
```

The option ONLY after the PLOTS option is included to suppress the production of influence plots that would otherwise appear by default. We’ll discuss influence plots in the next section.

The resulting ROC curve is shown in Output 3.18. The 45-degree line represents the expected ROC curve for a model with an intercept only, that is, one with no predictive power. The more the curve departs from the 45-degree line, the greater the predictive power. The standard statistic for summarizing that departure is the area under the curve, which here is reported as .8998. As noted earlier, this is the same as the c statistic that is reported in the “Association of Predicted Probabilities and Observed Responses” table. (There may be a slight difference because different methods are used to approximate the area.) So if all you want is the area under the curve, there is no need to request the curve itself. One technical note: The predicted probabilities used in the construction of the ROC curve are not biased corrected like the ones used to produce Output 3.17.