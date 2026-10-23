arguments are the integrand, the interval of integration and the number of subdivisions of the interval:

```
// Define interfaces
typedef std::function<double (double x)> Function;
typedef std::function<double (const Function& fun,
    const Range<double>& range, std::size_t N)> QuadMethod;
```

An important remark is that all quadrature methods accept three arguments representing objects that are created elsewhere. This ensures that the code for numerical quadrature is not hampered by our having to construct objects in addition to implementing an algorithm (this is an example of the Single Responsibility Principle (SRP)). These construction activities are encapsulated in a dedicated class:

```
class NumericalIntegrator
{
public:    // Convenience only
    Function fun;
    Range<double> ran;
    QuadMethod quad;

    // Call the quad scheme as a function object
    double operator () (std::size_t N) { return quad(fun, ran, N);}
};
```

This is a generic and customisable class. Clients choose which functions to integrate and which numerical quadrature schemes to use. For example, we test the following functions:

```
// Test data
double func(double x)
{
    return x*x*x*x + 1;
}

double func2(double x)
{
    return exp(-x);
}
```

Furthermore, we have implemented two specific schemes (in this case we use random number generators from the Boost Random library):

```
double MidpointRule(const Function& fun, const Range<double>& range,
    std::size_t N)
{ // Global C function (based on Duffy 2004)

double A = range.low();
double B = range.high();
```