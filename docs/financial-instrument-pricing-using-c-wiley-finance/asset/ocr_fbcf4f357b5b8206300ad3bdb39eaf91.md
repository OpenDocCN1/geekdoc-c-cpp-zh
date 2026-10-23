```
```cpp
{
private:
    IFunctionType<T> f;    // Function to be minimised
    T x0;                   // Initial guess
    ITerminationType<T> tol;
    T a, b;
    int incr;
public:
    AitkenFixedPointSolver (const IFunctionType<T>& function, T A, T B,
                            T initialGuess, const ITerminationType<T>&
                            termination)
        : f(function), a(A), b(B), x0(initialGuess), tol(termination), incr(0)
    {}

    //void operator () (T& a, T& b, T& fa, T& fb)
    void operator () ()
    {

        double x1, x2, ait;

        // Kick-off the first 3 values.
        do
        {
            x1 = f(x0);
            x2 = f(x1);

            double den = (x2 - x1) - (x1 - x0);

            double num = x2 - x1;
            ait = x2 - (num*num) / den;

            x0 = ait;
            ++incr;

        } while (!tol(x2, ait));

        a = b = ait;

    }

    T value() const
    {
        return 0.5*(a + b);
    }

    int NumberIterations() const
    {
        return incr;
    }
};
```
```