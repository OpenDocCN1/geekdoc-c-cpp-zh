```
```cpp
private:
    IFunctionType<T> f;    // Function to be minimised
    T x0;                   // Initial guess
    ITerminationType<T> tol;
    T a, b;
    int incr;
public:
    BanachFixedPointSolver
        (const IFunctionType<T>& function, T A, T B, T initialGuess,
         const ITerminationType<T>& termination)
        : f(function), a(A), b(B), x0(initialGuess), tol(termination), incr(0)
    {
    }

    void operator () ()
    {
        double x1, x2;

        do
        {
            x1 = f(x0);
            x2 = f(x1);

            x0 = x2;
            ++incr;

        } while (!tol(x2, x1));

        a = x1;
        b = x2;
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

and the class implementing the Aitken algorithm is given by:

```
```cpp
template <typename T>
    class AitkenFixedPointSolver
```
```