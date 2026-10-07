![](bbox=[0.625, 0.95, 0.89, 0.285])

# # Generalized Linear Models

+   2.1 Introduction ................................................................................15
2.2 Linear Regression Models......................................................................16
2.3 A Simple Linear Regression Example...........................................................19
2.4 Generalized Linear Models......................................................................22
2.5 The Deviance and the Pearson Chi-Square Statistic ........................24
2.6 Maximum Likelihood Estimation for Generalized Linear Models..................26
2.7 A Dosage-Mortality Example.....................................................................28
2.8 Odds-ratios and Logistic Regression.........................................................39
2.9 A Poisson Example of Failures of Electronic Equipment ........................46

# ## 2.1 Introduction

Standard linear models are composed of two components known as the systematic effects and the random errors. The underlying distribution of errors is assumed to be Normal. The estimation method is the well-known Ordinary Least Squares. Generalized Linear Models (GLM) is an extension of the usual linear regression to distributions such as, but not limited to, the Binomial, Multinomial, Poisson, Negative-binomial, Gamma, and Beta. Originally proposed by Nelder and Wedderburn (1972), GLM is a unified approach that allows performing regression analyses with any important in statistical regression and inference. Historically, it preceded three important areas related to overdispersion, Quasi-likelihoods, Generalized Estimating Equations (GEE), and Generalized Linear Mixed Models (GLMM). In this chapter we will review the basic concepts of the classical linear model, provide a quick illustrative example of simple linear regression, then we will cover the main characteristics of GLM, emphasizing the Binomial and Poisson distributions. We will provide some examples. The examples illustrate only selected aspects of these models and are not meant to be exhaustive.

Morel, Jorge and Nagaraj Neeraj. Overdispersion Models in SAS®. Copyright © 2011, SAS Inc., North Carolina, USA . ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.