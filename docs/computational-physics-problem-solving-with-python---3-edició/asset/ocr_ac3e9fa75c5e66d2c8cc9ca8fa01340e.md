# 12.5.4

# Nonperiodic Function DFT (Exploration)

Consider a simple model (a wave packet) of a “localized” electron moving through space and time. A good model for an electron initially localized around x = 5 is a Gaussian multiplying a plane wave:

ψ(x, t = 0) = exp[ −1/2 ((x − 5.0)/σ₀)² ] e^{i k₀ x}.  (12.52)

This wave packet is not an eigenstate of the momentum operator⁶ p = i d / dx and in fact contains a spread of momenta. Your problem is to evaluate the Fourier transform

ψ(p) = ∫_{-∞}^{+∞} dx e^{i p x} / √{2π} ψ(x) ,  (12.53)

as a way of determining the momenta components in (12.52).

# 12.6

# Filtering Noisy Signals

You measure a signal y(t) that obviously contains noise. Your problem is to determine the frequencies that would be present in the spectrum of the signal if the signal did not contain noise. Of course, once you have a Fourier transform from which the noise has been removed, you can transform it to obtain a signal s(t) with no noise.

> In the process of solving this problem, we examine two simple approaches: the use of autocorrelation functions and the use of filters. Both approaches find wide applications in science, with our discussion not doing the subjects justice. We will see filters again in the discussion of wavelets in Chapter 13.

# 12.7

# Noise Reduction via Autocorrelation (Theory)

We assume that the measured signal is the sum of the true signal s(t), which we wish to determine, plus some unwelcome noise n(t):

y(t) = s(t) + n(t) .  (12.54)

Our first approach at removing the noise relies on that fact that noise is a random process and thus should not be correlated with the signal. Yet what do we

6) We use natural units in which ℏ = 1.