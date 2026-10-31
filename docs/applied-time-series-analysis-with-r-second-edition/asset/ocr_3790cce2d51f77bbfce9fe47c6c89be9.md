# 12
Wavelets

As we know, a (covariance) stationary process, X(t), is defined to be a process for which the following conditions hold:

+   1. E[X(t)] = μ (constant for all t).
+   2. Var [X(t)] = σ² < ∞ (i.e., a finite constant for all t) (12.1).
+   3. Cov [X(t), X(t + h)] = γ(h) (i.e., the covariance between random variables X(t) and X(t + h) depends only on h (and not on t)).

To this point in this book, we have discussed processes that are stationary, processes that are not stationary because the process mean changes with time (signal + noise, etc.), and the ARUMA models (which have infinite variance). Time series for which Condition 3 in Equation 12.1 is not satisfied, are characterized by realizations whose correlation structure (or frequency behavior) changes with time. In Chapters 12 and 13, we will discuss techniques for analyzing data that are nonstationary because they have frequency (correlation) behavior that changes with time. Such data are called time-varying frequency (TVF) data and include a wide number of applications such as seismic signals, animal and insect noises (e.g., whale clicks, bat echolocation, and insect chirps), and astronomical signals. In Section 12.1, we will discuss shortcomings of classical spectral analysis when applied to data with TVFs. In Section 12.2, we will discuss modifications of Fourier-based spectral analysis techniques designed to capture TVF behavior in data, and in the remainder of the chapter we will discuss wavelet analysis as a much more general tool that can be used for analyzing such data. In Chapter 13, we discuss recent developments in the analysis of TVF data that change regularly across time.