refer the reader to Bevington and Robinson (2002); Press et al. (1994); Thompson (1992). However, we will emphasize three points:

+   1. If the data being fit contain errors, then the “best fit” in a statistical sense should not pass through all the data points.
+   2. If the theory is not an appropriate one for the data (e.g., the parabola in Figure 7.5), then its best fit to the data may not be a good fit at all. This is good, for this is how we know that the theory is not right.
+   3. Only for the simplest case of a linear least-squares fit, can we write down a closed-form solution to evaluate and obtain the fit. More realistic problems are usually solved by trial-and-error search procedures, sometimes using sophisticated subroutine libraries. However, in Section 7.8.2 we show how to conduct such a nonlinear search using familiar tools.

Imagine that you have measured N_D data values of the independent variable y as a function of the dependent variable x:

```
(x_i, y_i ± σ_i) ,    i = 1, N_D ,    (7.41)
```

where ±σ_i is the experimental uncertainty in the i-th value of y. (For simplicity we assume that all the errors σ_i occur in the dependent variable, although this is hardly ever true (Thompson, 1992)). For our problem, y is the number of decays as a function of time, and x_i are the times. Our goal is to determine how well a mathematical function y = g(x) (also called a theory or a model) can describe these data. Additionally, if the theory contains some parameters or constants, our goal can be viewed as determining the best values for these parameters. We assume that the theory function g(x) contains, in addition to the functional dependence on x, an additional dependence upon M_p parameters {a_1, a_2, ..., a_Mp}. Notice that the parameters {a_m} are not variables, in the sense of numbers read from a meter, but rather are parts of the theoretical model, such as the size of a box, the mass of a particle, or the depth of a potential well. For the exponential decay function (7.40), the parameters are the lifetime τ and the initial decay rate dN(0)/dt. We include the parameters as

```
g(x) = g(x; {a_1, a_2, ..., a_Mp}) = g(x; {a_m}) ,    (7.42)
```

where the a_i's are parameters and x the independent variable. We use the chi-square (χ²) measure (Bevington and Robinson, 2002) as a gauge of how well a theoretical function g reproduces data:

```
χ² ≡ Σ_{i=1}^{N_D} ( (y_i - g(x_i; {a_m})) / σ_i )² ,    (7.43)
```

where the sum is over the N_D experimental points (x_i, y_i ± σ_i). The definition (7.43) is such that smaller values of χ² are better fits, with χ² = 0 occurring if the theoretical curve went through the center of every data point. Notice also