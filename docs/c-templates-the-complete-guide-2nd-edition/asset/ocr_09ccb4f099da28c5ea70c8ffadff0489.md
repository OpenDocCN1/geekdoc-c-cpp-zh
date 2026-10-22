```
template<typename T>
struct RParam<Array<T>> {
    using Type = Array<T> const&;
};
```