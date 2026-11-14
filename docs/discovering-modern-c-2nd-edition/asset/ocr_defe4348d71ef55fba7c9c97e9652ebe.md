```
template <typename Value> // #2
std::true_type is_a_matrix(const dense_matrix<Value>&);

template <typename Matrix, typename Functor> // #3
std::true_type is_a_matrix(const map_view<Matrix, Functor>&);
```