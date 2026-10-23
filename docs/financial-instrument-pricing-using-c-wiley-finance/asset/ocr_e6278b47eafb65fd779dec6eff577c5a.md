Finally, we show how to compute quantiles and the number of degrees of freedom needed in the t-distribution for a given significance level:

```
// Quantiles and conversions between significance levels
// (fractions, 0.05) and confidence levels (in percentages,
// e.g. 95%)
double Alpha = 0.25;
cout << "Confidence 1: "
    << quantile(myStudent, Alpha / 2) << endl;
cout << "Confidence, in %: "
    << quantile(complement(myStudent, Alpha / 2)) << endl;

// Required sample sizes for Students t-distribution
double M = 1.2;    // True mean
double Sm = 1.8;   // Sample mean
double Sd = 2.4;   // Sample standard deviation
try
{
    double df = students_t::find_degrees_of_freedom (fabs(M-Sm), Alpha,
        Alpha, Sd);
    int dof = ceil(df) + 1;
    cout << "One-sided degrees of freedom: " << dof << endl;
}
catch(const std::exception& e)
{
    cout << e.what() << endl;
}
```

# 15.7 ADVANCED DISTRIBUTIONS

There are approximately 35 classes in the Boost Statistics library, each of which models a particular univariate distribution. In order to avoid code duplication we have created a single generic class that encapsulates common properties and algorithms. The design rationale is similar to that of the generic class that we created in Section 15.5.2 where we created generic code to generate random numbers. In particular, we create an adapter class that supports all distributions and that uses variadic arguments in its constructor. Its interface mimics the corresponding Boost interface in the sense that we use the same member function names (notice that we use the template–template parameter trick):

```
template <typename T, template <typename T> class Dist>
    class Distribution
{
private:
    Dist<T> dist;
public:
    template <typename... Args>
    Distribution(Args... args) : dist(Dist<T>(args...)) {}
```