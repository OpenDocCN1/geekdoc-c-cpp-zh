```
PROC LOGISTIC DATA=penalty;
    MODEL death(EVENT='1')=blackd whitvic serious;
RUN;
```

Of course, there are also numerous options and special features that we’ll consider later.

One option that I’ve specified in the MODEL statement is EVENT='1', after the dependent variable. The default in LOGISTIC is to estimate a model predicting the lowest value of the dependent variable. Consequently, if I had omitted EVENT='1', the result would be a logistic model predicting the probability that the dependent variable DEATH is equal to 0. The EVENT='1' option reverses this so that the model predicts the probability that the dependent variable is equal to 1. (The single quotes around 1 are necessary because PROC LOGISTIC treats the dependent variable as a character variable rather than as a numeric variable.)

An equivalent (and popular) way to accomplish this is to use the option DEATH(DESCENDING), which tells LOGISTIC to model the “higher” value of DEATH rather than the lower. But what is considered higher rather than lower can depend on other options that are chosen, so it’s safer to be explicit about which value of the dependent variable is to be modeled. If you forget the EVENT='1' option, the only consequence is to change the signs of the coefficients. As long as you realize what you’ve done, you shouldn’t need to rerun the model.

Results are shown in Output 2.3. The “Model Information” table is pretty straightforward, except for the “Optimization Technique,” which is reported as Fisher’s scoring. This is the numerical method used to maximize the likelihood function, and we will see how it works in Chapter 3. After the “Response Profile” table, we see the message “Probability modeled is death=1.” If we had not used the EVENT='1' option, this would have said “death=0”, so it’s important to check this so that you correctly interpret the signs of the coefficients. Next we are told that the convergence criterion was satisfied, which is a good thing. Iterative methods don’t always converge, and we’ll talk about why that happens and how to deal with it in Chapter 3.

The next table reports three different “Model Fit Statistics:” AIC, SC, and -2 Log L. Values of these fit statistics are displayed for two different models, a model with an intercept but no covariates (predictors), and a model that includes all the specified predictors (covariates). Usually, we can ignore the INTERCEPT ONLY column. The most fundamental of the fit statistics, -2 Log L, is simply the maximized value of the logarithm of the likelihood