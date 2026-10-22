```
```cpp
template<typename T> constexpr std::size_t SZ = sizeof(T);

template<typename T> constexpr std::size_t SZ<T&> = sizeof(void*);
```
```