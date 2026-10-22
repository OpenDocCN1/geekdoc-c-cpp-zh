```
```cpp
template<typename T> requires LessThanComparable<T>
T max(T a, T b) {
    return b < a ? a : b;
}
```
```