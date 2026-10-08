```
template<typename T, typename U = T>
concept Arithmetic = Number<T,U> && Number<U,T>;
```