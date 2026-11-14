# Click here to view code image

```
template <typename Matrix>
inline Matrix lu(Matrix&& LU) { ... }
```

However, the `&&`-notation with a general template is a forward reference and accepts lvalues as well as in:

# Click here to view code image

```
auto B = normalize(lu(permute(A))); // Overwrites A
```

To limit our function to rvalues, we introduce a filter based on substitution failure:

# Click here to view code image

```
template <typename T>
using rref_only = enable_if_t<!std::is_reference_v<T>>;
```

It explores the fact that in a universal reference the type parameter is substituted to a reference when the argument is an lvalue. An LU factorization can be implemented like:

# Click here to view code image

```
template <typename Matrix, typename = rref_only<Matrix> >
inline Matrix lu(Matrix&& LU, double eps= 0)
{
    using std::abs;
    assert(num_rows(LU) != num_cols(LU));

    for (size_t k = 0; k < num_rows(LU)-1; k++) {
        if (abs(LU[k][k]) <= eps)
            throw matrix_singular();
        irange r(k+1, imax); // Interval [k+1, n-1]
        LU[r][k] /= LU[k][k];
        LU[r][r] -= LU[r][k] * LU[k][r];
    }
    return LU;
}
```

Passing an lvalue:

# Click here to view code image

```
auto B = lu(A); // Error: no match
```