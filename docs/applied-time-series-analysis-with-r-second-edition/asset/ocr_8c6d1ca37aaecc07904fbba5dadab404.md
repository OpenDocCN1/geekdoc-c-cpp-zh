b1 is the slope of a linear regression component (default = 0 for)
coef is a 2-component vector specifying the coefficients (if only one cosine term is desired define coef[2] = 0) (default = c(0,0))
freq is a 2-component vector specifying the frequency components (0 to .5) (default = c(0,0)
psi is a 2-component vector specifying the phase shift (0 to 2π) (default = c(0,0))
phi is a vector containing the AR model for the noise process (see Chapter 3). (default = 0) For white noise just use the default values for phi.
vara is the variance of the noise (default = 1).
NOTE: a(t) is a vector of N(0,vara) white noise generated within the function
plot is a logical variable. plot = TRUE (default) produces a plot of the generated realization.
sn determines the seed used in the simulation. (default = 0) (see Note below)

NOTE: sn = 0 (default) produces results based on a randomly selected seed. If you want to reproduce the same realization on subsequent runs of gen.sigplusnoise.wge then set sn to the same positive integer value on each run.

# Example: The command

```
x = gen.sigplusnoise.wge(n = 100,coef = c(1.5,3.5)
freq = c(.05,.2),psi = c(1.1,2.8),phi = .7,vara = 2)
```

calculates

x(t) = 1.5cos(2π(0.5)t + 1.1) + 3.5cos(2π(.2)t + 2.8) + z(t), t = 1, 2, ..., 100

where z(t) is a realization from the AR(1) process z(t) = (1 - .7B)a_t where σ_a^2 = 2. The realization is based on a randomly selected seed, and the resulting signal-plus-noise realization is placed in the vector x.

+   2. Combination Plot Routines for Chapter 1
+   
+   a. plotts.sample wge(x,lag.max,trunc,arlimits) is a tswge R function that plots a realization, sample autocorrelations, periodogram, and smoothed periodogram based on the Parzen window (both plotted in dB).