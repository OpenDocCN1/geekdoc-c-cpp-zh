# Definition 5.1

1. The *autoregressive integrated moving average process* of orders p, d, and q (ARIMA(p,d,q)) is a process, X_t, whose differences (1 − B)^d X_t satisfy an ARMA(p,q) model (that is, a stationary model) where d is a non-negative integer. We use the notation

φ(B)(1 − B)^d X_t = θ(B)a_t  (5.7)

where all the roots of φ(z) = 0 and θ(z) = 0 are outside the unit circle, and φ(z) and θ(z) have no common factors.

2. The *autoregressive unit root moving average process* of orders p, d, and q (ARUMA(p,d,q)) is an extension of the ARIMA(p,d,q) model to include processes, X_t, for which the process λ(B)X_t satisfies an ARMA(p,q) model where λ(B) = 1 − λ_1 B − ⋯ − λ_d B^d is an operator whose characteristic equation has all its roots (real and/or complex) on the unit circle. We use the notation

φ(B)λ(B)(X_t − μ) = θ(B)a_t  (5.8)

to denote such a process.

It is worth noting that φ(B)λ(B)μ = φ(1)λ(1)μ, and therefore, we can write Equation 5.8 in the form

φ(B)λ(B)X_t = φ(1)λ(1)μ + θ(B)a_t  (5.9)

The term φ(1)λ(1)μ is called the *moving average constant*, and if λ(B) = (1 − B)^d, then λ(1) = 0 and so φ(1)λ(1)μ = 0. This is not true in general for an ARUMA(p,d,q) model, that is, if 1 − B is not a factor of λ(B), then φ(1)λ(1) ≠ 0.

# EXAMPLE 5.3: ARIMA(0, 1, 0) MODELS AND THE DOW JONES 2014 DATA

A realization from an ARIMA(0, 1, 0) process will be similar to those from a stationary AR(1) process with φ_1 close to +1. Consider for example the realization in Figure 3.5a from the AR(1) model (1 − 0.95B)X_t = a_t which shows the characteristic wandering behavior associated with the AR(1) model with a positive real root close to +1.