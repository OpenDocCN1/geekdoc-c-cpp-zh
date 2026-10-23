where U is drawn from a uniform distribution in the interval (−1/2, 1/2).

The second example is the Extreme Value distribution whose pdf and cdf are given respectively by:

$f(x) = \sigma^{-1} \exp\left(-\frac{x - \mu}{\sigma}\right) \exp\left(-\exp\left(-\frac{x - \mu}{\sigma}\right)\right), \ x \in \mathbb{R}$

$F(x) = \exp\left(-\exp\left(-\frac{x - \mu}{\sigma}\right)\right), \ x \in \mathbb{R}.$

Show that:

$X = -\sigma \log(-\log(U)) + \mu$

where U is drawn from a uniform distribution in the interval (0, 1). In the case of the extreme value distribution compare your results with those from C++11.

Write functions in C++ to compute random variates from these two distributions.

8. (A Reusable Framework for Random Number Generation)

The goal of this exercise is to create a software framework containing functionality that is needed for random number generation in computational finance. We focus on producing arrays of correlated random numbers. The main requirements are efficiency and accuracy in the short term and then extendibility in a second increment of the framework. You should use the generic class RNGgenerator from Section 15.5.2 as it contains functionality that you can use in the framework.

Answer the following questions:
a) Extend the functionality of RNGgenerator for the creation of matrices with random values.
b) Create free functions to generate two correlated standard normal variates having a given correlation.
c) Create two separate functions to generate an array of correlated random numbers using Cholesky decomposition; one function uses the code presented in Section 26.9.1 while the second function uses the Eigen library. Test these functions on examples to compare efficiency and accuracy. Does Eigen support Cholesky decomposition on matrices with complex coefficients?
d) Stress test: create a loop and in the loop create a random covariance matrix. Apply the functions from part c). Compute the maximum error between the two solutions.
e) Modify the code so that it can switch between different implementations of the Cholesky algorithm (we are typically thinking of a Strategy design pattern (GOF, 1995) or a mixin). Implement this code using the CRTP with std::function as embedded algorithm.
f) Can you discover new requirements and features that you would like to add to the software framework?