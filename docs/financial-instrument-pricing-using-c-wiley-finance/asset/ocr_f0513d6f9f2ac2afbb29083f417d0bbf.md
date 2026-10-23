```
for (long i = Size - 2; i >= 0; --i)
{
    r[i] = z[i] - (gamma[i] * r[i + 1]);
}

}

public:
    LUTridiagonalSolver() = delete;
    LUTridiagonalSolver(const LUTridiagonalSolver<T>& source) = delete;
    virtual ~LUTridiagonalSolver() = default;
    LUTridiagonalSolver<T>& operator = (const LUTridiagonalSolver<T>& source) = delete;

    LUTridiagonalSolver(Vector<T>& lower, Vector<T>& diagonal, Vector<T>& upper, Vector<T>& RHS)
    {
        a = lower;
        b = diagonal;
        c = upper;
        r = RHS;

        Size = diagonal.size();

        beta = Vector<T>(Size);
        gamma = Vector<T>(Size);

        z = Vector<T>(Size);
    }

Vector<T> solve()
{
    calculateBetaGamma_ZU(r);      // Calculate beta and gamma

    return r;
}

Vector<T> operator () ()
{
    return solve();
}

bool diagonallyDominant() const
{
    if (std::abs(b[0]) < std::abs(c[0]))
        return false;

    if (std::abs(b[Size - 1]) < std::abs(a[Size - 1]))
        return false;
```