```
%gof_test(Pred_Milk_1,'Poisson Hurdle',7-1-2);
title2 "Negative-binomial Hurdle Model";
%gof_test(Pred_Milk_2,'Negative-binomial Hurdle',7-1-3);\ods htm close;
```

The results of the Pearson's Goodness-of-fit (GOF) tests are shown in Output 6.6. Under the Poisson Hurdle model (null), the value of the GOF test is 38.04, which is asymptotically distributed as a Chi-square random variable with four degrees of freedom. Its associated P-value is smaller than 0.0001, indicating that the Poisson Hurdle model is not a good fit to these data. On the other hand, the value of the GOF statistic for the Negative-binomial Hurdle model is 2.06, which, under the null hypothesis, is asymptotically distributed as a Chi-square random variable with three degrees of freedom. Its associated P-value is approximately 0.56. We conclude that the Negative-binomial Hurdle model allows for overdispersion and also accommodates the presence of excess of zeros in a reasonable way.

Output 6.7: Goodness-of-fit Results of the Hurdle Models—Daily Milk Consumption Data

![](bbox=[0.256, 0.393, 0.743, 0.873])

Morel, Jorge, and Nagaraj Neerajal. Overdispersion Models in SAS*. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA: ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.