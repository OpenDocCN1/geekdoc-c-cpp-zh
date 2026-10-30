```
```text
> Hf := Hessian(f(x1,x2), [x1,x2]);
  IsDefinite(Hf, query = 'positive_definite');
  IsDefinite(Hf, query = 'negative_definite');
  IsDefinite(Hf, query = 'indefinite');

                         Hf := [ 2  0 ]
                               [ 0  6 ]
                               true
                               false
                               false

> Hg := Hessian(g(x1,x2), [x1,x2]);
  IsDefinite(Hg, query = 'positive_definite');
  IsDefinite(Hg, query = 'negative_definite');
  IsDefinite(Hg, query = 'indefinite');

                         Hg := [ -2   1 ]
                               [  1  -6 ]
                               false
                               true
                               false

> Hh := Hessian(g(x1,x2), [x1,x2]);
  IsDefinite(Hh, query = 'positive_definite');
  IsDefinite(Hh, query = 'negative_definite');
  IsDefinite(Hh, query = 'indefinite');

                         Hh := [ 2   1 ]
                               [ 1  -6 ]
                               false
                               false
                               true
```
```

Maple has a number of functions that compute the Hessian of a function. Versions of the *Hessian* command are in the *Student[VectorCalculus], Vector-Calculus,* and *LinearAlgebra* packages. Consult Maple’s Help pages to help you decide which version is best to use in a given situation.

In a more general setting, if a function has terms with power higher than 2 or includes transcendental functions, such as $x_1x_2^2$ or $\sin(x_1x_2)$, the Hessian will have terms with variables. Then the analysis of definiteness for classifying a stationary point as a maximum, minimum, or saddle point is a bit more complicated.

For two variables, we use the *quadratic form*

$$Q(x_1,x_2) = [x_1\quad x_2] \times H \times \begin{bmatrix}x_1\\x_2\end{bmatrix}$$

to test the Hessian matrix. In general, we use $Q(\vec{x}) = \vec{x}^{T}H\,\vec{x}$. Then define