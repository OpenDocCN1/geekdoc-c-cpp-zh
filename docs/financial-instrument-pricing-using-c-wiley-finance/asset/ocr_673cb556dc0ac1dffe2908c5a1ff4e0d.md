|  | Erf | Erf c |
|+1 | +1 | + 0 |
|i 1 | -1 | 2 |
|Na N | NaN | NaN |

# FIGURE 15.1 Error handling and extreme values for the error functions

C++11 supports both the error function and the complementary error function. Both functions accept float, double, long double and integral arguments:

```
// Error functions
int i = 1;
float f = 3.0F;
double d = 3.14;
long double d2 = 2.71;
std::cout << "i, erf(x): " << i << ", " << std::erf(i) << '\n';
std::cout << "f, erf(x): " << f << ", " << std::erf(f) << '\n';
std::cout << "d, erfc(x): " << d << ", " << std::erfc(d) << '\n';
std::cout << "d2, erfc(x): " << d2 << ", " << std::erfc(d2) << '\n';
```

In Figure 15.1 we give the values of the error functions for special cases of their arguments.

The error functions are related to the cumulative distribution Φ (integral of the standard normal distribution) by the formulae:

Φ(x) ≡ N(x) = 1/2 + 1/2 erf(x/√2). (15.3)

We can check the following relationships:

erf(x) = 2Φ(x√2) − 1

erfc(x) = 2Φ(−x√2) = 2(1 − Φ(x√2)). (15.4)

The error function has many applications in statistics, probability and partial differential equations.

# 15.2.1 Approximating the Error Function

Since C++11 officially supports the error function we recommend using it instead of other approximations unless there is a good reason for not doing so. It is possible to use other approximations based on polynomials or rational functions (Abramowitz and Stegun, 1965). For example, a fifth-order polynomial approximation (called ‘26.2.16’ in Abramowitz and Stegun, 1965) for non-negative values of the argument is given by:

```
const double SQRT2PI = std::sqrt(2.0*3.14159);
const double p = 0.33267;
const double a1 = 0.4361836;
```