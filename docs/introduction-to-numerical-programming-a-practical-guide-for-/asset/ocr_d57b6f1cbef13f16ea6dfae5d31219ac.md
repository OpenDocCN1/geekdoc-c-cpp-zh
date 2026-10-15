Unlike the first and second derivatives, the third derivatives (equal to 6A_i) are discontinuous at the subinterval boundaries.

The second spline derivative, S_i''(x), is a linear function defined in the interval [x_i, x_{i+1}] by the equation

$$\frac{S_i''(x) - \tilde{D}_i}{x - x_i} = \frac{\tilde{D}_{i+1} - \tilde{D}_i}{x_{i+1} - x_i}, \tag{9.27}$$

where $\tilde{D}_i \equiv S''(x_i)$ and $\tilde{D}_{i+1} \equiv S''(x_{i+1})$ are the boundary values of the second derivative. From this equation, one may express

$$S_i''(x) = \frac{\tilde{D}_{i+1}(x - x_i) + \tilde{D}_i(x_{i+1} - x)}{h_i}, \tag{9.28}$$

with

$$h_i = x_{i+1} - x_i, \quad i = 1,2,\dots,n-1. \tag{9.29}$$

Integrating Equation 9.28 twice, one obtains successively the first derivative and the spline itself:

$$S_i'(x) = \frac{\tilde{D}_{i+1}(x - x_i)^2 - \tilde{D}_i(x_{i+1} - x)^2}{2h_i} + C_i', \tag{9.30}$$ $$S_i(x) = \frac{\tilde{D}_{i+1}(x - x_i)^3 + \tilde{D}_i(x_{i+1} - x)^3}{6h_i} + C_i'x + C_i''. \tag{9.31}$$

The integration constants $C_i'$ and $C_i''$ may be determined by imposing on the spline the interpolation conditions at the nodes $x_i$ and $x_{i+1}$, that is,

$$S_i(x_i) = y_i, \quad S_i(x_{i+1}) = y_{i+1},$$

which result in the system:

$$\begin{cases}\frac{\tilde{D}_i h_i^2}{6} + C_i' x_i + C_i'' = y_i \\ \frac{\tilde{D}_{i+1} h_i^2}{6} + C_i' x_{i+1} + C_i'' = y_{i+1}.\end{cases}$$

Solving this system for $C_i'$ and $C_i''$ yields

$$C_i' = \frac{y_{i+1} - y_i}{h_i} - \frac{(\tilde{D}_{i+1} - \tilde{D}_i)h_i}{6}, \tag{9.32}$$ $$C_i'' = \frac{x_{i+1}y_i - x_i y_{i+1}}{h_i} + \frac{(x_i \tilde{D}_{i+1} - x_{i+1} \tilde{D}_i)h_i}{6}. \tag{9.33}$$

Upon replacement of the integration constants back into Equation 9.31 and collection of the equal powers of $x$, one obtains the polynomial coefficients of the spline $S_i(x)$ in terms of the second derivatives $D_i$ at