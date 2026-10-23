```
// Interface I1. Scalar-valued functions of a single variable
template <typename T>
    using IFunctionType = std::function<T (T)>;

// 2. Termination I2; test if interval [a,b] is less than a TOL
template <typename T>
    using ITerminationType = std::function<bool (T a, T b)>;

// 3. Solver I3; compute new interval [a,b] and values
template <typename T>
    using ISolverType = std::function<void (T& a,T& b,T& fa,T& fb)>;

// 4. Progress MIS component i4; send current interval [a,b] and the
// function values at a and b.
template <typename T>
    using IMISType = std::function<void (T a, T b, T fa, T fb)>;

// 5. Core data to client I5, i.e. comprising a, b, fa, fb. A function
// that returns a tuple
template <typename T>
    using IReportType = std::function<void(T a, T b, T fa, T fb)>;;

#endif
```

When using this software framework we can instantiate these interfaces using function objects, lambda functions, free functions or binded member functions. We have created classes for the following algorithms: three-point interval search, golden-mean search, fixed-point iteration and Aitken. We have also created an adapter class that delegates to the Brent solver in the Boost C++ Math Toolkit library. For example, the code for the three-point interval search method is:

```
template <typename T>
    class ThreePointIntervalSolver
{
private:
    IFunctionType<T> f;      // Function to be minimised

    // Extra vars
    T h, a1, a2, a3, fa1, fa2, fa3;
    T a, b;

public:
    ThreePointIntervalSolver(const IFunctionType<T>& function, T A, T B)
        : f(function)
    {
        // std::cout << "3-pt scheme\n";
        // Iniitialisation
        h = 0.25 * std::abs(B-A);
        a = (A < B) ? A : B;
        a1 = a + h;
```