# 1.2 Stationary Time Series

In the study of a time series, it is common that only a single realization from the series is available. Analysis of a time series on the basis of only one realization is analogous to analyzing the properties of a random variable on the basis of a single observation. The concepts of stationarity and ergodicity will play an important role in enhancing our ability to analyze a time series on the basis of a single realization in an effective manner. A process is said to be *stationary* if it is in a state of “statistical equilibrium.” The basic behavior of such a time series does not change in time. As an example, for such a process, μ(t) would not depend on time and thus could be denoted μ for all t. It would seem that, since x(t) for each t ∈ T provides information about the ensemble mean, μ, it may be possible to estimate μ on the basis of a single realization. An *ergodic* process is one for which ensemble averages such as μ can be consistently estimated from a single realization. In this section, we will present more formal definitions of stationarity, but we will delay further discussion of ergodicity until Section 1.4.

The most restrictive notion of stationarity is that of *strict stationarity*, which we define as follows.

# Definition 1.4

A process {X(t); t ∈ T} is said to be strictly stationary if for any t₁, t₂, …, tₖ ∈ T and any h ∈ T, the joint distribution of {X(t₁), X(t₂), …, X(tₖ)} is identical to that of {X(t₁ + h), X(t₂ + h), …, X(tₖ + h)}.

**NOTE:** We have tacitly assumed that T is closed under addition, and we will continue to do so.

Strict stationarity requires, among other things, that for any t₁, t₂ ∈ T, the distributions of X(t₁) and X(t₂) must be the same, and further that all bivariate distributions of pairs {X(t), X(t + h)} are the same for all h, etc. The requirement of strict stationarity is a severe one and is usually difficult to establish mathematically. In fact, for most applications, the distributions involved are not known. For this reason, less restrictive notions of stationarity have been developed. The most common of these is *covariance stationarity*.