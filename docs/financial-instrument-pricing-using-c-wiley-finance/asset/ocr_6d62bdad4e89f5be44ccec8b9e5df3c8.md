It is worth noting that one of these functions returns a tuple. We stress that the use of tuples can impact performance depending on the frequency with which they are created and returned from functions.

# 13.5.1 Examples

The first example is to test cubic spline interpolation applied to the standard normal distribution. The code for the probability distribution function, its first and second derivatives as well as cumulative distribution functions is:

```
double Pdf(double x)
{ // Probability function for Gauss fn.

    double A = 1.0 / sqrt(2.0 * 3.14159265358979323846);
    return A * exp(-x*x*0.5);
}

double dPdfdx(double x)
{ // 1st derivative of probability function for Gauss fn.

    return -x * Pdf(x);
}

double d2Pdfdx2(double x)
{ // 2nd derivative of probability function for Gauss fn.

    return -Pdf(x) + x*x*Pdf(x);
}

double Cdf(double x)
{ // The approximation to the cumulative normal distribution

    // C++11
    return 0.5* (1.0 + std::erf(x / std::sqrt(2.0)));
}
```

We take these functions because they are important in computational finance and we can check our results against them. We test the accuracy of the interpolator by examining the values at a random point (we discuss random number generation in more detail in Chapter 26). The code is:

```
// Infinite interval, truncated to [a,b]
double a = -6.0;                    // Left of interval
double b = 6.0;                    // Right of interval
std::size_t n = 200000;            // N.B. n subintervals
double h = (b - a) / static_cast<double>(n);

std::vector<double> xarr = CreateMesh(n, a, b);
```