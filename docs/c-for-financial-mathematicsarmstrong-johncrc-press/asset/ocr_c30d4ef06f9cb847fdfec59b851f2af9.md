As an example, suppose that we want to write a function that takes parameters $a$, $b$ and $c$ and then computes

$$\int_{0}^{1}(ax^{2}+bx+c)\mathrm{d}x$$

using the trapezium rule. We will first need to write a function object to compute the integrand $ax^{2}+bx+c$. We can then compute the integral using our \texttt{integrate} function.

Here is the long answer which doesn't use lambda functions:

```
"""
class QuadraticFunction {
public:
/* Members */
double a;
double b;
double c;
/* Constructor */
QuadraticFunction(double a,
double b,
double c) :
a(a), b(b), c(c) {}
/* Operator */
double operator()(double x) {
return a*x*x+b*x+c;
}
};

double integrateQuadratic(double a,
double b,
double c) {
QuadraticFunction integrand(a, b, c);
return integrate(integrand, 0, 1, 1000);
}
"""
```

We have to define a class, give it appropriate member variables and a constructor, and override the operator $()$. We then need to construct an instance of this class and pass it to \texttt{integrate}. A lambda function allows us to do all of this in only a few lines.

```
"""
double integrateQuadratic2(double a,
double b,
double c) {
auto lambda =
[a, b, c](double x) {
return a*x*x + b*x + c;
};
"""
```