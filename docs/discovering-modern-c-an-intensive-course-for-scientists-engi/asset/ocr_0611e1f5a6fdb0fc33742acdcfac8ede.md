# 3.11.8 Stack with Custom Size

Revise your stack implementation from Exercise 3.11.3 (and optionally that of Exercise 3.11.7) with a user-defined size. The size is passed as the second template argument. The default should be 4096.

# 3.11.9 Deducing Non-type Template Arguments

We have seen that the type of a template argument can be deduced in a function call. Non-type template arguments are in most cases declared explicitly, but they can be deduced as well when they are part of the argument type. As illustration, write a function array_size that accepts a C array of arbitrary type and size as a reference and returns the size of that array. The actual function argument can be omitted since we are only interested in its type. Do you remember? We threatened this exercise in Section 1.8.7.1. On the other hand, we revealed the trickiest part of it in the meantime.

# 3.11.10 Trapezoid Rule

A simple method for computing the integral of a function is the trapezoid rule. Suppose we want to integrate the function f over the interval [a, b]. We split the interval in n small intervals [x_i, x_{i+1}] of the same length h = (b - a)/n and approximate f by a piecewise linear function. The integral is then approximated by the sum of the integrals of that function.

This leads to the following formula:

```
I = \frac{h}{2}f(a) + \frac{h}{2}f(b) + h \sum_{j=1}^{n-1} (f(a + jh) \quad (3.1)
```

In this exercise, we develop a function for the trapezoid rule, with a functor argument. For comparison, implement this using inheritance and generic programming. As a test case, integrate:

+   f = exp(-3x) for x in [0, 4]. Try trapezoid with the following arguments:

```
double exp3f(double x) {
    return std::exp(3.0 * x);
}
```

```
struct exp3t {
    double operator() (double x) const {
        return std::exp(3.0 * x);
    }
};
```

+   f = sin(x) if x < 1 and f = cos(x) if x >= 1 for x in [0, 4].

+   Can we call trapezoid( std::sin, 0.0, 2.0 ); ?

As a second exercise, develop a functor for computing the finite difference. Then integrate the finite difference to verify that you get the function value back.