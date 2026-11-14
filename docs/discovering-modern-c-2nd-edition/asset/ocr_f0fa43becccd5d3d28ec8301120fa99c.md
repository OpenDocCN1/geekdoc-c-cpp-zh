```
struct scale_functor
{
    scale_functor(int factor) : factor(factor) {}
    int operator()(int x) const { return factor * x; }
    int factor;
};
```

```
template <typename Matrix>
struct scale_view
    : map_view<Matrix, scale_functor>
{
    scale_view(const Matrix& A, int factor) : A(A), f(factor) {}
    const Matrix& A;
    scale_functor f;
};
```