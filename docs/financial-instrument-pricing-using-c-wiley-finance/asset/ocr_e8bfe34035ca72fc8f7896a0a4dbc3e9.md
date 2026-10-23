We have implemented this function in C++ by explicitly computing the inverse of the covariance matrix. We also used a more explicit form for the probability density function:

f(b1, b2, b3; Σ)
= e^{-w} / [2(ρ12² + ρ13² + ρ23²) − 2ρ12ρ13ρ23] √2π^{3/2} √[1 − (ρ12² + ρ13² + ρ23²) + 2ρ12ρ13ρ23]  (16.13)

where:

w = b1²(ρ23² − 1) + b2²(ρ13² − 1) + b3²(ρ12² − 1) + 2[b1b2(ρ12 − ρ13ρ23) + b1b3(ρ13 − ρ12ρ23) + b2b3(ρ23 − ρ12ρ13)].

The code for this function is:

```
double f(double x, double y, double z, double a12, double a13, double a23)
{
    double q = 2.0*(a12*a12 + a13*a13 + a23*a23 - 2.0*a12*a13*a23 - 1.0);

    // Covariance matrix must be positive semi-definite
    double tmp = 1.0 - (a12*a12 + a13*a13 + a23*a23) + 2.0*a12*a13*a23;
    if (tmp <= 0.0)
        return std::numeric_limits<double>::max();

    double fac = std::sqrt(tmp);

    double fac2 = 2.0*std::sqrt(2.0)*std::pow(3.14159, 1.5);
    // x = b, y = b2. Z = b3

    double w = x*x*(a23*a23 - 1.0) + y*y*(a13*a13 - 1.0) + z*z*(a12*a12 - 1.0)
        2.0*(x*y*(a12 - a13*a23) + x*z*(a13 - a12*a23) + y*z*(a23 - a12*a13));

    return std::exp(-w / q) / (fac2 * fac);
}
```

When testing the finite difference code we used both forms for the probability density function when computing the integral in equation (16.12).

Similar to the two-dimensional case we can differentiate the integral to produce a third-order hyperbolic PDE:

∂³u / ∂x∂y∂z = f.  (16.14)

We solve (16.14) by a finite difference method that is the three-dimensional analogue of scheme (16.6):

V_{i,j,k} = V_{i-1,j,k} + V_{i,j-1,k} − V_{i-1,j-1,k} + V_{i,j,k-1} − V_{i-1,j,k-1} − V_{i,j-1,k-1} + V_{i-1,j-1,k-1} + h_x h_y h_z f_{i-1/2,j-1/2,k-1/2}  (16.15)