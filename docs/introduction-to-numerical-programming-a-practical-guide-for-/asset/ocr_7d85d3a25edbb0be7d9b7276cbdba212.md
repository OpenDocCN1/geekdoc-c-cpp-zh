chosen to be a polynomial $P_m(x)$, with the number of coefficients not exceeding the number of tabulation nodes $(m+1 \le n)$ and satisfying the interpolation conditions:

$$P_m(x_i)=y_i,\quad i=1,2,\ldots,n.$$

From this equation set, one can determine the polynomial coefficients and the approach is called *polynomial interpolation*.

Predominating in practice are the polynomial interpolants and, from among them, the most frequent are the *Lagrange polynomial* and the *cubic splines*. Using trigonometric functions, instead of the polynomial basis set $1, x, x^2, \ldots$, leads to the so-called *trigonometric interpolation* and, also, to the related Fourier transform methods.

**Regression.** If the tabulated values $y_i=f(x_i)$ originate from observations, they are typically affected by *measurement errors*, which are usually specified as *standard deviations* $\sigma_i$ (see Figure 9.1b). In such cases, the less empirical the considerations by which the model function $F=F(x;\mathbf{a})$ is established, the higher the statistical significance of the obtained model parameters. Having in view the inherent inaccuracies of the observed data, the model function is not actually expected to interpolate the data points, that is, to pass rigorously through them (even though this may, in principle, happen). It is rather natural to impose the *minimization* of the distance with respect to the set of parameters $\{a_j\}$,

$$d(f,F)=\min_{\{a_j\}},$$

not its rigorous vanishing (like for interpolation). Concretely, this amounts to considering a model function belonging to a certain continuity class (with continuous derivatives up to a certain order) and determining the $m$ parameters $a_j$ that minimize the sum of squared deviations of its values from the data points:

$$S=\sum_{i=1}^{n}\left[y_i-F(x_i;\mathbf{a})\right]^2.$$

The approach of adjusting (optimizing) the model parameters is called *regression* or *curve fitting* by the *method of least squares*. The functional (9.7) represents in a broader sense a so-called *function of merit*. By convention, merit functions are defined in such a way that lower values indicate a better agreement between the model and observations. Regression can be regarded in this respect as a *multidimensional minimization procedure*.

The merit function used most commonly in practice is the *chi-square functional*:

$$\chi^2=\sum_{i=1}^{n}\frac{1}{\sigma_i^2}\left[y_i-F(x_i;\mathbf{a})\right]^2.$$

Unlike the simple sum of squared deviations $S$ (Equation 9.7), the observed data enter the $\chi^2$-merit function with different weights, namely, inverse proportional to the individual standard deviations $\sigma_i$. The relative weights of the data points affected by lower errors are thereby increased, “forcing” the model function $F(x;\mathbf{a})$ to minimize predominantly the distances with respect to these, at the expense of the less accurate observations (with larger $\sigma_i$’s). In particular, in the case of equal or unknown precisions $\sigma_i$, the formalism simplifies and falls back to the regression based on the $S$ merit function.

The minimum of the $\chi^2$ functional with respect to the model parameters $a_j$ is characterized by the conditions:

$$\frac{\partial\chi^2}{\partial a_j}=0,\quad j=1,2,\ldots,m.$$