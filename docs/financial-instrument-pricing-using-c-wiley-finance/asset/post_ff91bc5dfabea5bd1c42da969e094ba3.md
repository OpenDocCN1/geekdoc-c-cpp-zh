
```cpp
std::cout << "Number of decimal digits representable without change:" << std::numeric_limits<T>::digits10 << "\n";
std::cout << "Smallest negative power of radix valid normalised number: " << std::numeric_limits<T>::min_exponent << "\n";
std::cout << "One more than largest power of radix that gives a valid floating point value: " << std::numeric_limits<T>::max_exponent << "\n";
}

template <typename T>
void NumericFunctions(const std::string& arithType)
{
std::cout << '\n' << "**Type: " << arithType << '\n';
std::cout << "Largest finite value: " << std::numeric_limits<T>::max();
std::cout << "Smallest finite value: " << std::numeric_limits<T>::min();
std::cout << "Lowest finite value: " << std::numeric_limits<T>::min();
std::cout << "Positive infinity value: " << std::numeric_limits<T>::infinity() << "\n";
std::cout << "Difference between 1.0 and next representable value: " << std::numeric_limits<T>::epsilon() << "\n";

std::cout << "FLT rounding: 0.5 to nearest digit, 1.0 to 0 or inf";
std::cout << "Maximum rounding error: " << std::numeric_limits<T>::round_error() << "\n";

std::cout << "Return value for quiet NaN: " << std::boolalpha << std::numeric_limits<T>::quiet_NaN() << "\n";
std::cout << "Return value for signaling NaN: " << std::numeric_limits<T>::signaling_NaN() << "\n";

std::cout << "Smallest positive subnormal value: " << std::hex << std::numeric_limits<T>::denorm_min() << "\n";
}

int main()
{
NumericConstants<float>("float");
NumericConstants<double>("double");

NumericFunctions<float>("float");
NumericFunctions<double>("double");

// 100-digit precision type from Boost multiprecision
// Discussed in Appendix C in more detail
namespace mp = boost::multiprecision;
NumericConstants<mp::cpp_dec_float_100>("100-digit type");
NumericFunctions<mp::cpp_dec_float_100>("100-digit type");

NumericConstants<mp::cpp_dec_float_50>("50-digit type");
NumericFunctions<mp::cpp_dec_float_50>("50-digit type");

return 0;
}
```

A subset of the functionality consisting of public static member constants and public static member functions in the class template is:

```cpp
enum float_round_style
{
    round_indeterminate = -1,
    round_toward_zero = 0,
    round_to_nearest = 1,
    round_toward_infinity = 2,
    round_toward_neg_infinity = 3
};
```

## 8.4 An Introduction to Error Analysis

A major topic in numerical analysis and its applications is the study of approximation errors and how errors are propagated in numerical processes and algorithms. In particular, we need some way of quantifying the concept of error because the measurement of data is not precise in general and floating-point data types have a fixed precision. Approximations are used instead of the real or exact data. In other words, we need some way to measure the difference between a floating-point number and the real number that it approximates. To this end, let the value \(a\) be an approximation to the value \(v\). Some examples are:

- Absolute error:
  \[
  \varepsilon = |v-a|.
  \]

- Relative error:
  \[
  \eta = \varepsilon/|v| = \left|\frac{v-a}{v}\right| = \left|1-\frac{a}{v}\right|.
  \]

- Percentage error:
  \[
  \delta = 100\% \times \eta = 100\% \times \varepsilon/|v| = 100\% \times \left|\frac{v-a}{v}\right|.
  \]

The relative error is often used when comparing approximations of numbers of widely different sizes. Second, it makes sense only when the denominator in equations (8.2) and (8.3) is not zero. As an example, if \(v=50\) and \(a=49.9\), then the absolute error is 0.1, the relative error is \(0.1/50 = 0.002\), and the percentage error is 2%.

A round-off error (rounding error) is the difference between the calculated approximation of a number and its exact mathematical value due to rounding. It is important to take this into consideration in numerical analysis and its applications where it is essential to estimate errors in calculations (including round-off errors) when using approximation equations and algorithms, especially when using finitely many digits to represent real numbers (which in theory have infinitely many digits). When a sequence of calculations subject to rounding error is made, errors may accumulate, sometimes dominating the calculation. In ill-conditioned problems, significant errors may accumulate.

We note that these definitions can be extended to cases in which the variables are vectors and matrices. In this case, the concept of the absolute value of a number is replaced by the concepts of vector norm and matrix norm, respectively. We discuss these concepts in more detail in later chapters when we need them in applying the finite difference method, for example.

### 8.4.1 Loss of Significance

This is an undesirable effect in calculations using finite-precision arithmetic. It occurs when an operation on two numbers increases relative error substantially more than it increases absolute error, for example in subtracting two nearly equal numbers (known as catastrophic cancellation). The effect is that the number of significant digits in the result is unacceptably reduced.

## 8.5 Example: Numerical Quadrature

We consider the common case of computing approximate values of one-dimensional integrals. In order to reduce the scope, we focus on Gauss quadrature. This is a popular scheme in computational finance and it is a weighted sum of function values at specified points in the domain of integration. An \(n\)-point Gaussian quadrature rule yields a result that is exact for polynomials of degree \(2n-1\) or less by a suitable choice of integration points and weights. In general, the domain of integration is \([-1,1]\):

\[
\int_{-1}^{1} f(x)\,dx = \sum_{j=1}^{n} w_j f(x_j)
\]

where:

- \(w_j\) = weights, \(x_j\) = integration points, \(j = 1, \ldots, n\).

This formula only produces good results if the function \(f(x)\) can be accurately approximated by a polynomial. For example, it is not suitable for functions with singularities. For a general interval \((a, b)\), the Gauss integration rule becomes:

\[
\int_a^b f(x)\,dx \approx \frac{b-a}{2} \sum_{j=1}^{n} w_j f\left(\frac{b-a}{2} x_j + \frac{a+b}{2}\right).
\]

In this case the related polynomials are Legendre polynomials (Abramowitz and Stegun, 1965, formula 25.4.29).

We now discuss a small C++ software framework for Gauss–Legendre quadrature. We model the following entities:

- The integrand (the function to be integrated).
- The domain of integration.
- The numerical quadrature method.

We model these entities as classes. The class to model the integrand and domain is:

```cpp
#include <functional>
#include <tuple>

template <typename T>
class IIntegration
{
private:
    std::function<T(T x)> f;        // Function to be integrated
    std::tuple<T, T> range;         // Interval of integration

public:
    IIntegration(const std::function<T(T x)>& function,
                 const std::tuple<T, T>& interval)
        : f(function), range(interval) {}

    // Getter functions (V2 A = A(x), B = B(x))
    T A() const
    { // Lower bound
        return std::get<0>(range);
    }

    T B() const
    { // Upper bound
        return std::get<1>(range);
    }

    T operator() (T x)
    {
        return f(x);
    }
};
```

The class that implements Gauss–Legendre quadrature is:

```cpp
template <typename T>
class GaussLegendre
{
private:
    std::vector<T> w;        // Weights
    std::vector<T> x;        // Nodes
    IIntegration<T> fun;     // Function + interval
```

```cpp
0.8391169718222188, -0.9122344282513259, 0.9122344282513259,
-0.963971927779138, 0.963971927779138, -0.9931285991850949,
0.9931285991850949 };

const std::vector<double> wGL20 = { 0.1527533871307258,
0.1527533871307258, 0.1491729864726037, 0.1491729864726037,
0.1420961093183820, 0.1420961093183820, 0.1316886384491766,
0.1316886384491766, 0.1181945319615184, 0.1181945319615184,
0.1019301198172404, 0.1019301198172404, 0.0832767415767048,
0.0832767415767048, 0.0626720483341091, 0.0626720483341091,
0.0406014298003869, 0.0406014298003869, 0.0176140071391521,
0.0176140071391521 };
```

Finally, a test program is:

```cpp
int main()
{
    auto f = [](double x) { return std::exp(x); };
    auto range = std::make_tuple(0.0, 5.0);

    IIntegration<double> integrandInfo(f, range);

    GaussLegendre<double> glIntegrator10(integrandInfo,
                                    wGL10, xGL10);
    std::cout << "Integral 10 nodes: " << std::setprecision(20)
              << glIntegrator10() << '\n';

    GaussLegendre<double> glIntegrator20(integrandInfo,
                                    wGL20, xGL20);
    std::cout << "Integral 20 nodes: " << std::setprecision(20)
              << glIntegrator20() << '\n';

    std::cout << "Exact e^5: " << std::setprecision(20)
              << std::exp(5.0) << '\n';

    return 0;
}
```

The output from this program is:

```cpp
Integral 10 nodes: 147.41315910257662836
Integral 20 nodes: 147.41315910257657151
Exact e^5: 148.41315910257659993
```

This approach can be generalised to numerical quadrature schemes.
