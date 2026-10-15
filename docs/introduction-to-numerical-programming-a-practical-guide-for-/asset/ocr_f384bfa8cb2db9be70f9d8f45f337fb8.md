To evaluate the probable imprecisions associated with the optimal model parameters (9.46), one can apply the general definition (9.11) of the variance:

```
σ_a² = Σ_{i=1}^n σ_i² (∂a/∂y_i)²,   σ_b² = Σ_{i=1}^n σ_i² (∂b/∂y_i)².
```

By using the specific expressions (9.46) of the parameters, one obtains the derivatives:

```
∂a/∂y_i = (s x_i - s_x)/(σ_i² Δ),   ∂b/∂y_i = (s_xx - s_x x_i)/(σ_i² Δ).
```

Summation over all data points yields, for example, for the variance of the parameter a:

```
σ_a² = Σ_{i=1}^n [s² x_i² - 2s x_i s_x + s_x²]/[σ_i² Δ²] = [s² s_xx - 2s s_x² + s s_x²]/Δ² = [s(s s_xx - s_x²)]/Δ² = s/Δ.
```

Proceeding similarly for the parameter b, one finally obtains the usable expressions of the probable imprecisions of the two model parameters:

```
σ_a = √(s/Δ),   σ_b = √(s_xx/Δ).   (9.47)
```

The developed formalism of linear regression can be also applied to cases of nonlinear functional dependences which admit analytic inverses. For example, the exponential model

```
y = b e^{a x}
```

can be obviously linearized by applying the logarithm and naming y' = ln y and b' = ln b:

```
y' = a x + b'.
```

The adjustment of the parameters a and b' of the linearized model is to be carried out with respect to the transformed observations y'_i = ln y_i and the optimized parameter b of the initial nonlinear model finally results as b = exp(b').

Based on the n observed coordinate pairs, received by way of the arrays x and y, and the associated standard deviations, sigmy, the routine LinFit shown in Listing 9.8 returns the adjusted parameters a and b of the linear model, as well as the associated probable imprecisions, sigma and sigm b. As a synthetic measure of the fit quality, the routine also returns by chi2 the value of the χ²-merit function calculated with the optimized model parameters.

If the control parameter iopt is set to 0, the routine initializes all the components of sigmy with 1 and the procedure falls back to the least-squares approximation based on the simple sum of squared deviations as a merit function:

```
S = Σ_{i=1}^n (y_i - a x_i - b)².   (9.48)
```