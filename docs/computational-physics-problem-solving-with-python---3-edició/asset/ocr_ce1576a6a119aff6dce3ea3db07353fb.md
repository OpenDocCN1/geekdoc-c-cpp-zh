where we have made the change of variable $y_i \to a_i$ for the present problem. We use that same formalism here for the $N = 3$ Equation 7.69 by writing them as

```
$f_1(a_1, a_2, a_3) = \sum_{i=1}^{9} \frac{y_i - g(x_i, a)}{(x_i - a_2)^2 + a_3} = 0 , \qquad (7.71)$
```

```
$f_2(a_1, a_2, a_3) = \sum_{i=1}^{9} \frac{\{y_i - g(x_i, a)\}(x_i - a_2)}{[(x_i - a_2)^2 + a_3]^2} = 0 , \qquad (7.72)$
```

```
$f_3(a_1, a_2, a_3) = \sum_{i=1}^{9} \frac{y_i - g(x_i, a)}{[(x_i - a_2)^2 + a_3]^2} = 0 . \qquad (7.73)$
```

Because $f_r \equiv a_1$ is the peak value of the cross section, $E_R \equiv a_2$ is the energy at which the peak occurs, and $\Gamma = 2\sqrt{a_3}$ is the full width of the peak at half-maximum, good guesses for the $a$'s can be extracted from a graph of the data. To obtain the nine derivatives of the three $f$'s with respect to the three unknown $a$'s, we use two nested loops over $i$ and $j$, along with the forward-difference approximation for the derivative

```
$\frac{\partial f_i}{\partial a_j} \simeq \frac{f_i(a_j + \Delta a_j) - f_i(a_j)}{\Delta a_j} , \qquad (7.74)$
```

where $\Delta a_j$ corresponds to a small, say $\le 1\%$, change in the parameter value.

# Nonlinear Fit Implementation

Use the Newton–Raphson algorithm as outlined in Section 7.8.2 to conduct a nonlinear search for the best-fit parameters of the Breit–Wigner theory (7.64) to the data in Table 7.1. Compare the deduced values of $(f_r, E_R, \Gamma)$ to that obtained by inspection of the graph.