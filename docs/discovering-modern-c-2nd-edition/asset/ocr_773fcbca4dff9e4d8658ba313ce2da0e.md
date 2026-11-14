```
```cpp
template <typename Matrix>
struct is_matrix<transposed_view<Matrix> >
: is_matrix<Matrix>
{};
// more views ...
```
```