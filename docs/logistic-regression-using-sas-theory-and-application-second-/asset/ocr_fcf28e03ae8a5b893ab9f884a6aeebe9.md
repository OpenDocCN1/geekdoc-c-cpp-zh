compensate for the fact that the approximation to the normal or chi-square distributions may be poor.

The other reason for ML’s popularity is that it is often straightforward to derive ML estimators when there are no other obvious candidates. One case that ML handles very nicely is data with categorical dependent variables.

The basic principle of ML is to choose as estimates those parameter values that, if true, would maximize the probability of observing what we have, in fact, observed. There are two steps to this: (1) write down an expression for the probability of the data as a function of the unknown parameters, and (2) find the values of the unknown parameters that make the value of this expression as large as possible.

The first step is known as constructing the *likelihood function*. To accomplish this you must specify a model, which amounts to choosing a probability distribution for the dependent variable and choosing a functional form that relates the parameters of this distribution to the values of the explanatory variables. In the case of the logistic model, the dichotomous dependent variable is presumed to have a binomial distribution with a single “trial” and a probability of “success” given by $p_i$. Then $p_i$ is assumed to depend on the explanatory variables according to equation (2.3), which is the logistic model. Finally, we assume that the observations are independent across individuals.

The second step—maximization—typically requires an iterative numerical method, which means that it involves successive approximations. Such methods are usually more computationally demanding than a non-iterative method like ordinary least squares. For those who are interested, I will work through the basic mathematics of constructing and maximizing the likelihood function in Chapter 3. Here I focus on some of the practical aspects of ML estimation with SAS.

# 2.7  Maximum Likelihood Estimation with PROC LOGISTIC

The most popular SAS procedure for doing ML estimation of the logistic regression model is PROC LOGISTIC. SAS has several other procedures that will also do this, and we will meet some of them in later chapters. But LOGISTIC has been around the longest, and it has the largest set of features that are likely to be used by most data analysts.

Let’s estimate a logistic model analogous to the linear probability model that we examined in Section 2.2. Minimal SAS code for this model is