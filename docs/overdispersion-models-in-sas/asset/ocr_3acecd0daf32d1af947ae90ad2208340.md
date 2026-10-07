# Quasi-likelihood Functions

+   3.1 Introduction...............................................................................................51

+   3.2 Quasi-likelihood functions......................................................................52

+   3.3 An Oral Care Example....................................................................................54

+   3.4 Toxoplasmosis in El Salvador...............................................................57

+   3.5 A Carcinogenesis Pre-clinical Experiment...............................................63

+   3.6 An Osteoporotic Example of Patients at High Risk for Vertebral Fractures................................................................................................................66

+   3.7 Williams’ Quasi-likelihood Model ........................................69

# 3.1 Introduction

In Chapter 2, we discussed Maximum Likelihood Estimation (MLE) of the parameters in the context of Generalized Linear Models (GLM). As we discussed, these estimators enjoy desirable properties: they are consistent, asymptotically efficient, and normally distributed. In many instances where overdispersion is present, it would be ideal to use maximum likelihood estimation. Extending MLE to overdispersed data requires additional information on the random mechanism generating the overdispersion; this information makes it possible for a complete likelihood to be written down. However, in many real-life cases, a likelihood that explains overdispersion might not be available. Therefore, estimation of overdispersion models may be addressed by Quasi-Likelihood Estimates (QLEs), which are based essentially on the specification of the first two moments of the data. QLEs are the natural first method of estimating the parameters of the overdispersion model obtained from a function known as quasi likelihood, defined by Wedderburn (1974), and based on a likelihood function. These functions allow one to analyze overdispersed data without full knowledge of the likelihood function and show the relation between the mean and the variance of the observations that reveal. In this chapter we will introduce the concept of quasi-likelihood functions and show applications to the Binomial and Poisson distributions. QLEs will form the starting point for the numerical computation; it will also become the benchmark for theoretical comparisons of the full likelihood estimation methods, which will be presented in later

![](bbox=[0.6265, 0.0985, 0.8905, 0.3335])