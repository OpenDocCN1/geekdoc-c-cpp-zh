# Chapter 1 Overdispersion 5

Note while the expected value of T matches the Binomial model, the variance given in equation (1.2) is more than the variance modeled by a Binomial model because the factor {1+p²(m-1)} is greater than one. A random variable T with mean and variance, as in equations (1.1) and (1.2), is said to have overdispersion or extra variance relative to the Binomial model. This simple structure of overdispersion is well-recognized among sampling practices. See, for instance, equation 8.1 in Hansen and (1953), where the variance under one-stage sampling is presented as a function of the variance under simple random sampling. Similar observations can be found in the classical books by Kish (1965) and Cochran (1977).

Among practitioners, the parameter ρ² represents the intra-cluster correlation and the factor {1+ρ²(m-1)} is the design effect. The case “positively correlated” corresponds to overdispersion. Previously stated, the occurrence of overdispersion is less common and corresponds to a negative correlation among the Bernoulli which comprise T.

Similarly, the definition of overdispersion can be extended to the case of Multinomial distribution. A cluster consisting of m elemental units where the elemental units are being classified into (d+1) categories. Let T denote the d-dimensional vector of counts, corresponding to the first d categories, where i-th component represents the number of elemental units classified into the i-th category. With clustered data, the vector T, which is usually modeled by a Multinomial distribution, often exhibit higher variability in the data than was allowed by the Multinomial model. In order to accommodate this overdispersion, the following moment structure is usually hypothesized as

```
E(T) = mμ
```

```
Var(T) = m[Diag(π) - πᵀ]{1+ρ²(m-1)}
```

where π = (π₁, π₂, ..., πᵈ) is a vector of probabilities, 0 < πᵢ < 1, Σπᵢ ≤ 1, and ρ (or ρ²) is the overdispersion parameter. If the multinomial-type T has mean and variance-covariance matrix it is said to have overdispersion relative to the Multinomial distribution. When ρ=0 the variance estimators in equations (1.2) and (1.4) reduce to that of the Binomial/Multinomial model. Several issues such as maximum likelihood estimation and Quasi-likelihood Models over the Multinomial distribution will be covered in Chapter 7.

Recall that for a Poisson random Y, E(Y) = Var(Y) = μ, μ > 0. Poisson random variable is a count of the number of occurrences of an event in a given time interval. As in the binomial case, there underlying assumptions on the process for deriving the properties of a Poisson random variable. When these assumptions are not met, overdispersion may arise. When Y is a Poisson-type of random variable, Y is said to have overdispersion if its first two moments are of the form

```
E(Y) = μ, μ > 0
```