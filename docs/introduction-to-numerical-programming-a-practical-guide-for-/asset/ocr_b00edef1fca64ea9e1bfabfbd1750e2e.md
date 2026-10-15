variation, may result in a prohibitive computational effort in regions of reduced variation. An efficient algorithm for solving Cauchy problems for ODEs is actually expected to exert an adaptive control over the step size to achieve a targeted overall precision of the solution.

The essential information required for automatic step size control is contained in the truncation error. In the following, we discuss the simplest way of estimating the truncation error, namely by the step-halving method. To this end, we compare two estimates of the solution, \tilde{y}_{m+1} and y_{m+1}, obtained by propagating an initial solution y_m ≡ y(t_m) in a single step of size h, and, respectively, in two steps of size h/2, whereby also producing the intermediate value y_{m+1/2} for t_m + h/2. The difference between the two approximations (with y_{m+1} naturally more precise) provides useful estimates of the absolute truncation error:

```
\Delta_{m+1} = |y_{m+1} - \tilde{y}_{m+1}|, \tag{12.43}
```

and of the corresponding relative error:

```
\delta_{m+1} = \frac{\Delta_{m+1}}{|y_{m+1}|} = \left| 1 - \frac{\tilde{y}_{m+1}}{y_{m+1}} \right|. \tag{12.44}
```

The adjustment mechanism of the integration step size mainly relies on the specific order of the truncation error. From this perspective, there are basically two practical options: to take as reference the local or the global truncation error. As discussed in Section 12.3, the solution provided by an ODE solver of order p is equivalent with the Taylor series including terms up to O(h^p) and it displays, consequently, a local truncation error O(h^{p+1}) and a one order lower global truncation error O(h^p). Since, in applications, it appears to be generally more meaningful to control the global error, we associate in the following the relative error δ_{m+1} with the global truncation error and we assume it to scale with the integration step size such as:

```
\delta_{m+1} \approx K h^{p}. \tag{12.45}
```

Setting a maximum admissible error ε, one may assume that it is not exceeded for step sizes below a maximum value h_1, which is expected to be linked to ε by a dependence similar to the above one:

```
\varepsilon \approx K_1 h_1^{p}. \tag{12.46}
```

From the ratio of these two dependences, one may predict the maximum usable step size, h_1, in terms of the one effectively used, h, and the resulting error, δ_{m+1}:

```
h_1 \approx \left( \frac{\varepsilon}{\delta_{m+1}} \right)^{1/p} h. \tag{12.47}
```

If the occurring error δ_{m+1} exceeds the admissible one (δ_{m+1} > ε), this formula prescribes a reduced step size, to be used in repeating the propagation step. On the contrary, if δ_{m+1} < ε, the formula specifies an increased step size, which could have been used to propagate the solution without exceeding ε. In the latter case, there is actually no need to repeat the step, since the desired precision is already attained and the step size guess h_1 may be rather used at the next propagation step.

One should bear in mind, though, that Formula 12.47 is not an exact result and it merely provides a prediction of the step size to be used. Moreover, for rapidly varying solutions, the error estimate δ_{m+1} itself may depart significantly from its exact value. All things considered, one can further fine-tune the prediction h_1 by an ad hoc subunity factor (see for variants Burden and Faires 2010 and Press et al. 2007), aimed at causing an overall reduction of the employed step sizes.