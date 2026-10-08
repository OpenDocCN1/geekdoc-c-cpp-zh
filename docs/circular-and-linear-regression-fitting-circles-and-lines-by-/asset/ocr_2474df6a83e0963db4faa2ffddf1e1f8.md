tions of the true values $\tilde{y}_i = g(x_i; \tilde{\Theta})$, i.e.

```
$y_i = g(x_i; \tilde{\Theta}) + \varepsilon_i, \quad i = 1, \ldots, n$
```

where $\tilde{\Theta}$ stands for the true (but unknown) value of $\Theta$, and (small) errors $\varepsilon_i$ are independent normally distributed random variables with zero mean and, in the simplest case, common variance $\sigma^2$. Then the joint probability density function is

```
$f(y_1, \ldots, y_n) = \frac{1}{(2\pi\sigma^2)^{n/2}} \exp \left[ -\frac{1}{2\sigma^2} \sum_{i=1}^{n} \left(y_i - g(x_i; \Theta)\right)^2 \right]$,
```

so the log-likelihood function is

```
$\log L(\Theta, \sigma^2) = - \ln(2\pi\sigma^2)^{n/2} - \frac{1}{2\sigma^2} \sum_{i=1}^{n} [y_i - g(x_i; \Theta)]^2. \qquad (1.1)$
```

Thus the maximum likelihood estimate $\hat{\Theta}$ of $\Theta$ is obtained by minimizing the sum of squares

```
$\mathscr{F}(\Theta) = \sum_{i=1}^{n} [y_i - g(x_i; \Theta)]^2$, \qquad (1.2)
```

which leads us to the classical least squares. This method for solving regression problems goes back to C.-F. Gauss [69] and A.-M. Legendre [121] in the early 1800s. It is now a part of every standard undergraduate statistics course.

![](bbox=[0.38, 0.54, 0.64, 0.69])

Figure 1.1 Ordinary regression minimizes the sum of squares of vertical distances: a cubic polynomial fitted to 10 data points.

We emphasize that the x and y variables play different roles: x is called a control variable (controlled by the experimenter), its values $x_1, \ldots, x_n$ are error-free, and y is called a response variable (observed as a response), its values $y_1, \ldots, y_n$ are imprecise (contaminated by noise). Geometrically, the regression procedure minimizes the sum of squares of vertical distances (measured along the y axis) from the data points $(x_i, y_i)$ to the graph of the function $y = g(x; \Theta)$, see Fig. 1.1.