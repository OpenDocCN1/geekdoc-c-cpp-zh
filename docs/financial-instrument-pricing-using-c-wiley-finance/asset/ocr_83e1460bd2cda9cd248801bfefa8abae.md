```
template <class T> class LUTridiagonalSolver
{ // Solve tridiagonal matrix equation
private:

    // Defining arrays (input)
    // V2 optimise so to work with pointers
    Vector<T> a;    // The lower-diagonal array [0..J]
    Vector<T> b;    // The diagonal array [0..J] "baseline array"
    Vector<T> c;    // The upper-diagonal array [0..J]
    Vector<T> r;    // The right-hand side of the equation
                    // Au = r [0..J]

    // Work arrays
    // Coefficients of Lower and Upper matrices: A = LU

    Vector<T> beta; // Range [0..J]
    Vector<T> gamma;// Range [0..J]
                    // Solutions of temporary and final problems
    Vector<T> z;    // Range [0..J]

    std::size_t Size;

    void calculateBetaGamma_ZU(Vector<T>& r)
    {

        // Equation 13.10
        beta[0] = b[0];
        gamma[0] = c[0] / beta[0];

        for (std::size_t j = 1; j < Size - 1; ++j)
        {
            beta[j] = b[j] - (a[j] * gamma[j - 1]);
            gamma[j] = c[j] / beta[j];
        }

        beta[Size - 1] = b[Size - 1] - (a[Size - 1] * gamma[Size - 2]);

        // Calculate z and u
        // Forward direction, equation 13.11
        z[0] = r[0] / beta[0];

        for (std::size_t j = 1; j < Size; ++j)
        {
            z[j] = (r[j] - (a[j] * z[j - 1])) / beta[j];
        }

        // Backward direction, equation 13.12
        r[Size - 1] = z[Size - 1];
```