
```
double SphereGlobalFunction(double x)
{
    return x*x;
}
```

The output is:

```
Function Ackley, x and y values: -30, -8048.57
Function Rastrigin, x and y values: 2.87297e-08, 1.40831e-10
Function Sphere, x and y values: 2.84217e-14, 8.07794e-28
Function Test, x and y values: 8.09975e-21, 6.5606e-41
```

In general, many benchmark multivariate optimisation examples in the literature have been designed to produce the easily checked results:

```
f(x*) = 0,  where x* = (x*_0, ..., x*_{n-1}),    x*_j = 0,    j = 0, ..., n - 1.      (A2.13)
```

## A2.6 MULTIVARIATE OPTIMISATION

We conclude this appendix with a short overview of multivariate optimisation, which is a generalisation of the one-dimensional methods to n independent variables. We focus on the steepest ascent (descent) method, set up a basic software framework and give some examples for two-factor problems.

## A2.7 NONLINEAR PROGRAMMING AND MULTIVARIABLE OPTIMISATION

In this section we introduce the mathematical formulation of unconstrained multivariable optimisation problems (minimise or maximise a given objective function).

Consider the scalar function F : ℝⁿ → ℝ¹, n ≥ 1 that maps n-dimensional Euclidean space into the real line. In general, we wish to find a point x in Euclidean space that minimises or maximises this function. The general optimisation problem is to find a real number z such that:

```
optimise  z = F(x),    x = (x₁, ..., xₙ)ᵀ.      (A2.14)
```

Here F is called the objective function and the problem is unconstrained because there are no restrictions placed on x. We note that maximisation of F(x) is the same as the minimisation of its additive inverse − F(x). In the main, we are usually interested in minimisation problems.

We now introduce some terms. The gradient function ∇F associated with F = F(x₁, ..., xₙ) is a vector defined by:

```
∇F = ( ∂F/∂x₁, ..., ∂F/∂xₙ )ᵀ.      (A2.15)
```

The Hessian matrix $H_F$ associated with $F$ is defined as:

$$H_F = \left( \frac{\partial^2 F}{\partial x_i \partial x_j} \right), \quad i,j = 1,\dots,n. \tag{A2.16}$$

We take a simple example and to this end we consider the case $n = 2$. Let $F(x) = x_1^2 + x_2^2$. Then:

$$\nabla F(x) = (2x_1,\ 2x_2)^\top$$ $$H_F = \begin{pmatrix} 2 & 0 \\ 0 & 2 \end{pmatrix}.$$

We discuss two methods to solve problem (A2.14). First, the method of steepest descent defines an iterative scheme to compute a sequence of values:

$$x_{k+1} = x_k + \lambda_k^* \nabla F(x_k), \quad k = 0,1,2,\dots \tag{A2.17}$$

where $x_0$ is an initial vector and $\lambda_k^*$ is a positive scalar that minimises $F(x_k + \lambda \nabla F(x_k))$. This single-variable problem can be solved using Brent's method or a sequential search technique, for example, and in this case finding a local minimum is acceptable. The iterative process in equation (A2.17) terminates if and when the difference (in some norm) between the values of the solution at two successive iterates is smaller than a prescribed tolerance. The last computed $x$-vector is taken as the final approximation to the solution $x^*$ of problem (A2.14).

Another approximation is the Newton–Raphson method. Again, we choose an initial vector $x_0$. We then generate a sequence of vectors by the following iterative scheme:

$$x_{k+1} = x_k + H_F(x_k)^{-1} \nabla F(x_k), \quad k = 0,1,2,\dots \tag{A2.18}$$

where $H_F$ is defined in equation (A2.16).

The stopping criterion is the same as in scheme (A2.17). The scheme (A2.18) converges to a local minimum if the Hessian matrix is positive definite. If the initial vector is not chosen correctly then scheme (A2.18) may not converge to a local minimum or it may not even converge at all.

We wish to extend problem (A2.14) by discussing multivariable optimisation problems with constraints. There are several kinds of constraints than can be used, for example:

- Equality constraints: $g(x) = 0.$  (A2.19)
- Inequality constraints: $g(x) \ge 0.$  (A2.20)
- Linear constraints: $\bigl(g(x) = Ax - b = 0(g_1(x),\dots,g_m(x)^\top)\bigr)$  (A2.21)

where $A$ is a constant $n \times m$ matrix, $b$ is an $m$-dimensional vector and the symbol $\top$ denotes the transpose of a vector or of a matrix. The function $g$ is given.

We now consider problem (A2.14) subject to the constraints (A2.19) and we assume that $m<n$ (that is, problem (A2.14) has fewer constraints than variables). In order to solve this problem, we form the *Lagrangian* function:

$$L(x_1,\ldots,x_n,\lambda_1,\ldots,\lambda_m)\equiv F(x)-\sum_{j=1}^{m}\lambda_jg_j(x)$$

where $\lambda_j(j=1,\ldots,m)$ are unknown constants called *Lagrange multipliers*. We then solve the system of equations:

$$\frac{\partial L}{\partial x_j}=0,\qquad j=1,\ldots,n$$

and

$$\frac{\partial L}{\partial \lambda_j}=0,\qquad j=1,\ldots,m.$$

In general, the Lagrange multiplier method is equivalent to using the constraint equations to eliminate some of the $x$-variables from the objective function and then solving an unconstrained minimisation problem in the remaining variables.

It is possible to solve system (A2.22) using the Newton–Raphson method. To this end, we define the extended vector $z=(x_1,\ldots,x_n,\lambda_1,\ldots,\lambda_m)$ and then we define the scheme:

$$z_{k+1}=z_k+H_L(z_k)^{-1}\nabla L(z_k),\qquad k=0,1,2,\ldots$$

The problem with this scheme is that it is difficult to find an initial vector and if it is incorrect then the Newton–Raphson method will not converge to the correct value or the method may even diverge. Other methods for solving system (A2.22) are discussed in Scales (1985) and Bronson and Naadimuthu (1997).

## A2.8 NONLINEAR LEAST SQUARES

We now discuss a special class of objective function (A2.14), namely when the function $F(x)$ is the sum of squares of other nonlinear functions:

$$F(x)=\sum_{j=1}^{m}f_j^2(x)$$

where:

$$x\in\mathbb{R}^n\text{ and }f(x)=(f_1(x),\ldots,f_m(x))^{\mathsf T}.$$

The minimisation of functions of this kind is called *nonlinear least squares*. We see that the objective function can never take negative values for these kinds of problems. We can write equation (A2.14) in the equivalent form:

F(x) = fᵀ(x)f(x)  (A2.27)

when fᵀ is the transpose of f.

### A2.8.1 Basic Algorithm and C++ Code

We now show how we implemented the method of steepest descent as described by equation (A2.17). We mention that steepest descent finds a function minimum while steepest ascent computes a function maximum (you can turn the latter problem into the former problem by simply changing the sign of the objective function).

We describe what we need to do in order to implement the algorithm for equation (A2.17). First, we define uniform function wrappers for functions that map a vector to a scalar (*real-valued functions*) and functions that map vectors into vectors (*vector-valued functions*):

```
#include <boost/numeric/ublas/vector.hpp>
#include <boost/numeric/ublas/io.hpp>

namespace u = boost::numeric::ublas;

// Function categories used in optimisation
using FunctionType
    = std::function<double (const u::vector<double>&)>;
using GradientType
    = std::function<u::vector<double> (const u::vector<double>&)>;
```

The next step is to design a C++ class to implement the steepest descent method. The members and constructor of an *initial version* are:

```
class SteepestDescent
{ // Classic steepest descent method

private:

    FunctionType func;          // Function + gradient

    GradientType grad;

    u::vector<double> Xk;       // Value at iteration k
    u::vector<double> X0;       // Initial seed
    u::vector<double> XkP1;     // Value at iteration k+1
    u::vector<double> gXk;      // Gradient at iteration k

    double minV, maxV;          // Bracket for Brent method
    double TOL;                 // Tolerance
```

And it uses the following member functions:

```
const u::vector<double>& result() const
{ // Updated value

    return XkP1;
}
```

```
double operator () (double x) const
{ // Function call operator (needed for Brent)

    return func(Xk + (x * gXk));
}
```

Finally, information pertaining to the efficiency and accuracy of the algorithm is given by a reporting function:

```
void Statistics() const
{ // Both strategic and operational reporting

    std::cout << "**** Steepest descent statistics ****" << "\n\n";
    std::cout << "*TOL and [min, max] for Brent: " << TOL
              << ", [" << minV << ", " << maxV << "]" << '\n';
    std::cout << "*Error and number of iterations needed: "
              << error << ", " << errors.size() << "\n\n";

    int n = 11;
    for (auto error : errors)
    {
        std::cout << "(" << n++ << "," << error << ")";
    }

    std::cout << "\nInitial guess: " << X0 << '\n';
    std::cout << "Final result: " << result() << '\n';

    std::cout << "Function value: " << func(result()) << '\n';

    std::cout << '\n';
}
```

### A2.8.2 Examples

We give a single example to show how to use the algorithm:

x = F(x, y) = sin(x + y),    y = G(x, y) = cos(x − y)    (A2.28)

or in least squares form:

min_{(x,y)} ((x − sin(x + y))² + (y − cos(x − y))²).    (A2.29)
