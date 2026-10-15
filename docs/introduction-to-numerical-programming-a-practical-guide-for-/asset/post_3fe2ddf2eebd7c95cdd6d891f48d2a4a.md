
## Modeling of Tabulated Functions

### 9.1 Interpolation and Regression

The necessity of modeling incompletely known or biased functional dependences occurs in rather diverse numerical contexts, the variety of developed formulations and methods being a direct reflection thereof.

Quite often in numerical applications, functions need to be used for which the mere values on a discrete mesh of points are known. Such discontinuous dependences can represent, for instance, tabulations of mathematical functions or measured physical quantities. For the sake of simplicity, we confine the discussion to real-valued dependences of a single real variable. In such cases, a function defined on some real interval,

$f : [\alpha, \beta] \to \mathbb{R}, \quad [\alpha, \beta] \subset \mathbb{R}, \tag{9.1}$

is specified by its values $y_i$ at a certain number of mesh points $x_i \in [\alpha, \beta]$:

$f(x_i) = y_i, \quad i = 1, 2, \dots, n. \tag{9.2}$

The numerical processing of such dependences requires rather frequently the use of supplementary values corresponding to arguments differing from those of the tabulation. Alas, obtaining additional information on the dependence is in many situations difficult, if at all possible. In particular, even if the algorithm is known, its complexity may render the direct computation of certain functions too expensive in large-scale computations. On the other hand, if the tabulated values stem from observations, they are typically affected by measurement (observational) errors.

With a view to synthesizing the information on a tabulated dependence $f$ and using it efficiently in further calculations, it is a common practice to approximate it by a continuous function, called model function, $F = F(x; a_1, \dots, a_m)$, which generally depends on a certain number of adjustable model parameters, $a_j$. The functional form of the model $F$ and the values of the parameters $a_j$ enjoy a certain freedom, but have to be determined, anyway, so as to approximate the discrete function $f$ optimally in a predefined sense.

The concrete choice of the model function $F$ is, indeed, a nontrivial task and it should be based, in as much as possible, on a rigorous reasoning. Broadly speaking, the following options are available:

- The model function is selected from a convenient class (such as polynomials, Gaussian functions, etc.), which ensures simplicity and efficiency in the postprocessing.
- The model function is derived from a theoretical framework, within which the parameters have well-defined significances.
- The model function results from a compromise between the constraints and advantages of the previous options.

To determine optimal model parameters, one has to define first a functional reflecting the degree to which the model function $F$ approximates the tabulated dependence $f$. Admitting that, as commonly encountered, both $f$ and $F$ are square integrable functions on $[\alpha, \beta]$ (the integral of their squares is finite),

a useful synthetic measure of the deviation of the model function from the modeled function is provided by the distance

```
$$d(f,F)=\left\{\int_{\alpha}^{\beta}[f(x)-F(x;\mathbf{a})]^2dx\right\}^{1/2},$$
```

where **a** ≡ (a₁, a₂,…) denotes the ensemble of model parameters. From the general statement of the modeling problem, it is obvious that this definition is actually inoperable, since it implies the knowledge of the analytical expression of f. A less rigorous definition of the distance, however applicable only to discrete functions, is

```
$$d(f,F)=\left\{\sum_{i=1}^{n}[f(x_i)-F(x_i;\mathbf{a})]^2\right\}^{1/2}.\tag{9.3}$$
```

The approach of *adjusting* the model parameters or *fitting* the model function to observed data sets based on the distance (9.3) is known as *least-squares approximation* and lies at the core of two basic methods, namely, *interpolation* and *regression.*

**Interpolation.** If the tabulated values yᵢ = f(xᵢ) are considered *error-free* or numerically *exact*, it is natural to impose a *vanishing distance* between the functions f and F:

```
$$d(f,F)=0.\tag{9.4}$$
```

This amounts to constructing a model function of a certain continuity class, which takes on *the same values* at the data nodes xᵢ as the modeled function f(x):

```
$$F(x_i;\mathbf{a})=y_i,\quad i=1,2,\dots,n.\tag{9.5}$$
```

The model function satisfying these conditions is normally used to approximate the function f(x) for interior points of the interval [x₁,xₙ] and the procedure is called *interpolation*. F(x;**a**) is called *interpolation function* or *interpolant*, while the discrete arguments xᵢ are also known as *interpolation nodes*. If the arguments for which the interpolant is evaluated lie outside the tabulation interval [x₁,xₙ], the approach is called *extrapolation.*

In geometrical terms, interpolation implies finding the curve y = F(x;**a**) which passes through *all* the data points Mᵢ(xᵢ,yᵢ) (see Figure 9.1a). With such a general statement, however, the modeling problem can have an infinity of solutions or none, depending on the continuity class to which the model function belongs. Quite in contrast, the solution becomes unambiguous if, for instance, the model function is

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_286_0.png)

FIGURE 9.1 The model function passes in the case of the interpolation through the tabulation nodes (a), while in the case of the regression, it minimizes the merit function and passes between the nodes (b). For the same data set, the interpolation and the regression curves can be significantly different.

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
