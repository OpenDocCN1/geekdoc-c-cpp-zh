an exponential sigmoid function. The equations for these NLP functions are:

For

| | arctan | sigmoid |
|---|---|---|
| $y = \frac{2}{\pi}(1-\frac{x^2}{3})$ | $y = \frac{\arctan(kx)}{\arctan(k)}$ | $y = \frac{2}{1+e^{-x}}-1$ | (4.67)

simplicity's sake, all of the non-linear processing blocks in our synthesizers use the tanh(x) function. In some cases, this is warranted that the nonlinearity results from a hyperbolic tangent function in the filter equations. In other cases involving diode-based distortion, other wave shapers may yield more accurate results. Of course you are encouraged to experiment with all of the wave shapes in your projects.

Figure 4.39: (a) and (b) two alternate versions of the bilinear integrator.

![](bbox=[0.345, 0.255, 0.952, 0.485])

# 4.17 Challenges

# Bronze

Derive the equation for $y_{HP}$ for the VA state variable filter.

# Sliver

Derive the equations for $y_{LP}$ and $y_{BP}$ for the VA state variable filter.

# Gold

Use signal flow graphing and Mason's Gain Equation to verify that the input/output relationship of the three filters-feedback-loops (Figures 4.29, 4.31 and 4.33) all produce the relationship $y = Gx + S$.

# Platinum

Use the Modified Härmä to resolve the delay-free loop in Figure 4.33.

# Diamond

Two alternate versions of the bilinear integrator are shown in Figure 4.39. Replace the bilinear integrator in the VA lowpass filter with each of these and use the Modified Härmä to derive the resulting modified structures with delay-loops resolved. Formulate the difference equations of the integrators using the s node values.

# Bibliography

Avanini, Federico, Fontana, Federico and Rocchesson, Davide. 2000. "Computation of Nonlinear Filter Networks Containing Delay Free Paths." Proceedings from the Seventh International Conference on Digital Audio Effects.

Borin, Gianpaolo, De Poli, Gianovani and Rocchesson, Davide. 2000. "Estimation of Delay Free Loops in Discrete-Time Models of Nonlinear Acoustic Systems." IEEE Transactions on Speech and Signal Processing, vol. 23, pp. 558–562.

Brut, Len. 1975. "Low-Sensitivity Digital Ladder Filters." IEEE Transactions on Circuits and Systems, vol. CAS-22, no. 3, pp. 168–176.