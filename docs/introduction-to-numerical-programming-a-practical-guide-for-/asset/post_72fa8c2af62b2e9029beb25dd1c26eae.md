
# Listing 9.7 Interpolation Using Cubic Splines (Python Coding)

```
# Interpolation with cubic splines
from modfunc import *

def sinc(x): return (sin(x)/x if x else 1e0)

# main

xmin = 0e0; xmax = 5*asin(1e0)                     # tabulation interval: [0,5*pi/2]
n = 6                                             # number of data points
ni = 100                                          # number of interpolation points

a = [0]*(n+1); b = [0]*(n+1)                      # spline coefficients
c = [0]*(n+1); d = [0]*(n+1)
x = [0]*(n+1); y = [0]*(n+1)                       # data points

h = (xmax-xmin)/(n-1)                             # generate data points
for i in range(1,n+1):
    xi = xmin + (i-1)*h
    x[i] = xi; y[i] = sinc(xi)

Spline(x,y,n,0e0,0e0,0,a,b,c,d,x,y,0)             # natural splines

out = open("interpol.txt","w")                  # open output file
out.write("        x            y            xi            yi      " +
          "            y1            y2            f\n")
h = (xmax-xmin)/(ni-1)
for i in range(1,ni+1):
    xi = xmin + (i-1)*h                           # interpolation argument
    ip = 1
    while (ip < n-1 and xi > x[ip+1]): ip += 1    # index of spline

    yi = ((a[ip]*xi + b[ip])*xi + c[ip])*xi + d[ip]          # spline
    y1 = (3*a[ip]*xi + 2*b[ip])*xi + c[ip]                   # 1st derivative
    y2 = (6*a[ip]*xi + 2*b[ip])                              # 2nd derivative

    if (i <= n):
        out.write(
          "{0:12.3e}{1:12.3e}{2:12.3e}{4:12.3e}{5:12.3e}{6:12.3e}\n".
          format(x[i],y[i],xi,yi,y1,y2,sinc(xi)))
    else:
        out.write("{0:36.3e}{1:12.3e}{2:12.3e}{3:12.3e}{4:12.3e}\n".
          format(xi,yi,y1,y2,sinc(xi)))
out.close()
```

On the other hand, however, insufficient interpolated data points, especially in regions of pronounced variations, may lead even for spline interpolants to deficient approximations. One such example is depicted in Figure 9.4 and shows in the case of the function f(x) = 1/x^12 − 10^4/x^6 that, due to the sparse tabulation mesh, the spline cannot reproduce in the left-most subinterval both the appreciable slope and the curvature.

Besides the density of the interpolated data points, the quality of the spline interpolation is also directly affected by the way in which the first derivatives at the end points of the tabulation interval are modeled. The output produced by Program 9.7 is plotted in the left panel of Figure 9.5 and shows that natural boundaries (second derivatives implicitly set to 0) lead to visible deviations of the interpolant from

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_303_0.png)

FIGURE 9.4 Case in which the natural cubic spline deviates significantly from the modeled function due to insufficient interpolated points. The interpolated data samples the function f(x) = 1/x^12 − 10^4/x^6.

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_303_1.png)

FIGURE 9.5 Interpolation with natural cubic splines (left) and clamped cubic splines (right). The modeled dependence, f(x) = sin x / x, is sampled in the interval [0, 5π/2] with a π/2 spacing.

the true behavior of the modeled function. Quite in contrast, clamped boundaries clearly improve the matching between the interpolant and the modeled dependence (see the right panel of Figure 9.5).

## 9.5 Linear Regression

In quite a few practical situations, the plot of the observations or the theoretical framework on which the data collection is based suggests a linear functional dependence of the modeled function on the independent variable (see Figure 9.6):

F(x; a, b) = a x + b. (9.40)

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_304_0.png)

FIGURE 9.6 Linear regression based on the least-squares approximation. The parameter a of the model function represents the slope of the regression line, while b is the corresponding y-intercept.

Linear regression actually represents the simplest application of the general concepts regarding the least-squares fitting of model functions to tabulated dependences, which have been presented in Section 9.1.

Assuming the uncertainties σ_i associated with the observed values y_i to be available, the quality of the model function F(x; a, b) adjusted to the observed data may be quantified by the χ²-merit function (Equation 9.8), taking in this case the form:

χ²(a, b) = Σ_{i=1}^{n} 1/σ_i² (y_i - a x_i - b)². (9.41)

The optimal model parameters a and b, which minimize χ², result from the condition of vanishing partial derivatives of χ² with respect to a and b:

∂χ²/∂a ≡ -2 Σ_{i=1}^{n} 1/σ_i² (y_i - a x_i - b) x_i = 0,
∂χ²/∂b ≡ -2 Σ_{i=1}^{n} 1/σ_i² (y_i - a x_i - b) = 0. (9.42)

By introducing the notations for the involved sums

s = Σ_{i=1}^{n} 1/σ_i²,  s_x = Σ_{i=1}^{n} x_i/σ_i²,  s_xx = Σ_{i=1}^{n} x_i²/σ_i²,  s_y = Σ_{i=1}^{n} y_i/σ_i²,  s_xy = Σ_{i=1}^{n} x_i y_i/σ_i², (9.43)

one obtains the simplified system:

{ s_xx a + s_x b = s_xy
  s_x a + s b = s_y. } (9.44)

With the additional notation

Δ = s s_xx - s_x², (9.45)

the solution of the system provides the values of the optimized model parameters:

a = (s s_xy - s_x s_y)/Δ,  b = (s_y s_xx - s_x s_xy)/Δ. (9.46)

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

## Listing 9.8 Linear Regression (Python Coding)

```
# =================================================================================
def LinFit(x, y, sigmy, n, iopt):
# ---------------------------------------------------------------------------------
# Determines the coefficients a and b of a linear model P(x;a,b) = a * x + b
# and the associated uncertainties, sigma and sigmb, for a set of observed
# data points by "Chi-square" regression
# x[]      - x-coordinates of observed data, i = 1,..,n
# y[]      - y-coordinates of observed data
# sigmy[]  - standard deviations of observed data
# n        - number of observed data points
# iopt     - iopt == 0 - initializes sigmy[i] = 1 (equal weights)
#            iopt != 0 - uses the received values of sigmy[i]
# a, b     - parameters of the linear model (output)
# sigma    - uncertainties associated with the model parameters (output)
# sigmb    - value of Chi-square merit function for the output parameters
# ---------------------------------------------------------------------------------
    if (iopt == 0):
        for i in range(1,n+1): sigmy[i] = 1e0        # iopt = 0: equal weights

    s = sx = sy = sxx = sxy = 0e0                        # prepare sums
    for i in range(1,n+1):
        f = 1e0/(sigmy[i]*sigmy[i])
        s += f
        sx += x[i] * f; sxx += x[i] * x[i] * f
        sy += y[i] * f; sxy += x[i] * y[i] * f

    f = 1e0/(s*sxx - sx*sx)
    a = (s *sxy - sx*sy ) * f; sigma = sqrt(s*f)        # model parameters
    b = (sy*sxx - sx*sxy) * f; sigmb = sqrt(sxx*f)      # and uncertainties

    chi2 = 0e0                                          # value of Chi-square function
    for i in range(1,n+1):
        f = (y[i] - a*x[i] - b)/sigmy[i]
        chi2 += f*f

    return (a, b, sigma, sigmb, chi2)
```

This option is typically useful in situations in which the standard deviations σi of the observed data are unknown. Anyway, it should be noted that the comparative use of the two merit functions, χ² and S, may lead to rather different regression lines.

In the example shown in Figure 9.7, the merit function S, not making use of observational errors σi and assigning equal weights to all observed data, yields a regression line not passing through all the error bars. In contrast, by applying the χ²-regression and considering, for the sake of simplicity, errors σi proportional to the observed values yi (a somewhat typical situation), the first data point, bearing the lowest imprecision, forces the regression line to pass also through its error bar.

Specifically, the coordinates of the tabulated data points are (1,0.8), (2,2.1), (3,2.8), (4,4.0), and (5,4.4), and the corresponding standard deviations are generated simply as σi = 0.15 yi. By using the functional S one obtains the model parameters a = 0.9100 and b = 0.0900, while for the χ²-merit function, the values a = 0.9983 and b = −0.1681 result.
