=> c++14/matrix_access_example.cpp

The CRTP idiom allows us to tackle a problem mentioned earlier (§2.6.4): accessing multidimensional data structures with the bracket operator in a reusable implementation. At the time we did not know the necessary language features, especially templates and inheritance. Now we do and will apply this knowledge to realize two bracket operator calls by one of a binary call operator, i.e., evaluate A[i][j] as A(i, j).

Say we have a matrix type going by the elegant name `some_matrix` whose `operator() a_ij`. For consistency with the vector notation, we prefer bracket operators. Those accept only one argument, and we therefore need a proxy that represents the access to a matrix row. This proxy in turn provides a bracket operator for accessing a column in the corresponding row, i.e., yields an element of the matrix:

Click here to view code image

```
class some_matrix; // Forward declaration

class simple_bracket_proxy
{
public:
    simple_bracket_proxy(some_matrix& A, size_t r)
    : A(A), r(r) {}

    double& operator[](size_t c) { return A(r, c); } // Error

private:
    some_matrix& A;
    size_t     r;
};

class some_matrix
{
    // ...
    double& operator() (size_t r, size_t c) { ... }

    simple_bracket_proxy operator[](size_t r)
    {
        return simple_bracket_proxy(*this, r);
    }
};
```

The idea is that A[i] returns a proxy p referring to A and containing i. Calling A[i][j] corresponds to p[j] which in turn should call A(i, j).