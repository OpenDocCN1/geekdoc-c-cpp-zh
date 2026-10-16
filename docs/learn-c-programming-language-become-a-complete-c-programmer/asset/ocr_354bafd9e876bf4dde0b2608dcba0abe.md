When we reach a list with non`initializer_list` elements, we insert those elements into our `vector`:

```
```cpp
template<typename T, typename Vec>
void add_list(const T* first, const T* last, Vec& vec) {
    vec.insert(vec.end(),first,last);
}
```
```

I use `vec.insert(vec.end(),first,last)` because there is no `push_back()` that takes a sequence argument.

# 29.4.5 Matrix Access

A Matrix provides access by row, column, slice (§29.4.1), and element (§29.4.3). A row() or column() operation returns a Matrix_ref<T,N−1>, the () subscript operation with integers returns a T&, and the () subscript operation with slices returns a Matrix<T,N>.

The row of a Matrix<T,N> is a Matrix_ref<T,N−1> as long as 1<N:

```
```cpp
template<typename T, size_t N>
Matrix_ref<T,N−1> Matrix<T,N>::row(size_t n)
{
    assert(n<rows());
    Matrix_slice<N−1> row;
    Matrix_impl::slice_dim<0>(n,desc,row); return {row,data()};
}
```
```

We need specializations for N==1 and N==0:

```
```cpp
template<typename T>
T& Matrix<T,1>::row(size_t i)
{
    return &elems[i]; }
template<typename T>
T& Matrix<T,0>::row(size_t n) = delete;
```
```

Selecting a column() is essentially the same as selecting a row(). The difference is simply in the construction of the Matrix_slice:

```
```cpp
template<typename T, size_t N>
Matrix_ref<T,N−1> Matrix<T,N>::column(size_t n)
{
    assert(n<cols());
    Matrix_slice<N−1> col;
    Matrix_impl::slice_dim<1>(n,desc,col);
```
```