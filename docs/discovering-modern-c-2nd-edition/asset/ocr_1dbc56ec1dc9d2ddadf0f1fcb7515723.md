```
template <typename T>
constexpr bool is_matrix_v=
decltype(is_a_matrix(std::declval<T>()))::value;
```