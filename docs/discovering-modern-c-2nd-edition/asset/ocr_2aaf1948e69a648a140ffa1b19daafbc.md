In this exercise, we develop a function for the trapezoid rule with a functor and the limits as arguments. For comparison, implement this using inheritance and generic programming. As a test case, integrate:

+   • f = exp(3x) for x ∈ [0, 4]. Try trapezoid with the following arguments:

Click here to view code image

```
double exp3f(double x) {
    return std::exp(3.0 * x);
}

struct exp3t {
    double operator() (double x) const {
        return std::exp(3.0 * x);
    }
};
```

+   • f = sin(x) if x < 1 and f = cos(x) if x ≥ 1 for x ∈ [0, 4].

+   • Can we call trapezoid( std::sin, 0.0, 2.0 ) ?

As a second exercise, develop a functor for computing the finite difference. Then integrate the finite difference to verify that you get the function value back.

# 3.12.11 Partial Specialization with a static Function

Implement the specialized abs functionality from Section 3.5.4 with a static function named eval and call this function without creating a class object.

# 3.12.12 Functor

Write a functor for 2 cos x+x^2 and compute the first and second derivatives with the functor from Section 3.7.1.

# 3.12.13 Lambda

Compute the same derivatives as in Exercise 3.12.12 but this time with a lambda expression.