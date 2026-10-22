```
```cpp
std::remove_const_t<std::remove_reference_t<int const&>>  // int
std::remove_reference_t<std::remove_const_t<int const&>> // int const
```
```