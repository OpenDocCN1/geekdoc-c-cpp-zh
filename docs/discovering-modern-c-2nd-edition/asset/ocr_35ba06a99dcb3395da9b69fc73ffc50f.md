```
template <typename T>
enable_if_t<is_matrix<T>::value && !is_sparse_matrix<T>::value,
        Magnitude_t<T> >
one_norm(const T& A);
```

```
template <typename T>
enable_if_t<is_sparse_matrix<T>::value, Magnitude_t<T> >
one_norm(const T& A);
```