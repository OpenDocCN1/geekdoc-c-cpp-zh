as

```
y = f(x_1, x_2) + \epsilon \tag{10.1}
```

where \( f \) is a nonlinear function and \( \epsilon \) is the random effect of experimental error. When \( f \) is unknown it can be approximated near the point \( (x_{10}, x_{20}) \) using the two-term Taylor series approximation, i.e.,

```
\( f(x_1, x_2) \approx f(x_{10}, x_{20}) + (x_1 - x_{10}) \frac{\partial f(x_1, x_2)}{\partial x_1} \bigg|_{x_1=x_{10}, x_2=x_{20}} + (x_2 - x_{20}) \frac{\partial f(x_1, x_2)}{\partial x_2} \bigg|_{x_1=x_{10}, x_2=x_{20}} + \frac{(x_1 - x_{10})^2}{2} \frac{\partial^2 f(x_1, x_2)}{\partial x_1^2} \bigg|_{x_1=x_{10}, x_2=x_{20}} + \frac{(x_2 - x_{20})^2}{2} \frac{\partial^2 f(x_1, x_2)}{\partial x_2^2} \bigg|_{x_1=x_{10}, x_2=x_{20}} + \frac{(x_1 - x_{10})(x_2 - x_{20})}{2} \frac{\partial^2 f(x_1, x_2)}{\partial x_1 \partial x_2} \bigg|_{x_1=x_{10}, x_2=x_{20}}, \tag{10.2} \)
```

which leads to a general quadratic equation of the form

```
y = \beta_0 + \beta_1 x_1 + \beta_2 x_2 + \beta_{11} x_1^2 + \beta_{22} x_2^2 + \beta_{12} x_1 x_2 + \epsilon \tag{10.3}
```

where \( \beta_1 = \frac{\partial f(x_1, x_2)}{\partial x_1} |_{x_1=x_{10}, x_2=x_{20}} \), etc. If the region of interest is of moderate size, this general quadratic equation will provide a good approximation to \( f \) and can be used for interpolation within this region. The general quadratic equation is quite flexible and with appropriate coefficients it can describe a wide variety of surfaces such as hilltops, valleys, rising or falling ridges, or saddle points as shown with contour plots in Figure 10.1.

With \( k \) factors or independent variables the general quadratic equation can be written in the form

```
y = \beta_0 + \sum_{i=1}^k \beta_i x_i + \sum_{i=1}^k \beta_{ii} x_i^2 + \sum \sum_{i<j} \beta_{ij} x_i x_j + \epsilon, \tag{10.4}
```

and unless the function \( f \) is known, this equation forms the basis of response surface methods. Response surface designs were created to provide data to approximate this equation, and mathematical tools were created to explore the fitted surface represented by this equation.