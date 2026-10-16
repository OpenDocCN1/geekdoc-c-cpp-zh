```
template<size_t N>
template<typename... Dims>
size_t Matrix_slice<N>::operator()(Dims... dims) const {
static_assert(sizeof...(Dims) == N, "");
size_t args[N] { size_t(dims)... }; // Copy arguments into an array
return inner_product(args,args+N,strides.begin(),size_t(0));
}
```

Subscripting must be efficient. This is a simplified algorithm that needs to be optimized. If nothing else, specialization can be used to eliminate the simplifying copy of subscripts out of the variadic template’s parameter pack. For example:

```
template<>
struct Matrix_slice<1> {
// ...
size_t operator()(size_t i) const
{
return i;
}
}
```

```
template<>
struct Matrix_slice<2> {
// ...
size_t operator()(size_t i, size_t j) const
{
return i*strides[0]+j;
}
}
```

The Matrix_slice is fundamental for defining the shape of a Matrix (its extents) and for implementing N-dimensional subscripting. However, it is also useful for defining submatrices.

# 29.4.3 Matrix_ref

A Matrix_ref is basically a clone of the Matrix class used to represent subMatrices. However, a Matrix_ref does not own its elements. It is constructed from a Matrix_slice and a pointer to elements:

```
template<typename T, size_t N>
class Matrix_ref {
public:
Matrix_ref(const Matrix_slice<N>& s, T* p) :desc{s}, ptr{p} {}
// ... mostly like Matrix...
```